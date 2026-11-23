# Arithmetic Operators in Java

**Arithmetic Operators in Java** | Understanding addition, subtraction, multiplication, division, and modulus operators with string concatenation behavior.

- [Different Behaviours of Arithmetic Addition Operators in Java](#different-behaviours-of-arithmetic-addition-operators-in-java)
- [Java Division Operator](#java-division-operator)
- [Arithmetic Operators Modulus in Java](#arithmetic-operators-modulus-in-java)
- [Important Points on Arithmetic Operators in Java](#important-points-on-arithmetic-operators-in-java)
- [ArithmeticException](#arithmeticexception)

---

Arithmetic operators in Java are used to perform mathematical operations. The arithmetic operators in Java can operate on any built-in data type.

Syntax: `operand1 operator operand2`

| Operator ➕ | Meaning 📋 |
|------------|-----------|
| **`+`** | Addition |
| **`-`** | Subtraction |
| **`*`** | Multiplication |
| **`/`** | Division |
| **`%`** | Modulus |

**Basic arithmetic operations:**

```java
class ArithmeticOperator1{
   public static void main(String[] args) {
     System.out.println(50+20);
     System.out.println(50-20);
     System.out.println(50*20);
     System.out.println(50/20);
     System.out.println(50%20);
   }
 }
```

The unary minus operator has the effect of multiplying its operand by -1. Example: `8*(-1) = (-8)`

**Unary minus example:**

```java
class Substraction{
   public static void main(String[] args) {
     int a=5;
     System.out.println("a: "+ a);
     System.out.println("-a: "+ -a);
     System.out.println("- -a: "+ - -a);
   }
 }
```

📤 **Output:**

```
a: 5
-a: -5
- -a: 5
```

---

## 1. Different Behaviours of Arithmetic Addition Operators in Java

Java doesn't support operator overloading, but the `+` operator is the exception case. The only overloaded operator in Java is `+` only.

In Java, `+` operator acts as:

- ➕ Arithmetic addition operator
- 🔗 String concatenation operator

**When does `+` operator act as an arithmetic addition operator and when it acts as a string concatenation operator?**

If both operands of `+` operators are numbers or characters, then it acts as an arithmetic addition operator. But, at least one of the operand is a string, then it acts as a string concatenation operator.

```java
class Addition1{
   public static void main(String[] args) {

     //Addition operator
     System.out.println(9+10);
     System.out.println(3+'a');
     System.out.println('a'+'b');

     //String concatenation operator
     System.out.println("a"+"b");
     System.out.println("a"+9);
   }
 }
```

📤 **Output:**

```
19
100
195
ab
a9
```

In the first, second and third `println()` lines it acts as an addition operator because both operands are numbers or characters. In fourth and fifth lines `+` operator acts as string concatenation operator, in these case at least one operand is a string.

### The String Concatenation Operator (+)

In Concatenation, the compiler evaluates the given expression from left to right given that the operators have the same precedence and **once it encounters the string then it considers the rest of the expression as of a string** (again based on the precedence order of the expression).

```java
class Addition2{
   public static void main(String[] args) {

     System.out.println(1+2+3+4+"abcd");
     System.out.println("abcd"+1+2+3+4);

     System.out.println(1+2+3+4+"abcd"+5+6+7+8);
     System.out.println(1+2+3+4+"abcd"+(5+6+7+8));

     System.out.println(5+6+7+8+"abcd"+(1/2*3-4));
   }
 }
```

📤 **Output:**

```
10abcd
abcd1234
10abcd5678
10abcd26
26abcd-4
```

🧠 **In Simple Words:**

- In the first line, `1+2+3+4` gives 10. So, 10 and `abcd` concatenated and displayed `10abcd` on the screen.
- In the second line, the first string came so remaining expression acts as a string. Hence it gives results `abcd1234`.
- In the third line, `1+2+3+4` gives 10, then string `abcd` came so remaining expression also acts as a string and displayed `10abcd5678`.
- In the fourth line, `1+2+3+4` gives 10 then string `abcd` and `(5+6+7+8)` came. `(5+6+7+8)` gives 26 so this line displayed `10abcd26`.
- Similarly, the last line `(1/2*3-4)` gives -4 because expression evaluated from left to right, `*` and `/` have the same precedence.

> 💡 **Tip:** When using `+` operator inside `System.out.println()` make sure to use the parenthesis for arithmetic operation.

**Concatenation evaluation example:**

```java
 class Addition3{
   public static void main(String[] args) {
     int x=9;
     int y=10;
     int z=x*y;
     System.out.println(z);
     System.out.println("The multiplication of "+x+" and "+y+" is "+z);
   }
 }
```

📤 **Output:**

```
90
The multiplication of 9 and 10 is 90
```

**The evaluation process of the above statement:**

```java
("The multiplication of "+x+" and "+y+" is "+z);
("The multiplication of "+9+" and "+10+" is "+90);
("The multiplication of "+"9"+" and "+10+" is "+90);
("The multiplication of 9"+" and "+10+" is "+90);
("The multiplication of 9 and "+10+" is "+90);
("The multiplication of 9 and "+"10"+" is "+90);
("The multiplication of 9 and 10"+" is "+90);
("The multiplication of 9 and 10 is "+90);
("The multiplication of 9 and 10 is "+"90");
("The multiplication of 9 and 10 is 90");
```

---

### Exercise on String Concatenation Operator in Java

Find out the output of the below programs? The programs are based on arithmetic operators in Java.

**Program1:**

```java
class Addition4{
   public static void main(String[] args) {
     System.out.println(10+20);
     System.out.println(10+'a');
     System.out.println('a'+'b');
     System.out.println("a"+"b");
     System.out.println("a"+10);
     System.out.println("a"+true);
     System.out.println("a"+null);
   }
 }
```

📤 **Output:**

```
30
107
195
ab
a10
atrue
anull
```

**Program2:**

```java
class Addition5{
   public static void main(String[] args) {
     System.out.println(""+10+20);
     System.out.println(10+""+20);
     System.out.println(10+20+"");
     System.out.println(""+(10+20));
   }
 }
```

📤 **Output:**

```
1020
1020
30
30
```

**Program3:**

```java
class Addition6{
   public static void main(String[] args) {
     int a=10;
     int b=20;
     System.out.println(a+b);
     System.out.println("a+b");

     System.out.println("a+b:"+a+b);
     System.out.println("a+b:"+(a+b));
     System.out.println();

     //System.out.println("a-b:"+a-b);
     //error: bad operand types for binary operator '-'

     System.out.println("a-b:"+(a-b));
     System.out.println();
     System.out.println("a*b:"+a*b);
   }
 }
```

📤 **Output:**

```
30
a+b
a+b: 1020
a+b: 30

a-b: -10

a*b: 200
```

---

## 2. Java Division Operator

20 / 2 = 10
Here, 20 is called dividend, 2 is called the divisor, 10 is called the quotient.

1️⃣ **The division operator (`/`) produces the quotient.**

```java
class DivisionOperator1{
   public static void main(String[] args) {
     System.out.println(1/2);
     System.out.println(1F/2);
     System.out.println(1D/2);
     System.out.println(11/4);
     System.out.println(11F/4);
     System.out.println(11D/4);
   }
 }
```

📤 **Output:**

```
0
0.5
0.5
2
2.75
2.75
```

```java
class DivisionOperator2{
   public static void main(String[] args) {
     System.out.println(22/7*10*10);
     System.out.println(22F/7*10*10);
     System.out.println(22D/7*10*10);
   }
 }
```

📤 **Output:**

```
300
314.2857
314.2857142857143
```

2️⃣ **If exactly any one of the operand is negative then the result is negative.** If both operands are -ve/+ve then the result is positive.

```java
class DivisionOperator3{
   public static void main(String[] args) {
     System.out.println(9/5);
     System.out.println(9/-5);
     System.out.println(-9/5);
     System.out.println(-9/-5);
   }
 }
```

📤 **Output:**

```
1
-1
-1
1
```

3️⃣ **When any integer number is divided by ten** then it **removes the last digit** of the number. Later we will write many Java basic programs using this concept.

```java
class DivisionOperator4{
   public static void main(String[] args) {
     System.out.println(123/10);
     System.out.println(12300/10);
     System.out.println(123015/10);
   }
 }
```

📤 **Output:**

```
12
1230
12301
```

```java
class DivisionOperator5{
   public static void main(String[] args) {
     System.out.println(12.3/10);
     System.out.println(1230.0/10);
     System.out.println(123.015/10);
   }
 }
```

📤 **Output:**

```
1.23
123.0
12.3015
```

---

### Different Cases When the Divisor is Zero

> 📝 **Note:** In these cases dividend should not be zero.

| Operation ➗ | Result 📋 |
|-------------|----------|
| **Integer / 0** | 🚨 Runtime error |
| **Integer / 0.0** | Infinity |
| **Floating-point / 0** | Infinity |
| **Floating-point / 0.0** | Infinity |

We can't divide an integer number by integer zero, it leads to runtime error: `java.lang.ArithmeticException`.

```java
class DivisionOperator6{
   public static void main(String[] args) {
     System.out.println(10/0);
   }
 }
```

```
Exception in thread "main" java.lang.ArithmeticException: / by zero
	at Division1.main(A.java:3)
```

We can divide an integer number by floating-point zero. Its output is infinity.

```java
class DivisionOperator7 {
     public static void main(String[] args) {
         System.out.println(10/0.0);
         System.out.println(10/-0.0);
     }
 }
```

📤 **Output:**

```
Infinity
-Infinity
```

We can divide a floating-point number by ZERO (both integer and floating-point), its output is infinity.

```java
 class DivisionOperator8 {
   public static void main(String[] args) {
     System.out.println(10.0/0);
     System.out.println(10.0F/0);
     System.out.println(-10.0/0);
   }
 }
```

📤 **Output:**

```
Infinity
Infinity
-Infinity
```

```java
class DivisionOperator9 {
   public static void main(String[] args) {
     System.out.println(10.0/0.0);
     System.out.println(10.0F/0.0);
     System.out.println(-10.0/0.0);
   }
 }
```

📤 **Output:**

```
Infinity
Infinity
-Infinity
```

**Why integer/0 gives an exception but in other cases the result is infinity?**

From basic mathematics, we know that any number divided by zero is infinity. In the case of integral arithmetic (`byte`, `short`, `int`, `long`), there is no way to represent infinity. Hence, the integer number divided by zero gives runtime `error: java.lang.ArithmeticException`

When it comes to floating-point arithmetic (`float` and `double`) there it is represented as "Infinity". Hence in getting results as Infinity or -Infinity.

```bash
> javap java.lang.Double
```

By using this command you can observe that there are two constants (`final` variable) `POSITIVE_INFINITY` and `NEGATIVE_INFINITY` are defined in `Double` class. These two constants are also defined in the `Float` class.

```bash
> javap java.lang.Integer
```

But those constants are not defined in `Byte`, `Short`, `Integer`, and `Long` classes.

---

### Different Cases When Both Dividend and Divisor are Zero

| Operation ➗ | Result 📋 |
|-------------|----------|
| **0 / 0** | 🚨 `java.lang.ArithmeticException` |
| **0 / 0.0** | `NaN` |
| **0.0 / 0** | `NaN` |
| **0.0 / 0.0** | `NaN` |

We can't divide an integer zero by an integer zero. It also leads to runtime `error: java.lang.ArithmeticException`

```java
class DivisionOperator10{
   public static void main(String[] args) {
     System.out.println(0/0);
   }
 }
```

```
Exception in thread "main" java.lang.ArithmeticException: / by zero
	at Division2.main(A.java:3)
```

In the remaining cases the output is `NaN`. "NaN" stands for "not a number". If integer number is divided by floating-point zero then we get the result as "not a number".

```java
class DivisionOperator11 {
     public static void main(String[] args) {
         System.out.println(0/0.0);
         System.out.println(0/-0.0);
     }
 }
```

📤 **Output:**

```
NaN
NaN
```

We can divide a floating-point ZERO by ZERO its output is `NaN`.

```java
class DivisionOperator10{
   public static void main(String[] args) {
     System.out.println(0.0/0);
     System.out.println(-0.0/0);
     System.out.println(0.0/0);
     System.out.println(0.0/0);
   }
 }
```

📤 **Output:**

```
NaN
NaN
NaN
NaN
```

```java
class DivisionOperator10{
   public static void main(String[] args) {
     System.out.println(0.0/0.0);
     System.out.println(-0.0/0.0);
     System.out.println(0.0/0.0);
     System.out.println(0.0/0.0);
   }
 }
```

📤 **Output:**

```
NaN
NaN
NaN
NaN
```

**Why does operation 0/0 give an exception but in all other cases we get the result NaN?**

In regular mathematics ZERO (integral or floating-point) divided by ZERO (integral or floating-point) gives an undefined result. In integral arithmetic (`byte`, `short`, `int`, and `long`) there is no way to represent the undefined result. Hence, 0/0 gives an exception.

But in the case of floating-point arithmetic, to represent undefined result `Float` and `Double` class contain `NaN` constant. Hence, in this case, the result is `NaN`.

By using `javap` tool you can verify that `Float` and `Double` class contain `NaN` constant, but `Byte`, `Short`, `Integer`, and `Long` classes don't contain `NaN` constant.

```bash
> javap java.lang.Double
> javap java.lang.Integer
```

---

## 3. Arithmetic Operators Modulus in Java

The remainder operator or modulus operator (`%`) produces the remainder after integer division i.e. `x%y = x - (x/y)*y`.

1️⃣ **On using the modulus operator (`%`) the sign of the remainder is always the same as the sign of the numerator.**

```java
class Modulus1{
   public static void main(String[] args) {
     System.out.println(9%5);
     System.out.println(-9%5);
     System.out.println(9%-5);
     System.out.println(-9%-5);
   }
 }
```

📤 **Output:**

```
4
-4
4
-4
```

2️⃣ **The modulus operator (`%`) also operates on floats and doubles.** (In C language modulus operator (`%`) does not operate on the Floating point number, to find remainder on a floating-point number we need `fmod()` function).

```java
class Modulus2{
   public static void main(String[] args) {
     System.out.println(9.0%5);
     System.out.println(9F%5);
     System.out.println(9%5F);
     System.out.println(9D%5D);
     System.out.println(9D%5F);
   }
 }
```

📤 **Output:**

```
4.0
4.0
4.0
4.0
4.0
```

3️⃣ **The divisor should be a non-zero value.** If the dividend is an integer then it leads to runtime error: `java.lang.ArithmeticException`, but if the dividend is a floating-point number then it gives result `NaN` (Not a Number).

```java
class Modulus3{
   public static void main(String[] args) {
     System.out.println(9%0);
   }
 }
```

```
Exception in thread "main" java.lang.ArithmeticException: / by zero
	at Modulus1.main(A.java:3)
```

```java
 class Modulus4{
   public static void main(String[] args) {
         System.out.println(9.5%0);
   }
 }
```

📤 **Output:**

```
NaN
```

4️⃣ **Any integer number %10 (not a floating-point number) gives the last digit of the number.** In Java, whenever you need to find a digit of the integer number then use the `%` operator.

```java
class Modulus5{
   public static void main(String[] args) {
     System.out.println(123%10);
     System.out.println(97%10);
   }
 }
```

📤 **Output:**

```
3
7
```

```java
class Modulus6{
   public static void main(String[] args) {
     System.out.println(123.23%10);
     System.out.println(97.59784%10);
     System.out.println(123.5%10);
     System.out.println(9F%10);
     System.out.println(9D%5D);
   }
 }
```

📤 **Output:**

```
3.230000000000004
7.597840000000005
3.5
9.0
4.0
```

---

## 4. Important Points on Arithmetic Operators in Java

Only `+` operator operates on a [string data type](018_String_Data_Type_in_Java.md). If we use any other arithmetic operators except `+` then we get a compile-time error.

```java
class ArithmeticOperator2{
   public static void main(String[] args) {
     String s1 = "a";
     String s2 = "b";
     String s3 = s1 + s2;
     System.out.println(s3);
     /*
     //error: bad operand types for binary operator
     String s4 = s1 - s2;
     String s5 = s1 * s2;
     String s6 = s1 / s2;
     String s7 = s1 % s2;
     */
   }
 }
```

📤 **Output:**

```
ab
```

> ⚠️ **Caution:** We can't use any arithmetic operators on the `boolean` data type.

```java
class ArithmeticOperator3{
   public static void main(String[] args) {
     /*
     //error: bad operand types for binary operator
     boolean bo1 = true;
     boolean bo2 = false;
     boolean bo3 = bo1 + bo2;
     boolean bo4 = bo1 - bo2;
     boolean bo5 = bo1 * bo2;
     boolean bo6 = bo1 / bo2;
     boolean bo7 = bo1 % bo2;
     */
   }
 }
```

---

## 5. ArithmeticException

While using arithmetic operators many times we get `ArithmeticException`. So, we should have knowledge that what is it, and when it occurs.

- 🚨 `ArithmeticException` is a **runtime exception**. It means `ArithmeticException` will never occur during compilation time.
- 🔢 It occurs only for Integral arithmetic (`byte`, `short`, `int`, `long`), but not for Floating-point arithmetic (`float` and `double`).
- ➗ The division (`/`) and modulus (`%`) are only arithmetic operators which can cause `ArithmeticException`. The remaining other arithmetic operators will not give `ArithmeticException`.
