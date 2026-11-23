# Java Math Class with Examples

**Java Math Class with Examples** | The `Math` class in Java is available in the `java.lang` package. It contains several methods for performing basic numeric operations such as exponential, logarithm, square root, and trigonometric functions.

- [Java Math Class Methods](#java-math-class-methods)
- [Methods with multiple overloaded forms](#methods-with-multiple-overloaded-forms)

By default, many of the Math methods simply call the equivalent method in `StrictMath` class for their implementation. Code generators are encouraged to **use platform-specific native libraries or microprocessor instructions, where available, to provide higher-performance implementations of Math class methods.**

> 📝 **Note:** We can't create objects of the Java Math class. All members are `static`.

Math class contains two `public static final` variables:

| Variable 🏷️ | Value 🔢 |
|---------|-------|
| **`PI`** | 3.14159265358979323846 |
| **`E`** | 2.7182818284590452354 |

**Accessing Math constants:**

```java
public class Test {
   public static void main(String[] args) {
       System.out.println(Math.PI);
       System.out.println(Math.E);
   }
}
```

📤 **Output:**

```
3.141592653589793
2.718281828459045
```

> 💡 **Tip:** Instead of calling static members of the Math class through its class name, we can use a [static import statement](024_Static_Import_in_Java.md). Learn more: [import math class in Java](077_Import_Math_Class_in_Java.md).

---

## 1. Java Math Class Methods

| Return type 📋 | Method 🛠️ | Description 📖 |
|------------|--------|-------------|
| `double` | **pow**(double a, double b) | Returns a^b |
| `double` | **exp**(double x) | Returns e^x, where e is Euler's number |
| `double` | **expm1**(double x) | Returns e^x - 1 |
| `double` | **log**(double x) | Returns the natural logarithm base e of x |
| `double` | **log10**(double x) | Returns the base 10 logarithm of x |
| `double` | **log1p**(double x) | Returns the natural logarithm of x+1 |
| `double` | **sqrt**(double x) | Returns square root value of x |
| `double` | **cbrt**(double x) | Returns the cube root value of x |
| `double` | **ceil**(double x) | Returns the smallest double value >= x equal to a mathematical integer |
| `double` | **floor**(double x) | Returns the largest double value <= x equal to a mathematical integer |
| `double` | **rint**(double x) | Returns the double value closest to x equal to a mathematical integer |
| `int` | **round**(float a) | Returns the closest int to x, ties rounding to positive infinity |
| `long` | **round**(double a) | Similar to previous, argument and return type changed |
| `double` | **random**() | Returns a double value >= 0.0 and < 1.0 |

**Power, exponential, log, and root examples:**

```java
public class Test {
   public static void main(String[] args) {
      System.out.println(Math.pow(2, 3));

      System.out.println(Math.exp(1));
      System.out.println(Math.expm1(1));

      System.out.println(Math.log(11));
      System.out.println(Math.log10(10));
      System.out.println(Math.log1p(10));

      System.out.println(Math.sqrt(64));
      System.out.println(Math.cbrt(64));
   }
}
```

📤 **Output:**

```
8.0
2.718281828459045
1.718281828459045
2.3978952727983707
1.0
2.3978952727983707
8.0
4.0
```

**Rounding method examples:**

```java
public class Test {
   public static void main(String[] args) {
      System.out.println(Math.ceil(5.5));
      System.out.println(Math.floor(5.5));
      System.out.println(Math.rint(5.5));
      System.out.println(Math.round(5.5));
   }
}
```

📤 **Output:**

```
6.0
5.0
6.0
6
```

**Differences between ceil(), floor(), rint(), and round() methods:**

| x 🔢 | ceil(x) ⬆️ | floor(x) ⬇️ | rint(x) 🔄 | round(x) 🎯 |
|---|---------|----------|---------|----------|
| **9.0** | 9.0 | 9.0 | 9.0 | 9 |
| **9.3** | 10.0 | 9.0 | 9.0 | 9 |
| **9.5** | 10.0 | 9.0 | 10.0 | 10 |
| **9.7** | 10.0 | 9.0 | 10.0 | 10 |
| **-9.0** | -9.0 | -9.0 | -9.0 | -9 |
| **-9.3** | -9.0 | -10.0 | -9.0 | -9 |
| **-9.5** | -9.0 | -10.0 | -10.0 | -9 |
| **-9.7** | -9.0 | -10.0 | -10.0 | -10 |

> 📝 **Note:** The value of `Math.ceil(x)` is exactly the value of `-Math.floor(-x)`.

**Random number example:**

```java
public class Test {
   public static void main(String[] args) {
      for(int i=0; i<5; i++) {
         System.out.println(Math.random());
      }
   }
}
```

📤 **Output:**

```
0.49644420181133186
0.9310877968057992
0.1530478942321487
0.16209426500591828
0.5641161302608104
```

---

## 2. Methods with multiple overloaded forms

| Method 🛠️ | Description 📖 |
|--------|-------------|
| **abs()** | Returns the absolute value of the passed value |
| **max()** | Returns the greater of two passed values |
| **min()** | Returns the smaller of two passed values |

The overloaded forms of `Math.abs()` are:

- `public static int abs(int a)`
- `public static long abs(long a)`
- `public static float abs(float a)`
- `public static double abs(double a)`

Overloaded forms of `Math.max()` are:

- `public static int max(int a, int b)`
- `public static long max(long a, long b)`
- `public static float max(float a, float b)`
- `public static double max(double a, double b)`

The overloaded forms of `Math.min()` are:

- `public static int min(int a, int b)`
- `public static long min(long a, long b)`
- `public static float min(float a, float b)`
- `public static double min(double a, double b)`

**abs, max, min examples:**

```java
public class Test {
   public static void main(String[] args) {
      int a = 10, b = -20;
      System.out.println(Math.abs(a)); // 10
      System.out.println(Math.abs(b)); // 20
      System.out.println(Math.max(a, b)); // 10
      System.out.println(Math.min(a, b)); // -20
   }
}
```

### Java Math class Methods for angle conversion

| Return type 📋 | Method 🛠️ | Description 📖 |
|------------|--------|-------------|
| `double` | **toRadians**(double angdeg) | Converts degrees to radians |
| `double` | **toDegrees**(double angrad) | Converts radians to degrees |

**Convert degree to radian:**

```java
public class Test {
   public static void main(String[] args) {
      // take one value in degree
      double degree = 45;

      // convert to radian
      double radian = Math.toRadians(degree);

      // display value
      System.out.println(radian);
   }
}
```

📤 **Output:**

```
0.7853981633974483
```

**Convert radian to degree:**

```java
public class Test {
   public static void main(String[] args) {
      // take one value in radian
      double radian = 5;

      // convert to  degree
      double degree = Math.toDegrees(radian);

      // display value
      System.out.println(degree);
   }
}
```

📤 **Output:**

```
286.4788975654116
```

### Trigonometry-related Java Math class methods

| Return type 📋 | Method 🛠️ | Description 📖 |
|------------|--------|-------------|
| `double` | **sin**(double a) | Returns the trigonometric sine of an angle in radian |
| `double` | **cos**(double a) | Returns the trigonometric cosine of an angle in radian |
| `double` | **tan**(double a) | Returns the trigonometric tangent of an angle in radian |

Important points on `sin()`, `cos()` and `tan()` methods:

- 📐 **The argument value must be in radians.**
- ⚠️ If the argument is `NaN` or an infinity, then these three methods return `NaN`.

And in the case of `sin()` and `tan()`, if the argument is zero, then the result is a zero with the same sign as the argument.

**Trigonometric function example:**

```java
public class Test {
   public static void main(String[] args) {
      // take one value in degree
      double degree = 45;

      // convert to radian
      double radian = Math.toRadians(degree);

      // display sin, cos, tan values
      System.out.println(Math.sin(radian));
      System.out.println(Math.cos(radian));
      System.out.println(Math.tan(radian));
   }
}
```

📤 **Output:**

```
0.7071067811865475
0.7071067811865476
0.9999999999999999
```

**Special cases:**

```java
// Special cases
Math.sin(Double.NaN)                 // => NaN
Math.cos(Double.POSITIVE_INFINITY)   // => NaN
Math.tan(Double.NEGATIVE_INFINITY)   // => NaN
Math.sin(0.0)                        // => 0.0
Math.sin(-0.0)                       // => -0.0
Math.tan(0.0)                        // => 0.0
Math.tan(-0.0)                       // => -0.0
```

| Return type 📋 | Method 🛠️ | Description 📖 |
|------------|--------|-------------|
| `double` | **asin**(double a) | Returns the arc sine of a value |
| `double` | **acos**(double a) | Returns the arc cosine of a value |
| `double` | **atan**(double a) | Returns the arc tangent of a value |

Points on `asin()`, `acos()` and `atan()` method:

- 🔢 The argument value should be within the range of -1 to 1.
- ❌️ Else result is `NaN`.

And in the case of `asin()` and `atan()`, if the argument is zero, then the result is a zero with the same sign as the argument.

**Arc trigonometric example:**

```java
public class Test {
   public static void main(String[] args) {
      System.out.println(Math.asin(2));
      System.out.println(Math.asin(1));
      System.out.println(Math.atan(-1));
      System.out.println(Math.acos(0.5));
  }
}
```

📤 **Output:**

```
NaN
1.5707963267948966
-0.7853981633974483
1.0471975511965979
```

**Other hyperbolic and utility methods:**

| Return type 📋 | Method 🛠️ | Description 📖 |
|------------|--------|-------------|
| `double` | **sinh**(double x) | Returns the hyperbolic sine of x |
| `double` | **cosh**(double x) | Returns the hyperbolic cosine of x |
| `double` | **tanh**(double x) | Returns the hyperbolic tangent of x |
| `double` | **atan2**(double y, double x) | Returns the angle theta from rectangular to polar coordinates |

**Special cases on sinh(), cosh() and tanh():**

| x 🔢 | sinh(x) | cosh(x) | tanh(x) |
|---|---------|---------|---------|
| **NaN** | NaN | NaN | NaN |
| **zero** | Zero with same sign | 1.0 | Zero with same sign |
| **positive infinity** | positive infinity | positive infinity | +1.0 |
| **negative infinity** | negative infinity | positive infinity | -1.0 |

### Java Math class methods to perform basic arithmetic operations

Important points on these methods:

- 🔢 They return either `int`/`long` value.
- 📅 They were added to Java 1.8 onwards.
- 🔧 Most of them have overloaded forms, but they perform similar operations.
- ⚠️ They throw **`ArithmeticException`**.

Since `ArithmeticException` is an unchecked exception, no need to handle them. Here we list methods having a higher range argument/return type.

| Return type 📋 | Method 🛠️ | Description 📖 |
|------------|--------|-------------|
| `long` | **addExact**(long x, long y) | Returns the sum of its arguments |
| `long` | **subtractExact**(long x, long y) | Returns the difference of the arguments |
| `long` | **multiplyExact**(long x, long y) | Returns the product of the arguments |
| `long` | **floorDiv**(long x, long y) | Returns the largest long value <= algebraic quotient |
| `long` | **floorMod**(long x, long y) | Returns the floor modulus of the long arguments |
| `long` | **incrementExact**(long a) | Returns the argument incremented by one |
| `long` | **decrementExact**(long a) | Returns the argument decremented by one |
| `long` | **negateExact**(long a) | Returns the negation of the argument |
| `int` | **toIntExact**(long value) | Returns the int value of the long argument |

The `floorDiv()` and `floorMod()` throw `ArithmeticException` if the divisor (y) is zero, and the remaining methods throw `ArithmeticException` if the result overflows the return type value.

**All overloaded forms:**

All these methods were added in Java 1.8 but some overloaded forms were added in Java 9 version also.

- `public static int addExact(int x, int y)`
- `public static long addExact(long x, long y)`
- `public static int subtractExact(int x, int y)`
- `public static long subtractExact(long x, long y)`
- `public static int multiplyExact(int x, int y)`
- `public static long multiplyExact(long x, int y)` Since Java 9
- `public static long multiplyExact(long x, long y)`
- `public static int floorDiv(int x, int y)`
- `public static long floorDiv(long x, int y)` Since Java 9
- `public static long floorDiv(long x, long y)`
- `public static int floorMod(int x, int y)`
- `public static int floorMod(long x, int y)` Since Java 9
- `public static long floorMod(long x, long y)`
- `public static int incrementExact(int a)`
- `public static long incrementExact(long a)`
- `public static int decrementExact(int a)`
- `public static long decrementExact(long a)`
- `public static int negateExact(int a)`
- `public static long negateExact(long a)`
- `public static int toIntExact(long value)` (No overloaded form)

#### Examples

**addExact(), subtractExact(), multiplyExact(), floorDiv(), and floorMod():**

```java
public class Test {
   public static void main(String[] args) {

      // variables
      int a = 20;
      int b = 5;

      System.out.println(Math.addExact(a, b)); // 25
      System.out.println(Math.subtractExact(a, b)); // 15
      System.out.println(Math.multiplyExact(a, b)); // 100

      System.out.println(Math.floorDiv(a, b)); // 4
      System.out.println(Math.floorMod(a, b)); // 0
      System.out.println(Math.floorMod(12, 9)); // 3
  }
}
```

Compared to increment (`++`) and decrement (`--`) operators, the **incrementExact() and decrementExact()** are methods returning values. These operators perform the operations and are assigned to the variable itself, no need to do it explicitly but while working with methods we need to assign the return value to the variables.

**incrementExact() and decrementExact():**

```java
public class Test {
   public static void main(String[] args) {

      // variables
      int a = 20;
      int b = 10;

      // methods won't assign return values to
      // the passed variable
      System.out.println(Math.incrementExact(a)); // 21
      System.out.println(a); // 20
      System.out.println(Math.decrementExact(a)); // 19
      System.out.println(a); // 20

      // operators perform the operations
      // and assign it to the variables
      System.out.println(++b); // 11
      System.out.println(b); // 11
      System.out.println(--b); // 10
      System.out.println(b); // 10

      // while working with methods
      // we must assign it explicitly
      a = Math.incrementExact(a);
      System.out.println(a); // 21
      a = Math.decrementExact(a);
      System.out.println(a); // 20
  }
}
```

**negateExact() and toIntExact():**

```java
public class Test {
   public static void main(String[] args) {
      // variables
      int a = 20;

      System.out.println(Math.negateExact(a)); // -20
      System.out.println(a); // 20

      a = Math.negateExact(a);
      System.out.println(a); // -20

      System.out.println(Math.toIntExact(50L)); // 50
  }
}
```

**Cases when ArithmeticException is raised:**

```java
// variables
long a = Long.MAX_VALUE;
long b = Long.MIN_VALUE;

// all of these operations throws
// java.lang.ArithmeticException
Math.addExact(a, 10); // long overflow
Math.subtractExact(a, -10); // long overflow
Math.multiplyExact(a, 10); // long overflow

Math.floorDiv(a, 0); // / by zero
Math.floorMod(a, 0); // / by zero

Math.incrementExact(a); // long overflow
Math.decrementExact(b); // long overflow
Math.negateExact(b); // long overflow
Math.toIntExact(a); // integer overflow
```

### Other Methods

These methods have some overloaded forms.

| Method 🛠️ | Description 📖 |
|--------|-------------|
| `double` **fma**(double a, double b, double c) | Returns the fused multiply-add of three arguments |
| `double` **ulp**(double d) | Returns the size of an ulp of the argument |
| `double` **signum**(double x) | Returns 0 if x=0, 1.0 if x>0, -1.0 if x<0 |
| `double` **hypot**(double x, double y) | Returns sqrt(x^2+y^2) without intermediate overflow |
| `double` **copySign**(double magnitude, double sign) | Returns first argument with sign of second argument |
| `int` **getExponent**(double d) | Returns the unbiased exponent used in representation of x |
| `double` **nextAfter**(double start, double direction) | Returns floating-point number adjacent to first argument toward second |
| `double` **nextUp**(double d) | Returns floating-point value adjacent to d toward positive infinity |
| `double` **nextDown**(double d) | Returns floating-point value adjacent to d toward negative infinity |
| `double` **scalb**(double d, int scaleFactor) | Returns d x 2^scaleFactor |

#### Java Math class Methods added after Java 1.8

**Java 9 additions:**

| Return type 📋 | Method 🛠️ | Description 📖 |
|------------|--------|-------------|
| `long` | **multiplyFull**(int x, int y) | Returns the exact mathematical product of the arguments |
| `long` | **multiplyHigh**(long x, long y) | Returns as long the most significant 64 bits of the 128-bit product |

**Java 15 additions:**

`absExact(x)` -- Returns the mathematical absolute value of x if it is exactly representable as a `long`. Its overloaded forms are:

- `public static int absExact(int a)`
- `public static long absExact(long a)`

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

**Java Tutorial**

**Math Class in Java**
- Java Math class & methods
- [Import Math class in Java](077_Import_Math_Class_in_Java.md)
- [Math.PI in Java Example](079_PI_in_Java_–_Math.PI_Java_Example.md)
- Math.sqrt() method in Java
- Math.pow() method in Java
- Math.max() method in Java
- Math.abs() method in Java
- Math.ceil() method in Java
- Math.floor() method in Java
- Math.round() method in Java
- Math.random() method Java

**Java.lang.Object Class**
- [Object Class in Java](069_Object_Class_in_Java.md)
- getClass() method
- [hashCode() Method](071_Hashcode_in_Java_–_hashCode()_Method.md)
- toString() Method
- Java equals() Method
- == vs equals() in Java
- HashCode() vs equals()
- [Clone() Method in Java](074_Clone()_Method_in_Java.md)
- Object Class Quiz Set-1
- Object Class Quiz Set-2
- equals() Method Quiz
- Hashcode Value Quiz
