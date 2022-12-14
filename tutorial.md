# מדריך nasm x86 מקוצר #

## אוגרים ##
אוגרים הם משתנים כללים שניתן להפעיל עליהם פקודות
האוגרים בעלי 32 ביטים:

* eax
* ebx
* ecx
* edx
* ebp - מיועד לשמירת מיקום במחסנית
* esi - מיועד לשמירת כתובת בזיכרון
* edi - מיועד לשמירת מיקום בזיכרון
* eip - לא ניתן לשנות אותו - שומר את המיקום בו מתבצעת פקודה כלשהיא
* esp - מצביע למיקום האחרון במחסנית
* eflags - לא ניתן לשנות, כאן הדגלים נשמרים

בתוך האוגרים eax,ebx,ecx,edx קיימים אוגרים בעלי 16 ביטים (16 הביטים האחרונים (הקטנים)):  
* ax - eax
* bx - ebx
* cx - edx
* dx - ecx

אז לדוגמה:  
```
eax = 0x12345678 // 32bit
means
ax  = 0x5678     // 16bit
```
בתוך כל אוגר מסוג 16 ביטים קיימים שני אוגרים בעלי 8 ביטים, 8 הביטים הראשונים (h - high) ו8 הביטים האחרונים (l - low):  
* al - low ax
* ah - high ax
* bl - low bx
* bh - high bx
* cl - low cx
* ch - high cx
* dl - low dx
* dh - high dx

אז לדוגמה:  
```
eax = 0x12345678 // 32bit
means:
ax  = 0x5678     // 16bit
al  = 0x78       // 8bit
ah  = 0x56       // 8bit
```

## hello world (SASM) ##
אם הורדתם sasm כך תראה תוכנית hello world שלא באמת תדפיס hello world אלא היא תדפיס 100:  
```nasm
%include "io.inc"
section .text
global CMAIN
CMAIN:
    mov eax, 100
    PRINT_DEC 4, eax
    ret
```
נעבור שורה שורה:  
```nasm
%include "io.inc"
```
כולל את הקובץ `io.inc` שנותן לנו את האופציה להדפיס למסך, חלק מהפרוייקט של sasm  
```nasm
section .text
```
אנחנו מתחילים את החלק בו יש קוד

```nasm
global CMAIN
CMAIN:
```
הפעולה הראשית שבה הקוד רץ

```nasm
mov eax, 100
```
שם באוגר eax את הערך 100

```nasm
PRINT_DEC 4, eax
```
מדפיס אוגר בעל 4 בתים (כל בית הוא 8 ביטים ולכן אפשר להגיד שבעל 32 ביטים)

```nasm
ret
```
מסיים את התוכנית וחוזר למערכת ההפעלה

## immediate ##
כאשר ברשימת הפקודות כתוב imm זה אומר שניתן לשים מספר (כמו שראינו בתוכנית הhello world עם הפקודה mov)  
ניתן לכתוב מספרים מסומנים או לא מסומנים  
לדוגמה:  
```nasm
mov al, 255
mov al, -1
```
ניתן גם לשים תווין ומה שנקבל הוא ערך האסקי שלהם לדוגמה:  
```nasm
mov al, 'A'
```
ישים באוגר al את הערך 65  
שני הפקודות זהות מכיוון שבשניהם מכניסים לתוך האוגר את אותו ערך (הסתכלו בשיטת המשלים ל2 (על 8 ביטים))  
ניתן גם לשים מספרים בבסיסים שונים:
* hex  
  * `0x?`  
    ניתן לכתוב את הספרות בהקסה לאחר `0x\0X` 
  * `0h?`  
    ניתן לכתוב את הספרות בהקסה לאחר `0h\0H` 
  * `?x`  
    ניתן לכתוב את הספרות בהקסה לפני `X\x` רק חייבים להתחיל בספרה בין אפס לתשע, אם המספר לא מתחיל בספרה כזאת אפשר לשים אפס לפני
  * `?h`  
    ניתן לכתוב את הספרות בהקסה לפני `H\h` רק חייבים להתחיל בספרה בין אפס לתשע, אם המספר לא מתחיל בספרה כזאת אפשר לשים אפס לפני
  ```nasm
  mov al, 0XAb
  mov al, 0xAb
  mov al, 0haB
  mov al, 12h
  mov al, 0abH
  ```
* octal  
  * `0o?`  
    ניתן לכתוב את הספרות בהקסה לאחר `0o\0O` 
  `?o`  
    ניתן לכתוב את הספרות בהקסה לפני `O\o`
  ```nasm
  mov al, 0o11
  mov al, 11o
  ```
* binary  
  * `0b?`  
    ניתן לכתוב את הספרות בהקסה לאחר `0b\0B` 
  `?b`  
    ניתן לכתוב את הספרות בהקסה לפני `B\b`
  ```nasm
  mov al, 0b11
  mov al, 11b
  ```

## הערות ##
כל מה שבא בשורה לאחר ; אינו נחשב חלק מהקוד והקומפיילר אינו מתייחס אליו

## זיכרון ##
ניתן לשמור בזיכרון עוד משתנים
### `section .data` ###
באיזור הזה שומרים מערכי משתנים שערכם בתחילת התוכנית צריך להיות ידוע מראש והסינטקס הוא כזה:  
```nasm
<name> (`:` not needed) <type> <value1>, <value2>, <value3>, ...
```
ניתן גם להגיד שרוצים כמה פעמים יהיה את אותו ערך:  
```nasm
<name> (`:` not needed) <num_of_times> times <type> <value1>, <value2>, <value3>, ...
```
* `type`  
  הסוגים האפשריים הם
  * `db` - define byte - הגדרת משתנה בעל 8 ביטים
  * `dw` - define word - הגדרת משתנה בעל 16 ביטים 
  * `dd` - define double word - הגדרת משתנה בעל 32 ביטים 

וכך ניצור לדוגמה מערכים:  
```nasm
section .data
arr1: 2 times db 10, 20; arr1 = [10,20,10,20]
arr2 dw 0x1010, 1234h; arr1 = [0x1010,0x1234] 
var1 dd 0xC0FFEE
```
הבתים מוגדרים בזיכרון בlittle endian
כלומר בזיכרון קודם כל מופיעים הבתים הפחות משמעותיים בכל מספר לדוגמה אצלינו בדוגמה הזיכרון יראה כך:  
`0x0a|0x14|0x0a|0x14|0x10|0x10|0x34|0x34|0xEE|0xFF|0xC0|0x00`  
שימו לב שיש 00 בסוף מכיוון שאולי לא רואים אותם אבל המספר האחרון מוגדר כדאבלוורד כלומר יש בו 4 בתים
ניתן גם לכתוב תווים ברצף ע"י שימוש ב`"` כל תו הוא בית והם יבואו לפי הסדר שבו כתבו אותם כלומר:  
```nasm
var1 dd "Hello"
```
המקום בזיכרון לפי בתים יראה כך:  
`0x48|0x65|0x6c|0x6c|0x6f|0x00|0x00|0x00`  

### `section .bss` ###
באזור הזה שומרים בזיכרון מערכים בלי להכניס אליהם ערך התחלתי בסינקס הבא:  
```nasm
section .bss
<name> <`resb`\`resw`\`resd`> <num of elements>
```
* `resb` - reserve byte - הגדרה של בתים (8 ביט)
* `resw` - reserve word - הגדרה של מילים (16 ביט) 
* `resd` - reserve double word - הגדרה של ילים כפולות (32 ביט)  

כלומר הקוד הבא ישמור 8000 בתים:  
```nasm
arr resb 1000
```
הקוד שקול בדיוק לקוד הבא:  
```nasm
arr resw 500
```
או לקוד הבא:  
```nasm
arr resd 250
```

## חוקיות פקודות ##
פקודה היא חוקים אם היא מופיעה ברשימת הפקודות ואי אפשר להתבלבל בינה לבין פקודה אחרת, לדוגמה:  
```nasm
; legal commands
add eax, ebx      ; exist `add r32, r32/m32/im32`
add al, bl        ; exist `add r8, r8/m8/im8`
add byte[eax], 10 ; exist `add m8 r8/im8`
add [eax], al     ; exist `add m8 r8/im8`

; illigal commands
add byte[eax], byte[ebx] ; not exist `add m8, m8`
add [eax], 10            ; exist     `m8 r8/m8` and `m16 r16/m16` and `m32 r32/m32`
add byte[eax], ax        ; not exist `add m8 r16`
```