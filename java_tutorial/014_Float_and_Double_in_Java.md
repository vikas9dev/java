# Float and Double in Java

**Float and Double in Java** | Understanding floating-point data types, their sizes, precision differences, and usage in Java programming.

- [Double Data Type in Java](#double-data-type-in-java)
- [Float Data Type in Java](#float-data-type-in-java)
- [Comparison Table](#comparison-table)
- [Comparison with C/C++ Language](#comparison-with-cc-language)
- [Sample Programs](#sample-programs)
- [Difference Between Float and Double in Java](#difference-between-float-and-double-in-java)
- [Precision Differences](#precision-differences)

---

## 1. Double Data Type in Java

The `byte`, `short`, `int`, and `long` data types are used to store the integer values in Java programming, but the `float` and `double` data types used to **store real or floating-point numbers.** Prerequisites: [Data types in Java programming](013_Data_Types_in_Java.md)

| Property 🏷️ | Value 📋 |
|-------------|---------|
| **Size** | 8 bytes |
| **Range** | -3.4e38 to 3.4e38 (4.94065645841246544e-324 to 1.79769313486231570e+308) |
| **Default value** | `0.0` |
| **Corresponding Wrapper class** | `Double` |

🔑 **Key Point:** The suffix `D` or `d` is optional for the `double` data type.

```java
double d2 = 95.5;  // valid
double d3 = 95.5D; // valid
double d4 = 95.5d; // valid
```

💡 **Tip:** Except `boolean`, the `double` data type can hold all other primitive data type values.

**Demonstrating double compatibility:**

```java
public class Test {
  public static void main(String[] args) {
     double d1 = (byte)10; // byte
     double d2 = (short)20; // short
     double d3 = 30; // int
     double d4 = 40L; // long
     double d5 = 'a'; // char
     double d6 = 97.5; // double
     double d7 = 95.0F; // float
     // double d8 = true; // error

     // display values
     System.out.println(d1); // 10.0
     System.out.println(d2); // 20.0
     System.out.println(d3); // 30.0
     System.out.println(d4); // 40.0
     System.out.println(d5); // 97.0
     System.out.println(d6); // 97.5
     System.out.println(d7); // 95.0
  }
}
```

In Java, by default, **every floating-point number is of the `double` data type**. When we use floating-point numbers inside the program then the compiler and JVM treat them as a `double` data type.

**Proof using method overloading:**

```java
// program to show, by default every floating-point
// number is of the double data type
class Test{
   public static void main(String[] args) {
      m1(1.9);
   }
   static void m1(float n){
      System.out.println("float parameter.");
   }
   static void m1(double n){
      System.out.println("double parameter.");
   }
}
```

📤 **Output:**

```
double parameter
```

In the above program, we use the method overloading concept (We will discuss it later, At this time don't think much about method overloading, it is used here just to prove the concept). From the main method we call a function `m1()` and method `m1` has value 1.9. By default, every floating-point number is of the `double` data type. So, Compiler and JVM considered the number 1.9 as the `double` data type. Hence, the method having parameter `double` will be executed.

---

## 2. Float Data Type in Java

| Property 🏷️ | Value 📋 |
|-------------|---------|
| **Size** | 4 bytes |
| **Range** | -1.7e38 to 1.7e38 (1.40129846432481707e-45 to 3.40282346638528860e+38) |
| **Default value** | `0.0F` |
| **Corresponding Wrapper class** | `Float` |

We **must add suffix `F`** or `f` **to represent a floating-point number as a `float` data type** and to store the floating-point number in a `float` variable.

```java
float n1 = 9.9F;
```

> 📝 **Note:** We can assign floating point numbers directly to `double` data type but we can't assign directly to `float` data type.

```java
float n1 = 9.9;   // error, we must use F or f suffix
double n2 = 9.9;  // valid
```

In regular programming calculations, we don't use `float`. If we ensure that the result range is within the range of `float` data type then we can choose a `float` data type for saving memory. Generally, we use `double` because of two reasons:

- 🏷️ If we want to use the floating-point number as `float` data type then method caller must explicitly suffix `F` or `f`, because by default every floating-point number is treated as `double`. It increases the burden to the programmer. If we use a floating-point number as `double` data type then we don't need to add any suffix.
- 🎯 `Float` is a single-precision data type means it occupies 4 bytes. Hence in large computations, we will not get a complete result. If we choose `double` data type, it occupies 8 bytes and we will get complete results.

📏 **Bit representation:**

- `float` is represented in 32 bits, with 1 sign bit, 8 bits of exponent, and 23 bits of the significand
- `double` is represented in 64 bits, with 1 sign bit, 11 bits of exponent, and 52 bits of significand

> ⚠️ **Caution:** Both `float` and `double` data types were designed especially for scientific calculations, where approximation errors are acceptable. If accuracy is the most prior concern then, it is recommended to use [BigDecimal class](https://docs.oracle.com/javase/1.5.0/docs/api/java/math/BigDecimal.html) instead of `float` or `double` data types.

---

## 3. Comparison Table

| Property 🏷️ | float 🅰️ | double 🅱️ |
|-------------|---------|----------|
| **Size** | 4 bytes | 8 bytes |
| **Default value** | `0.0F` | `0.0` |
| **Range** | -1.7e38 to 1.7e38 (1.40129846432481707e-45 to 3.40282346638528860e+38) | -3.4e38 to 3.4e38 (4.94065645841246544e-324 to 1.79769313486231570e+308) |

---

## 4. Comparison with C/C++ Language

In C language we can store the floating-point number in either `float` or `double` variable, even we can store in `int` type variable but C compiler doesn't throw an error because it will do required conversions.

| Statement 📝 | C Language 🅰️ | Java Language 🅱️ |
|-------------|--------------|-----------------|
| **`int n1 = 9.9;`** | ✅ Allowed | ❌️ Not allowed |
| **`float n2 = 9.9;`** | ✅ Allowed | ❌️ Not allowed |
| **`double n3 = 9.9;`** | ✅ Allowed | ✅ Allowed |

In Java, we can't do the same thing. If we want to assign a floating-point number to a `float` variable then we must add suffix `F` or `f`. And if we want to assign to another variable then we must use a cast operator. Below all statements are valid:

```java
short n1 = (short)9.0;
int n2 = (int)9.0;
float n3 = 9.0F;
float n4 = (float)9.0;
double n5 = 9.0;
```

---

## 5. Sample Programs

**Program1: Write a Java program to demonstrate Floating-point numbers in Java.**

```java
class FloatingPointNumber {
  public static void main(String[] args) {
     double a = 9.5;
     // float b = 15.5; // error: incompatible types
     float c = 20.9F;

     System.out.println("Double = " + a);
     System.out.println("Float = " + c);
  }
}
```

📤 **Output:**

```
Double = 9.5
Float = 20.9
```

**Program2: Write a Java program to find the sum and average of three floating-point numbers.**

```java
class SumAverage {
  public static void main(String[] args) {
     double a = 9.5;
     double b = 15.5;
     double c = 20.9;

     double sum = a+b+c;
     double average = sum / 3;

     System.out.println("Sum = " + sum);
     System.out.println("Average = " + average);
  }
}
```

📤 **Output:**

```
Sum = 45.9
Average = 15.299999999999999
```

---

## 6. Difference Between Float and Double in Java

| Feature 🏷️ | float 🅰️ | double 🅱️ |
|------------|---------|----------|
| **Size** | 4 bytes | 8 bytes |
| **Precision** | Single precision | Double precision |
| **Decimal accuracy** | 5 to 6 decimal places | 14 to 15 decimal places |
| **Range** | -1.7e38 to 1.7e38 | -3.4e38 to 3.4e38 |
| **Suffix requirement** | Must use `F` or `f` suffix | `D` or `d` are optional suffixes |
| **Wrapper class** | `Float` | `Double` |

See more differences between [float vs double in Java](https://javahungry.blogspot.com/2019/11/difference-between-float-and-double-in-java.html).

---

## 7. Precision Differences

Different behaviors of storing the same value using `float` and `double` data type.

In Java, **the `float` and `double` data types store same value for x.0, x.5 but it stores different values for x.1, x.2, x.3, x.4, x.6, x.7, x.8, and x.9 where x is any integer number.**

**Precision comparison program:**

```java
public class Test {
  public static void main(String[] args) {
     double d1 = 1.0;
     float f1 = 1.0F;
     System.out.printf("%.15f \n", d1);
     System.out.printf("%.15f \n", f1);

     // compare d1 and f1
     if(d1 == f1)
     System.out.println("Both are same.");
     else
     System.out.println("Both are different.");

     double d2 = 1.1;
     float f2 = 1.1F;
     System.out.printf("%.15f \n", d2);
     System.out.printf("%.15f \n", f2);

     // compare d2 and f2
     if(d2 == f2)
     System.out.println("Both are same.");
     else
     System.out.println("Both are different.");
  }
}
```

📤 **Output:**

```
1.000000000000000
1.000000000000000
Both are same.
1.100000000000000
1.100000023841858
Both are different.
```

From the above program, we can observe that for 1.0 both `double` and `float` data type store the same value but for the 1.1 both stores different values. Let us see some more programs related to it.

**Guess the output of the below program:**

```java
class CheckDifference1 {
   public static void main(String[] args) {
      double a = 9.2;
      float b = 9.2F;

      if(a==b) System.out.println("a and b are equal");
      else System.out.println("a and b are different");

      System.out.printf("a = %.15f \n", a);
      System.out.printf("b = %.15f \n", b);

      if(9.2==9.2F) System.out.println("9.2 and 9.2F are equal");
      else System.out.println("9.2 and 9.2F are different");
   }
}
```

📤 **Output:**

```
a and b are different
a = 9.200000000000000
b = 9.199999809265137
9.2 and 9.2F are different
```

> ⚠️ **Caution:** Due to these differences **we should not use `==` operator with `float` and `double` data types to compare the values**. Instead of using `==` operator, we should use `>` and `<` comparison operators.
