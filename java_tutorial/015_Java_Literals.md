# Java Literals

**Java Literals** | Understanding constant values, literal types, number systems, and Java 1.7 enhancements for literals.

- [Types of Literals in Java](#types-of-literals-in-java)
- [Integral Literals in Java](#integral-literals-in-java)
- [Floating-Point Literals in Java](#floating-point-literals-in-java)
- [Character Literals in Java](#character-literals-in-java)
- [Conditional Literals in Java](#conditional-literals-in-java)
- [String Literals in Java](#string-literals-in-java)
- [Null Literals in Java](#null-literals-in-java)
- [Integral Literals Based on Number System in Java](#integral-literals-based-on-number-system-in-java)
- [Other Points for Integral Literals in Java](#other-points-for-integral-literals-in-java)
- [Java 1.7 Enhancement in Literals](#java-17-enhancement-in-literals)

---

Any constant value in the program is called a literal. Literals in Java are used to represent value or assign variables value. Examples of literals: 9, 9.5, `'a'`, `"a"`, `true`, `false`, `null`, and e.t.c.

**Rules for using Literals in Java:**

- ❌️ The literal can't be used as a single statement.

```java
class Test {
    public static void main(args[] String) {
       true; // invalid
       9; // invalid
    }
}
```

- ❌️ We can not use a literal left side of the assignment operator.

```java
int a;
a = 10; // valid
20 = a; // invalid
```

- ✅ We can use literal only in the variable assignment, or in an expression, or as method argument.

---

## 1. Types of Literals in Java

Based on the different types of data we store in the program, Java supports 7 types of literals. These are:

1. 🔢 Integral literals
2. 🔟 Floating-point literals
3. 🔤 Character literals
4. ✅ Conditional literals
5. 📝 String literals
6. 🚫 Null Literals

Let us discuss each literal one by one.

---

## 2. Integral Literals in Java

The **compiler treats every integer number as an `int` data type**. If we use 10 in a program, compiler and JVM consider 10 as an `int` data type.

If we want to treat an integer number as `long` data type, then we must suffix `L` or `l` to this number, and if we want to treat an integer number as a `byte` or `short` data type than we must prefix the cast operator.

| Data Type 🔢 | Literals 📋 |
|-------------|------------|
| **byte** | `(byte)9`, `(byte)50` e.t.c. |
| **short** | `(short)10`, `(short)50` e.t.c. |
| **int** | `9`, `5`, `50`, `800` e.t.c. |
| **long** | `9L`, `10L`, `55L` e.t.c. |

> 📝 **Note:** There is no `byte` and `short` literals in Java. We need to convert the `int` data type to `byte` or `short` data type by using cast operator.

**Integral literals example:**

```java
class IntegerLiterals{
   public static void main(String[] args) {
     byte n1 = (byte)90;
     short n2 = (short)900;
     int n3 = 9000;
     long n4 = 9000000L;

     System.out.println(n1);
     System.out.println(n2);
     System.out.println(n3);
     System.out.println(n4);
   }
 }
```

📤 **Output:**

```
90
900
9000
9000000
```

---

## 3. Floating-Point Literals in Java

By default, the **compiler treats every floating-point number as `double`**. If we want to tell the compiler to treat a number as a `float` data type, then we must suffix it with `F` or `f`. We can use suffix `D` or `d` for `double` data type but it is optional.

- `50.0` is of the `double` data type.
- `50.0F` is of the `float` data type.
- `float f1 = 50.0;` // C.E: Possible loss of precision
- `float f2 = 50.0F;` // valid

| Data Type 🔢 | Literals 📋 |
|-------------|------------|
| **float** | `5.0F`, `9.0F`, `50.5F`, e.t.c |
| **double** | `5.0`, `50.5`, `95.2`, e.t.c |

**Floating-point literals example:**

```java
class FloatingLiterals{
   public static void main(String[] args) {
     double n1 = 90.0;
     double n2 = 900D;
     float n3 = 901F;
     //float n4 = 902.0; //error

     System.out.println(n1);
     System.out.println(n2);
     System.out.println(n3);
   }
 }
```

📤 **Output:**

```
90.0
900.0
901.0
```

We can specify floating-point literal also in exponent form (scientific form).

**Scientific notation example:**

```java
class FloatingPointLiteral {
     public static void main(String[] args) {
         double d1 = 1.2e3;
         float f1 = 1.2e3F;
         System.out.println(d1);
         System.out.println(f1);
     }
 }
```

📤 **Output:**

```
1200.0
1200.0
```

---

## 4. Character Literals in Java

When any single letter/digit/special character is placed inside a single quote (`''`) then the compiler treats it as a `char` data type. By default, every character is treated as a `char` data type.

| Type 🔤 | Literals 📋 |
|---------|------------|
| **char** | `'A'`, `'a'`, `'5'`, `'@'`, `'$'`, e.t.c |

- `'A'` is of a `char` data type.
- `'9'` is of a `char` data type.
- `'@'` is of a `char` data type.
- `'10'` is *not* of `char` data type, because only one character is allowed inside the single quote.
- `''` is *not* of `char` data type, because inside the single quote one digit is necessary but it is empty.
- `' '` is of `char` data type, one blank space is inside a single quote.
- `x` is *not* a character, because it is not inside the single quote. It is an alphabet considered as a variable.

**Character literals example:**

```java
class CharacterLiterals1{
   public static void main(String[] args) {
     char ch1 = 'a';
     char ch2 = '9';
     char ch3 = ' ';
     char ch4 = '@';

     System.out.println(ch1);
     System.out.println(ch2);
     System.out.println(ch3);
     System.out.println(ch4);
   }
 }
```

📤 **Output:**

```
a
9

@
```

---

## 5. Conditional Literals in Java

In Java, we have a special data type called `boolean` to represent conditional values `true` and `false`. The `true` and `false` are the only allowed values for boolean data types. Unlike C, in Java we can not use 0 as false and 1 as true. Java compiler will throw an error if we use them, we must use `false` for false value and `true` for true value.

```java
boolean b1 = true; // valid
boolean b2 = false; // valid

boolean b3 = 0; // error
boolean b4 = 1; // error

if(true) { /* code */ } // valid
if(false) { /* code */ } // valid

if(0) { /* code */ } // error
if(1) { /* code */ } // error
```

| Type ✅ | Literals 📋 |
|--------|------------|
| **boolean** | `true`, `false` |

**Boolean literals example:**

```java
class BooleanLiterals{
   public static void main(String[] args) {
     boolean b1 = true;
     boolean b2 = false;

     /* error, Case sensitive
     boolean b3 = True; // error
     boolean b4 = False; // error
     */

     System.out.println(b1);
     System.out.println(b2);
   }
 }
```

📤 **Output:**

```
true
false
```

---

## 6. String Literals in Java

If we want to tell the compiler to treat some value as `String` type, we must place that value inside a double quote (`" "`). So, Any zero or multiple characters placed inside double quotes (`" "`) treated as a string.

In Java, every string is treated as `java.lang.String` type. The string is a referenced type and it is a class type.

- `"a"` is of string type.
- `"a51@"` is of string type.
- `""` is of string type.
- `" "` is of string type.
- `"Hi"` is of string type.
- `Hi` is not of string type because it is not inside the double quote, it will be considered as a variable.

**String literals example:**

```java
class StringLiterals{
   public static void main(String[] args) {
     String s1 = "a";
     String s2 = "KnowProgram";

     System.out.println(s1);
     System.out.println(s2);
   }
 }
```

📤 **Output:**

```
a
KnowProgram
```

---

## 7. Null Literals in Java

The literal `null` is of the referenced type, so it does not have any specific type. It may be of array / class / interface / enum / annotation type. It means we can store that literal `null` in any type of referenced variables.

```java
null; // type can not say
String s = null; // String type
Student s = null; // Student type
int[] ia = null; // int array type
Employee[] ie = null; // Employee array type
```

---

## 8. Integral Literals Based on Number System in Java

As per the number system, we have categorized integer literals into four types:

1. 🔢 Binary literals
2. 8️⃣ Octal literals
3. 🔟 Decimal literals
4. 🔠 Hexadecimal literals

| Type 🔢 | Base/Radix 📏 | Allowed Characters 🔤 | Can Start With 🏷️ |
|---------|-------------|---------------------|-------------------|
| **Decimal** | 10 | 0 to 9 | All except 0 |
| **Octal** | 8 | 0 to 7 | Always with 0 |
| **Hexadecimal** | 16 | 0 to 9, a-f, A-F | `0X` or `0x` |
| **Binary** | 2 | 0, 1 | `0B` or `0b` |

---

### Decimal Integral Literals

We can use decimal number for `int`, `long`, `float` and `double` data types. Example of decimal literals are: 123, 150L, 50F, 10.0

```java
class DecimalLiterals{
     public static void main(String[] args) {
       int n1 = 70;
       long n2 = 80L;
       float n3 = 90F;
       double n4 = 100;

       System.out.println(n1);
       System.out.println(n2);
       System.out.println(n3);
       System.out.println(n4);
     }
 }
```

📤 **Output:**

```
70
80
90.0
100.0
```

---

### Binary Integral Literals

We can use binary literals only for integer data types. If we try to use the binary literals *for floating data types* by using the suffix `F`, `D` or `.0` then the *compiler* will *throw an error*. Example of binary literals are: `0B1001`, `0b100` e.t.c. The binary literals always start with `0B` or `0b`, and the allowed digits are 0 and 1.

```java
class BinaryLiterals{
     public static void main(String[] args) {
       int n1 = 0B1010;
       long n2 = 0B1110L;
       //float n3 = 0B1111F; //error
       //double n4 = 0B1111D; //error

       System.out.println(n1);
       System.out.println(n2);
     }
 }
```

📤 **Output:**

```
10
14
```

---

### Hexadecimal Integral Literals

We can also represent Hexadecimal number as only for `int` and `long` data types. If we try to represent `float` or `double` with suffix `.0` or `.0F` or `.0D` then the compiler will throw an error. But we don't get a compile-time error if we suffix `F` or `D`. Because `F` and `D` are in the hexadecimal number range and their decimal values are 15 and 13 respectively. So, `F` and `D` do not act as a suffix character.

The hexadecimal integral literals always start with `0X` or `0x`, and the allowed characters are 0 to 9, a to f, A to F.

```java
class HexadecimalLiterals{
     public static void main(String[] args) {
       int n1 = 0xA1;
       long n2 = 0xA2L;
       float n3 = 0xA1F;
       double n4 = 0xA1D;
       /*
       float n5 = 0xA1.0F; //error
       double n6 = 0xA1.0D; //error
       float n7 = 0xA1.F; //error
       double n8 = 0xA1.D;//error
       */

       System.out.println(n1);
       System.out.println(n2);
       System.out.println(n3);
       System.out.println(n4);
     }
 }
```

📤 **Output:**

```
161
162
2591.0
2589.0
```

> 📝 **Note:** Java is case sensitive but in a few places, it doesn't show the case sensitivity. The suffix for the hexadecimal number is one of those places. Here you can use `a` to `f` or `A` to `F`, both lowercase and uppercase characters are valid. This is one of the very few areas where Java is not case sensitive.

---

### Octal Integral Literals

Octal literal can be represented as `int` and `long` data type. We can't use octal literal to represent floating point number.

Note that we can suffix `F`, `D`, and `0.0` to the octal literal, and in this case we don't get the compile-time error but here twist is the octal literal will not be converted into decimal. The octal literal, as it is used as a floating-point number. Example: `0123F` will be converted to `123.0`

```java
class OctalLiterals{
     public static void main(String[] args) {
       int n1 = 0123;
       long n2 = 0567L;
       float n3 = 0124F;
       double n4 = 0125D;
       float n5 = 056789F;
       double n6 = 056789D;

       System.out.println(n1);
       System.out.println(n2);
       System.out.println(n3);
       System.out.println(n4);
       System.out.println(n5);
       System.out.println(n6);
     }
 }
```

📤 **Output:**

```
83
375
124.0
125.0
56789.0
56789.0
```

If we suffix `F`, `D`, `.0` to an octal number, it is not considered as an octal number rather it is considered as a floating-point number. Hence with suffix character `F`, `D`, and `.0` in an octal number we can use the digits 8 or 9 also. For example: `012389D`, `012389F` and `012389.0` are converted to `12389.0`

If we are working with suffix character `L` (for `long`), then we can't use 8 and 9 in an octal number. The compiler will throw an error because it is considered as octal numbers and 8, 9 are not in the range of octal number (0 to 7).

```java
long n2 = 0567L;   //valid
long n3 = 05678L;  //error
long n3 = 056789L; //error
```

**Summary of literal representation:**

| Integral Literal 🔢 | Can Represent Integer? ✅ | Can Represent Floating-Point? 🔟 |
|---------------------|------------------------|-------------------------------|
| **Binary** | ✅ Yes | ❌️ No |
| **Octal** | ✅ Yes | ❌️ No |
| **Decimal** | ✅ Yes | ✅ Yes |
| **Hexadecimal** | ✅ Yes | ✅ Yes (conditions applied) |

---

## 9. Other Points for Integral Literals in Java

Literal assigned to a variable must be in the range of variable's data type otherwise we will get a compile-time error.

```java
class Program{
     public static void main(String[] args) {
       byte n1 = 0xA;
       //byte n2 = 0xA1; //incompatible types

       short n3 = 0xA9;
       int n4 = 0xA9;
       long n5 = 0xA9;
       char ch = 0xA9;

       //boolean b1 = 0xA9; //incompatible types
       //String str = 0xA9; //incompatible types

       System.out.println(n1);
       System.out.println(n3);
       System.out.println(n4);
       System.out.println(n5);
       System.out.println(ch);
     }
 }
```

📤 **Output:**

```
10
169
169
169
©
```

The value of `0xA` in decimal is 10 and it comes under byte-range so, no error occurs for the 3rd line of the program. But the value of `0xA1` is 161 and it is not in the range of `byte` data type so, in the next line, it gives an error.

Similarly, the value of `0xA9` is 169 so, it can be stored in `short`, `int`, `long`, and `char` data types but not in the `boolean` and `String` data types because 169 is integer number and it can't be converted to `boolean` and `String` data types.

---

### Binary, Octal, and Hexadecimal Number Conversions

When we use binary, octal, and hexadecimal numbers in a program, the **compiler will always convert all these three literals to the decimal number system**. After that decimal number used in the program for calculation and for displaying. The programmer having the choice to specify the integer value in binary, octal, decimal, and hexadecimal number system, but JVM always perform operations with decimal number system.

```java
class Program{
     public static void main(String[] args) {
       //binary
       System.out.println(0B1001);
       System.out.println(0B1111);

       //octal
       System.out.println(0153);
       System.out.println(0011);

       //decimal
       System.out.println(10);
       System.out.println(1100);

       //hexadecimal
       System.out.println(0x123);
       System.out.println(0xA05B);
     }
 }
```

📤 **Output:**

```
9
15
107
9
10
1100
291
41051
```

🧮 **Conversion from binary to decimal:**
`0B1001` can be written as `1001`
= (1\*2^3) + (0\*2^2) + (0\*2^1) + (1\*2^0)
= 8 + 0 + 0 + 1
= 9

🧮 **Conversion from octal to decimal:**
`0153` can be written as `153`
= (1\*8^2) + (5\*8^1) + (3\*8^0)
= 64 + 40 + 3
= 107

🧮 **Conversion from hexadecimal to decimal:**
`0x123` can be written as `123`
= (1\*16^2) + (2\*16^1) + (3\*16^0)
= 256 + 32 + 3
= 291

---

## 10. Java 1.7 Enhancement in Literals

In Java 1.7 version two new features were added in literals:

1. 🆕 Binary literal
2. 🔗 Underscore in number literals

### Binary Literals

Up to Java 1.6 version, Java supports only octal, decimal, and hexadecimal literals. From Java 7 onwards Java supports binary literals with below two rules:

- The binary number should start with `0B` or `0b`.
- It should contain digits 0, 1 only.

We had already discussed binary literals.

```java
class Program{
     public static void main(String[] args) {
       int n1 = 1010; //decimal
       int n2 = 0B1010; //binary
       System.out.println(n1);
       System.out.println(n2);
     }
 }
```

📤 **Output:**

```
101
10
```

---

### Underscore in Numeric Literals

In our real-life for separating digits in number we use comma (`,`) but in Java, we are not allowed to use the comma. The comma (`,`) was already used in Java for separating parameters. As a replacement for comma, we can use `_`. From Java 1.7 onwards we are allowed to place `_` in a number in between digits. This feature makes a number easily understandable and readable.

```java
class Program{
     public static void main(String[] args) {
       double d1 = 100000;
       //double d2 = 1,00,000; // error
       double d3 = 1_00_000;
       double d4 = 1_000_00;

       System.out.println(d1);
       System.out.println(d3);
       System.out.println(d4);
     }
 }
```

📤 **Output:**

```
100000.0
100000.0
100000.0
```

When we write a number with an underscore (`_`), then underscore won't be displayed, only the number will be displayed. Underscore is used for communication between programmers, for better understanding. Underscore is only present in the source file. It is not for end-user and JVM. In byte code, this underscore is not present. At the time of compilation, these underscore symbols will be removed automatically.

### Rules for Underscore in Number Literals

If we are working with an underscore in number literals then we should follow some rules. You don't need to remember these rules, just look and observe them once. When you are using an underscore in program then remember only one thing that Underscore is used for communication, for better understanding between programmers.

1️⃣ **Underscore must be in between digits.** We should not use it at the begin or end of the number.

```java
double d1 = 1_00_000;
double d2 = _1_00_00; //error: cannot find symbol
double d3 = _10000; //error: cannot find symbol
double d4 = 1_00_000_; //error: illegal underscore
```

2️⃣ **We can use multiple underscore in between a number.**

```java
double d1 = 1_000;
double d2 = 1_00_000;
double d2 = 1__00___000;
```

```java
class Program{
     public static void main(String[] args) {
       double d1 = 1_00_000;
       double d2 = 1_0_0_0_0_0;
       double d3 = 1_____00___00__0_0;

       System.out.println(d1);
       System.out.println(d2);
       System.out.println(d3);
     }
 }
```

📤 **Output:**

```
100000.0
100000.0
1000000.0
```

3️⃣ **Underscore is not allowed immediately before and after the dot (`.`) symbol in floating point number.**

```java
double d1 = 1_00_000.89;
double d2 = 1_00_000.8_9;
double d3 = 1_00_000._89; // error
double d4 = 1_00_000_.89; // error
double d5 = 1_00_000_._89; // error
float f1 = 1_00_000_.89; // error
```

4️⃣ **Underscore is not allowed immediately before or after suffix characters L, F, and D.**

```java
 double d1 = 1_00_000L;
 double d2 = 1_00_000_L; // error
 double d3 = 1_00_000L_; // error
 double d4 = 100000_L; // error
 double d5 = 1_00_000_F; // error
 double d6 = 100_000D_; // error
```

5️⃣ **Underscore is not allowed immediately before, after and in between the prefix characters `0X`, `0x`, `0B`, and `0b`.** But for octal literal underscore can be used only after 0.

```java
// hexadecimal
int n1 = _0xA123; // error
int n2 = 0_xA123; // error
int n3 = 0x_A123; // error
int n4 = 0xA_123;
int n5 = 0xA_12_3;
```

```java
// binary
int n6 = _0B1010; // error
int n7 = 0_B1010; // error
int n8 = 0B_1010; // error
int n9 = 0B10_10;
```

**Octal with underscore:**

```java
class Program{
     public static void main(String[] args) {
       //int n1 = _015; //error
       //int n2 = _0123; //error

       int n3 = 0_123;
       int n4 = 0_15;
       int n5 = 01_5;
       int n6 = 0_1_00_00;

       System.out.println(n3);
       System.out.println(n4);
       System.out.println(n5);
       System.out.println(n6);
     }
 }
```

📤 **Output:**

```
83
13
13
4096
```

> 📝 **Note:** We can use underscore in octal literal after zero, but not before zero.
