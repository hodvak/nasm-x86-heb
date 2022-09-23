# x86 Instruction Set (Short) #

## MOV ##
move  
השמה של ערך בתוך אוגר/זיכרון
הסינטקס:

```nasm
mov dest, source
```

| code                    | explain             |
|-------------------------|---------------------|
| `mov r8 , r8 / m8/ im8` | move source to dest |
| `mov r16, r16/m16/im16` | move source to dest |
| `mov r32, r32/m32/im32` | move source to dest |
| `mov m8 , r8 / im8`     | move source to dest |
| `mov m16, r16/im16`     | move source to dest |
| `mov m32, r32/im32`     | move source to dest |

הפעולה:

```c
dest = source;
```

דגלים:  
הדגלים אינם משתנים

## XCHG ##
xchange  
החלפה בין שני משתנים
הסינטקס:

```nasm
xchg var1, var2
```

| code                | explain                |
|---------------------|------------------------|
| `xchg r8 , r8 / m8` | xchange var1 with var2 |
| `xchg r16, r16/m16` | xchange var1 with var2 |
| `xchg r32, r32/m32` | xchange var1 with var2 |
| `xchg m8 , r8 `     | xchange var1 with var2 |
| `xchg m16, r16`     | xchange var1 with var2 |
| `xchg m32, r32`     | xchange var1 with var2 |

הפעולה:

```c
temp = var1;
var1 = var2;
var2 = temp;
```

דגלים:  
הדגלים אינם משתנים

## MOVSX / MOVZX ##
move sign extend / move zero extend  
השמה של ערך בתוך אוגר של אוגר/זיכרון קטן ממנו  
* movzx - משספרים לא מסומנים
* movsx - למספרים מסומנים  

הסינטקס:

```nasm
movzx dest, source
```

| code                             | explain             |
|----------------------------------|---------------------|
| `movzx/movsx r16, r8/m8/`        | move source to dest |
| `movzx/movsx r32, r8/m8/r16/m16` | move source to dest |

הפעולה:

```c
dest = source;
```

דגלים:  
הדגלים אינם משתנים

## CDQ ##
מרחיב את eax כך שיהיה על  
edx:eax  
כמספר מסומן  
כלומר לוקח את הMSB ו"מורח" אותו על כל edx
```nasm
cdq ; edx:eax = eax
```

## ADD ##

חיבור בין שני מספרים (מסומנים או לא מסומנים)
הסינטקס:

```nasm
add dest, source
```

| code                    | explain            |
|-------------------------|--------------------|
| `add r8 , r8 / m8/ im8` | add source to dest |
| `add r16, r16/m16/im16` | add source to dest |
| `add r32, r32/m32/im32` | add source to dest |
| `add m8 , r8 / im8`     | add source to dest |
| `add m16, r16/im16`     | add source to dest |
| `add m32, r32/im32`     | add source to dest |

הפעולה:

```c
dest = dest + source;
```

דגלים:

* zf = האם התוצאה היא 0
* cf = האם הייתה טעות עבור מספרים לא מסומנים
* af = האם הייתה טעות חישוב אם היינו מסתכלים רק על הניבל השמאלי ביותר
* of = האם הייתה טעות במספרים מסומנים
* sf = האם התואה נחשבת שלילית (כמספר מסומן)
* pf = האם יש מספר זוגי של ביטים דלוקים בבית הימני ביותר של התוצאה

## INC ##
increase   
הוספה של 1  

```nasm
inc dest
```

| code          | explain       |
|---------------|---------------|
| `inc r8 /m8`  | add 1 to dest |
| `inc r16/m16` | add 1 to dest |
| `inc r32/m32` | add 1 to dest |


הפעולה:

```c
dest = dest + 1;
```

דגלים:

* zf = האם התוצאה היא 0
* cf = cf (לא משתנה)
* af = האם הייתה טעות חישוב אם היינו מסתכלים רק על הניבל השמאלי ביותר
* of = האם הייתה טעות במספרים מסומנים
* sf = האם התואה נחשבת שלילית (כמספר מסומן)
* pf = האם יש מספר זוגי של ביטים דלוקים בבית הימני ביותר של התוצאה

## SUB ##
subtract  
חיסור בין שני מספרים (מסומנים או לא מסומנים)
הסינטקס:

```nasm
sub dest, source
```

| code                    | explain              |
|-------------------------|----------------------|
| `sub r8 , r8 / m8/ im8` | sub source from dest |
| `sub r16, r16/m16/im16` | sub source from dest |
| `sub r32, r32/m32/im32` | sub source from dest |
| `sub m8 , r8 / im8`     | sub source from dest |
| `sub m16, r16/im16`     | sub source from dest |
| `sub m32, r32/im32`     | sub source from dest |

הפעולה:

```c
dest = dest - source;
```

דגלים:
* zf = האם התוצאה היא 0
* cf = האם הייתה טעות עבור מספרים לא מסומנים
* af = האם הייתה טעות חישוב אם היינו מסתכלים רק על הניבל השמאלי ביותר
* of = האם הייתה טעות במספרים מסומנים
* sf = האם התואה נחשבת שלילית (כמספר מסומן)
* pf = האם יש מספר זוגי של ביטים דלוקים בבית הימני ביותר של התוצאה

## DEC ##
decrease  
הורדה של 1  

```nasm
dec dest
```

| code          | explain       |
|---------------|---------------|
| `dec r8 /m8`  | sub 1 to dest |
| `dec r16/m16` | sub 1 to dest |
| `dec r32/m32` | sub 1 to dest |


הפעולה:

```c
dest = dest - 1;
```

דגלים:

* zf = האם התוצאה היא 0
* cf = cf (לא משתנה)
* af = האם הייתה טעות חישוב אם היינו מסתכלים רק על הניבל השמאלי ביותר
* of = האם הייתה טעות במספרים מסומנים
* sf = האם התואה נחשבת שלילית (כמספר מסומן)
* pf = האם יש מספר זוגי של ביטים דלוקים בבית הימני ביותר של התוצאה

## ADC ##
add with carry  
חיבור בין שני מספרים (מסומנים או לא מסומנים) והוספה של דגל הנשא
הסינטקס:

```nasm
adc dest, source
```

| code                    | explain                      |
|-------------------------|------------------------------|
| `adc r8 , r8 / m8/ im8` | add source and carry to dest |
| `adc r16, r16/m16/im16` | add source and carry to dest |
| `adc r32, r32/m32/im32` | add source and carry to dest |
| `adc m8 , r8 / im8`     | add source and carry to dest |
| `adc m16, r16/im16`     | add source and carry to dest |
| `adc m32, r32/im32`     | add source and carry to dest |

הפעולה:

```c
dest = dest + (source + cf);
```

דגלים:
* zf = האם התוצאה היא 0
* cf = האם הייתה טעות עבור מספרים לא מסומנים
* af = האם הייתה טעות חישוב אם היינו מסתכלים רק על הניבל השמאלי ביותר
* of = האם הייתה טעות במספרים מסומנים
* sf = האם התואה נחשבת שלילית (כמספר מסומן)
* pf = האם יש מספר זוגי של ביטים דלוקים בבית הימני ביותר של התוצאה

## SBB ##
subtract with borrow
חיסור בין שני מספרים (מסומנים או לא מסומנים) וחיסור דגל הנשא
הסינטקס:

```nasm
sbb dest, source
```

| code                    | explain                     |
|-------------------------|-----------------------------|
| `sbb r8 , r8 / m8/ im8` | sub source and cf from dest |
| `sbb r16, r16/m16/im16` | sub source and cf from dest |
| `sbb r32, r32/m32/im32` | sub source and cf from dest |
| `sbb m8 , r8 / im8`     | sub source and cf from dest |
| `sbb m16, r16/im16`     | sub source and cf from dest |
| `sbb m32, r32/im32`     | sub source and cf from dest |

הפעולה:

```c
dest = dest - (source + cf);
```

דגלים:

* zf = האם התוצאה היא 0
* cf = האם הייתה טעות עבור מספרים לא מסומנים
* af = האם הייתה טעות חישוב אם היינו מסתכלים רק על הניבל השמאלי ביותר
* of = האם הייתה טעות במספרים מסומנים
* sf = האם התואה נחשבת שלילית (כמספר מסומן)
* pf = האם יש מספר זוגי של ביטים דלוקים בבית הימני ביותר של התוצאה

##  AND ##

מפעיל שער "וגם" על כל הביטים

```nasm
and dest, source
```

| code                    | explain            |
|-------------------------|--------------------|
| `and r8 , r8 / m8/ im8` | source and dest    |
| `and r16, r16/m16/im16` | source and dest    |
| `and r32, r32/m32/im32` | source and dest    |
| `and m8 , r8 / im8`     | source and dest    |
| `and m16, r16/im16`     | source and dest    |
| `and m32, r32/im32`     | source and dest    |

הפעולה:

```c
dest = dest & source;
```

דגלים:

* zf = האם התוצאה היא 0
* cf = 0
* af = ?
* of = 0
* sf = האם התואה נחשבת שלילית (כמספר מסומן)
* pf = האם יש מספר זוגי של ביטים דלוקים בבית הימני ביותר של התוצאה

##  OR ##

מפעיל שער "או" על כל הביטים

```nasm
or dest, source
```

| code                    | explain        |
|-------------------------|----------------|
| `and r8 , r8 / m8/ im8` | source or dest |
| `and r16, r16/m16/im16` | source or dest |
| `and r32, r32/m32/im32` | source or dest |
| `and m8 , r8 / im8`     | source or dest |
| `and m16, r16/im16`     | source or dest |
| `and m32, r32/im32`     | source or dest |

הפעולה:

```c
dest = dest | source;
```

דגלים:

* zf = האם התוצאה היא 0
* cf = 0
* af = ?
* of = 0
* sf = האם התואה נחשבת שלילית (כמספר מסומן)
* pf = האם יש מספר זוגי של ביטים דלוקים בבית הימני ביותר של התוצאה

##  XOR ##

מפעיל שער "או" על כל הביטים

```nasm
xor dest, source
```

| code                    | explain         |
|-------------------------|-----------------|
| `and r8 , r8 / m8/ im8` | source xor dest |
| `and r16, r16/m16/im16` | source xor dest |
| `and r32, r32/m32/im32` | source xor dest |
| `and m8 , r8 / im8`     | source xor dest |
| `and m16, r16/im16`     | source xor dest |
| `and m32, r32/im32`     | source xor dest |

הפעולה:

```c
dest = dest ^ source;
```

דגלים:

* zf = האם התוצאה היא 0
* cf = 0
* af = ?
* of = 0
* sf = האם התואה נחשבת שלילית (כמספר מסומן)
* pf = האם יש מספר זוגי של ביטים דלוקים בבית הימני ביותר של התוצאה

## NOT ##
הפיכת כל הביטים הדולקים למכובים וכל הביטים המכובים לדולקים
```nasm
not dest
```

| code          | explain |
|---------------|---------|
| `not r8 /m8`  |         |
| `not r16/m16` |         |
| `not r32/m32` |         |


הפעולה:

```c
dest = ~dest;
//////////////
dest = dest ^ 0xffff..;
//////////////
dest = -dest - 1;
```

דגלים:
לא משתנים

## NEG ##
הפיכת מספר שלילי לחיובי וחיובי לשלילי (ע"י שיטת המשלים ל2)
```nasm
neg dest
```

| code          | explain |
|---------------|---------|
| `neg r8 /m8`  |         |
| `neg r16/m16` |         |
| `neg r32/m32` |         |

הפעולה:

```c
dest = -dest;
/////////////
dest = (~dest) + 1;
```

דגלים:
* zf = האם התוצאה היא 0
* cf = האם התוצאה היא לא 0
* af = אם הניבל (הספרה בהקסהדצימלי) הימני ביותר של התוצאה הוא 0
* of = האם הייתה טעות במספרים מסומנים (קורה רק עבור מספרים בהם הביט השמאלי ביותר 1 והשאר 0)
* sf = האם התואה נחשבת שלילית (כמספר מסומן)
* pf = האם יש מספר זוגי של ביטים דלוקים בבית הימני ביותר של התוצאה

## CMP ##
משנה את הדגלים בדיוק כמו  
sub
אך בלי לשנות את הפרמטירים שהוכנסו אליו
```nasm
cmp var1, var2
```  

| code                    | explain     |
|-------------------------|-------------|
| `cmp r8 , r8 / m8/ im8` | var1 - var2 |
| `cmp r16, r16/m16/im16` | var1 - var2 |
| `cmp r32, r32/m32/im32` | var1 - var2 |
| `cmp m8 , r8 / im8`     | var1 - var2 |
| `cmp m16, r16/im16`     | var1 - var2 |
| `cmp m32, r32/im32`     | var1 - var2 |


הפעולה:  

```nasm
temp = var1 - var2;
```
דגלים:

* zf = האם התוצאה היא 0
* cf = האם הייתה טעות עבור מספרים לא מסומנים
* af = האם הייתה טעות חישוב אם היינו מסתכלים רק על הניבל השמאלי ביותר
* of = האם הייתה טעות במספרים מסומנים
* sf = האם התואה נחשבת שלילית (כמספר מסומן)
* pf = האם יש מספר זוגי של ביטים דלוקים בבית הימני ביותר של התוצאה

## TEST ##
משנה את הדגלים בדיוק כמו ש  
and  
עושה  
רק בלי לשנות את הפרמטרים שמכניסים אליו
```nasm
test var1, var2
```

| code                     | explain       |
|--------------------------|---------------|
| `test r8 , r8 / m8/ im8` | var1 and var2 |
| `test r16, r16/m16/im16` | var1 and var2 |
| `test r32, r32/m32/im32` | var1 and var2 |
| `test m8 , r8 / im8`     | var1 and var2 |
| `test m16, r16/im16`     | var1 and var2 |
| `test m32, r32/im32`     | var1 and var2 |

הפעולה:

```c
temp = dest & source;
```

דגלים:
* zf = האם התוצאה היא 0
* cf = 0
* af = ?
* of = 0
* sf = האם התואה נחשבת שלילית (כמספר מסומן)
* pf = האם יש מספר זוגי של ביטים דלוקים בבית הימני ביותר של התוצאה

## STC / STD / CLC / CLD ##
set carry / set direction / clear carry / clear diraction  
משנה רק את דגלי הנשא והכיוון לפי הפעולה
```nasm
stc ; cf = 1
clc ; cf = 0
std ; df = 1
cld ; df = 0
```

## MUL ##
כפל בין מספרים לא מסומנים
```nasm
mul var1
```
| code          | explain                        |
|---------------|--------------------------------|
| `mul r8 /m8`  | var2 is al, result is ax       |
| `mul r16/m16` | var2 is ax, result is dx:ax    |
| `mul r32/m32` | var2 is eax, result is edx:eax |

הפעולה:  
```nasm
result = var1 * var2;
```
דגלים:  
דגלי הנשא והגלישה יהיו מוגדרים 0 אם התוצאה הייתה נכנסת גם לאוגר מאותו גודל של הפרמטר.  
כל שאר הדגלים יהיו לא מוגדרים
* zf = ?
* cf = התוצאה הייתה נכנסת גם לאוגר מאותו גודל של הפרמטר
* af = ?
* of = התוצאה הייתה נכנסת גם לאוגר מאותו גודל של הפרמטר
* sf = ?
* pf = ?

## DIV ##
חילוק בין מספרים לא מסומנים
```nasm
div devider
```
| code          | explain                                              |
|---------------|------------------------------------------------------|
| `div r8 /m8`  | source is ax, result is al and reminder is ah        |
| `div r16/m16` | source is dx:ax, result is ax and reminder is dx     |
| `div r32/m32` | source is edx:eax, result is eax and reminder is edx |

הפעולה:  
```nasm
temp = source;
result = temp/devider;
reminder = temp%devider;
```
אם התוצאה לא יכולה להיכנס לאן שהיא אמורה (התוצאה עצמה או השארית) התוכנית תקרוס
דגלים:  
כל הדגלים לא מוגדרים:
* zf = ?
* cf = ?
* af = ?
* of = ?
* sf = ?
* pf = ?

## IMUL ##

כפל בין מספרים מסומנים
```nasm
imul var1
imul var1 and dest, var2
imul dest, var1, var2
```
| code                      | explain                                    |
|---------------------------|--------------------------------------------|
| `imul r8 /m8`             | var2 is al, dest is ax                     |
| `imul r16/m16`            | var2 is ax, dest is dx:ax                  |
| `imul r32/m32`            | var2 is eax, dest is edx:eax               |
| `imul r16, r16/m16`       | var1 and dest are the same first parameter |
| `imul r32, r32/m32`       | var1 and dest are the same first parameter |
| `imul r16, r16/m16, im16` |                                            |
| `imul r32, r32/m32, im32` |                                            |

הפעולה:  
```nasm
dest = var1 * var2;
```
אם אין מספיק מקום בdest מעלימים את החלק שגלש
דגלים:  
דגלי הנשא והגלישה יהיו מוגדרים 0 אם התוצאה הייתה נכנסת (ונכונה במספרים מסומנים) גם לאוגר מאותו גודל של הפרמטר.  
כל שאר הדגלים יהיו לא מוגדרים
* zf = ?
* cf = התוצאה הייתה נכנסת גם לאוגר מאותו גודל של הפרמטר
* af = ?
* of = התוצאה הייתה נכנסת גם לאוגר מאותו גודל של הפרמטר
* sf = ?
* pf = ?

## IDIV ##
חילוק בין מספרים מסומנים
```nasm
idiv devider
```
| code           | explain                                              |
|----------------|------------------------------------------------------|
| `idiv r8 /m8`  | source is ax, result is al and reminder is ah        |
| `idiv r16/m16` | source is dx:ax, result is ax and reminder is dx     |
| `idiv r32/m32` | source is edx:eax, result is eax and reminder is edx |

הפעולה:  
```nasm
temp = source;
result = temp/devider;
reminder = temp%devider;
```
אם התוצאה לא יכולה להיכנס לאן שהיא אמורה (התוצאה עצמה או השארית) התוכנית תקרוס  
אם המחלק והמחולק שונים (אחד חיובי והשני שלילי) התוצאה תהיה שלילית  
אם המחולק שלילי השארית תהיה שלילית  
דוגמה:
```math
5/3 = 1 (2)  
5/-3 = -1 (2)  
-5/3 = -1 (-2)  
-5/-3 = 1 (-2)
```

דגלים:  
כל הדגלים לא מוגדרים:
* zf = ?
* cf = ?
* af = ?
* of = ?
* sf = ?
* pf = ?

## SHL / SAL / SHR / SAR ##
מחלק או מכפיל ב2  
S(H) - Shift  
A - Aritmetic (sign)  
R - Right, L - left  
כלומר הזזה ימינה או שמאלה של הביטים
```nasm
shl/sal dest, number; dest = dest * cmath.pow(2, number)
shr/sar dest, number; dest = dest / cmath.pow(2, number) 
```

| code                                           | explain |
|------------------------------------------------|---------|
| `shl/sal/shr/sar r8/m8/r16/m16/r32/m32 cl/im8` |         |

הפעולה:
```c
// SHL/SAL
dest = dest << number;
// SHR
dest = dest >> number;
```
דגלים:   
במקרה של הזזה ב0:  
הדגלים לא משתנים ונשארים בדיוק כפי שהיו  

במקרה של הזזה ב1:  
* zf = האם התוצאה שקיבלנו היא 0
* cf = הביט שיצא החוצה
* af = ?
* of = האם המספר שינה סימן (היה שלילי והפך לחיובי או להפך)
* sf = האם התוצאה שלילית (אם נסתכל כמספר מסומן)
* pf = האם יש מספר זוגי של ביטים דלוקים בבית הימני ביותר של התוצאה

במקרה של הזזה ביותר מ1:
* zf = האם התוצאה שקיבלנו היא 0
* cf = הביט האחרון שיצא החוצה (אם הזזנו ביותר מכמות הביטים שקיימת אז לא מוגדר)
* af = ?
* of = ?
* sf = האם התוצאה שלילית (אם נסתכל כמספר מסומן)
* pf = האם יש מספר זוגי של ביטים דלוקים בבית הימני ביותר של התוצאה

## ROL / RCL / ROR / RCR ##
מסובב את הביטים ימינה או שמאלה עם לכלול את דגל הנשא בסבוב או בלי
R(O) - Rotate  
C - Carry
L - Left, R - right

```nasm
rol/rcl/ror/rcr dest, number 
```

| code                                           | explain |
|------------------------------------------------|---------|
| `rol/rcl/ror/rcr r8/m8/r16/m16/r32/m32 cl/im8` |         |

מסובב את הביטים כשאר כולל את דגל הנשא או לא 

דגלים:   
במקרה של הזזה ב0:  
הדגלים לא משתנים ונשארים בדיוק כפי שהיו  

במקרה של הזזה ב1:  
* zf = zf (לא משתנה)
* cf = הביט שיצא החוצה
* af = af (לא משתנה)
* of = האם המספר שינה סימן (היה שלילי והפך לחיובי או להפך)
* sf = sf (לא משתנה)
* pf = pf (לא משתנה)

במקרה של הזזה ביותר מ1:  
* zf = zf (לא משתנה)
* cf = הביט שיצא החוצה
* af = af (לא משתנה)
* of = ?
* sf = sf (לא משתנה)
* pf = pf (לא משתנה)

## LODSB /LODSW / LODSD ##
load string byte/word/dword  
שומר בal/ax/eax את הערך שיש במיקום בזיכרון בesi ומזיז את esi לתא הבא (בהתאם לגודל) התא הבא יכול להיות התא קדימה או אחורה לפי df
```nasm
lodsb/lodsw/lodsd
```
הפעולה:
```c
//lodsb
al = *esi;
if(df)
    esi = edi - 1;
else
    esi = edi + 1;

//lodsw
ax = *esi;
if(df)
    esi = esi - 2;
else
    esi = esi + 2;
    
//lodsd
eax = *esi;
if(df)
    esi = esi - 4;
else
    esi = esi + 4;
```
הדגלים אינם משתנים

## STOSB / STOSW / STOSD ##
store string byte/word/dword  
שם במיקום בזיכרון בedi את הערך שיש בal/ax/eax ומזיז את esi לתא הבא (בהתאם לגודל) התא הבא יכול להיות התא קדימה או אחורה לפי df
```nasm
stosb/stosw/stosd
```
הפעולה:
```c
//stosb
*edi = al;
if(df == 1)
    edi = edi - 1;
else
    edi = edi + 1;

//stosw
*edi = ax;
if(df == 1)
    edi = edi - 2;
else
    edi = edi + 2;
    
//stosd
*edi = eax;
if(df == 1)
    edi = edi - 4;
else
    edi = edi + 4;
```
הדגלים אינם משתנים

## MOVSB / MOVSW / MOVSD ##
move string byte/word/dword  
שומר במיקום בזיכרון בedi את הערך שיש במיקום בזיכרון בesi ומזיז את esi וedi לתא הבא (בהתאם לגודל) התא הבא יכול להיות התא קדימה או אחורה לפי df
```nasm
movsb/movsw/movsd
```
הפעולה:
```c
//movsb
*edi = *esi;
if(df == 1)
{
    esi = esi - 1;
    edi = edi - 1;
}
else
{
    esi = esi + 1;
    edi = edi + 1;
}

//movsw
*edi = *esi;
if(df == 1)
{
    esi = esi - 2;
    edi = edi - 2;
}
else
{
    esi = esi + 2;
    edi = edi + 2;
}
    
//movsd
*edi = *esi;
if(df == 1)
{
    esi = esi - 4;
    edi = edi - 4;
}
else
{
    esi = esi + 4;
    edi = edi + 4;
}
```
הדגלים אינם משתנים

## CMPSB / CMPSW / CMPSD ##
compare string byte/word/dword  
משווה (מחסר) בין במיקום בזיכרון בesi והערך שיש במיקום בזיכרון בedi ומזיז את esi וedi לתא הבא (בהתאם לגודל) התא הבא יכול להיות התא קדימה או אחורה לפי df
```nasm
movsb/movsw/movsd
```
הפעולה:
```c
//movsb
temp = *esi - *edi;
if(df == 1)
{
    esi = esi - 1;
    edi = edi - 1;
}
else
{
    esi = esi + 1;
    edi = edi + 1;
}

//movsw
temp = *esi - *edi;
if(df == 1)
{
    esi = esi - 2;
    edi = edi - 2;
}
else
{
    esi = esi + 2;
    edi = edi + 2;
}
    
//movsd
temp = *esi - *edi;
if(df == 1)
{
    esi = esi - 4;
    edi = edi - 4;
}
else
{
    esi = esi + 4;
    edi = edi + 4;
}
```
הדגלים משתנים בהתאם לפעולת החיסור  

דגלים:
* zf = האם התוצאה היא 0
* cf = האם הייתה טעות עבור מספרים לא מסומנים
* af = האם הייתה טעות חישוב אם היינו מסתכלים רק על הניבל השמאלי ביותר
* of = האם הייתה טעות במספרים מסומנים
* sf = האם התואה נחשבת שלילית (כמספר מסומן)
* pf = האם יש מספר זוגי של ביטים דלוקים בבית הימני ביותר של התוצאה

## SCASB / SCASW / SCASD ##
scan string byte/word/dword  
משווה (מחסר) בין al/ax/eax והערך שיש במיקום בזיכרון בedi ומזיז את edi לתא הבא (בהתאם לגודל) התא הבא יכול להיות התא קדימה או אחורה לפי df
```nasm
movsb/movsw/movsd
```
הפעולה:
```c
//movsb
temp = al - *edi;
if(df == 1)
{
    edi = edi - 1;
}
else
{
    edi = edi + 1;
}

//movsw
temp = ax - *edi;
if(df == 1)
{
    edi = edi - 2;
}
else
{
    edi = edi + 2;
}
    
//movsd
temp = eax - *edi;
if(df == 1)
{
    edi = edi - 4;
}
else
{
    edi = edi + 4;
}
```
הדגלים משתנים בהתאם לפעולת החיסור  

דגלים:
* zf = האם התוצאה היא 0
* cf = האם הייתה טעות עבור מספרים לא מסומנים
* af = האם הייתה טעות חישוב אם היינו מסתכלים רק על הניבל השמאלי ביותר
* of = האם הייתה טעות במספרים מסומנים
* sf = האם התואה נחשבת שלילית (כמספר מסומן)
* pf = האם יש מספר זוגי של ביטים דלוקים בבית הימני ביותר של התוצאה

## REP / (REPE / REPZ) / (REPNE / REPNZ) ##
אחרי פעולת הrep מגיעות אחת מפעולות הסטרינגים לדוגמה:  
```nasm
rep movsb
repe cmpsw
repne scasb
```
פעולת הrep מבצעת את הפעולה שיש בתוכה ecx פעמים  
פעולת הrepe\repz מבצעת את הפעולה שיש בתוכה ecx פעמים וכל עד דגל האפס המוחזר מהפעולה הוא 1
פעולת הrepne\repnz מבצעת את הפעולה שיש בתוכה ecx פעמים וכל עד דגל האפס המוחזר מהפעולה הוא 0

```c
// rep method
while(ecx > 0)
{
    ecx--;
    method();
}

// repe/repz method
while(ecx > 0)
{
    ecx--;
    method();
    if(zf != 1)
    {
        break;
    }
}

// repne/repnz method
while(ecx > 0)
{
    ecx--;
    method();
    if(zf == 1)
    {
        break;
    }
}
```

## PUSH / PUSHA / PUSHF ##
push (all) (flags) to the stack  
דוחף לתוך המחסנית מילה כפולה כלשהי או 8 עבור all

| code                | explain                        |
|---------------------|--------------------------------|
| `push r32/m32/im32` | push the data as dword         |
| `pusha`             | push all register (0x20 bytes) |
| `pushf`             | push the flags    (0x4 bytes)  |

## POP / POPA / POPF ##
pop (all) (flags) from the stack  
מושך מהמחסנית מילה כפולה כלשהיא או 8 עבור all

| code                | explain                        |
|---------------------|--------------------------------|
| `push r32/m32/im32` | push the data as dword         |
| `pusha`             | push all register (0x20 bytes) |
| `pushf`             | push the flags    (0x4 bytes)  |

## ENTER / LEAVE ##
בתחילת פונקציה נשתמש בenter שהיא תיתן לנו מקום במחסנית שניתן לפנות אליו לפי ebp
בסוף הפונקציה נשתמש בleave
```nasm
; enter x, 0
push ebp
mov ebp, esp
sub ebp, x

; leave
mov esp, ebp
pop ebp
```
