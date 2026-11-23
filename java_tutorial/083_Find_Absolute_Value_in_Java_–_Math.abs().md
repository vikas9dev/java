# Find Absolute Value in Java -- Math.abs()

**Find Absolute Value in Java -- Math.abs()** | To find the absolute value of a number, the `abs()` method is given in the [java.lang.Math class](078_Java_Math_Class_with_Examples.md). There are several overloaded forms to accept different types of arguments and return accurate values.

- [Math.abs() examples](#mathabs-examples)
- [Special Cases while finding absolute value in Java](#special-cases-while-finding-absolute-value-in-java)

- ✅ **If the argument is not negative, then the same argument is returned.**
- 🔄 **If the argument is negative, then the negation of the argument is returned.**

The **overloaded forms** of `java.lang.Math.abs()` method are:

- `public static int abs(int a)`
- `public static long abs(long a)`
- `public static float abs(float a)`
- `public static double abs(double a)`

**Implementation:**

```java
public static int abs(int a) {
   return (a < 0) ? -a : a;
}
```

---

## 1. Math.abs() examples

**All data type examples:**

```java
public class Test{
   public static void main(String[] args) {

      // argument is int type
      System.out.println(Math.abs(-9)); // 9
      System.out.println(Math.abs(9)); // 9

      // argument is long type
      System.out.println(Math.abs(-10L)); // 10
      System.out.println(Math.abs(10L)); // 10

      // argument is float type
      System.out.println(Math.abs(-9F)); // 9.0
      System.out.println(Math.abs(9F)); // 9.0

      // argument is double type
      System.out.println(Math.abs(-10.0)); // 10.0
      System.out.println(Math.abs(10.0)); // 10.0
   }
}
```

If the argument is negative then all of them return the absolute value as the negation of the argument, else the same argument is returned back.

If we import the Math class statically then we can invoke the `abs()` method without calling through its class name.

**Static import (all members):**

```java
import static java.lang.Math.*;
public class Test{
   public static void main(String[] args) {
      System.out.println(abs(-9)); // 9
      System.out.println(abs(9)); // 9
   }
}
```

The `import static java.lang.Math.*;` statement will import all static members of the Math class. But if we want to import only the `abs()` method of the Math class, not another static method and variables of Math class then we can use the `import static java.lang.Math.abs;` statement. Learn more about [static import in Java](024_Static_Import_in_Java.md)

**Static import (abs only):**

```java
import static java.lang.Math.abs;
public class Test {
   public static void main(String[] args) {
      System.out.println(abs(-9)); // 9
      System.out.println(abs(9)); // 9
   }
}
```

📤 **Output:**

```
9
9
```

---

## 2. Special Cases while finding absolute value in Java

1. ⚠️ When the **passed argument is of `int` data type and** it is **equal to `Integer.MIN_VALUE`** (i.e. -2147483648 or -2^31) then `abs(int a)` **returns the same value**, which is negative.

```java
System.out.println(Math.abs(-2147483648));
```

📤 **Output:** `-2147483648`

2. ⚠️ Similarly, when the **passed value is of `long` data type and** it is **equal to `Long.MIN_VALUE`** (i.e. -9223372036854775808 or -2^63) then `abs(long a)` **returns** absolute value as the **same value**, which is negative.

```java
System.out.println(Math.abs(-9223372036854775808L));
```

📤 **Output:** `-9223372036854775808`

> ⚠️ **Caution:** These edge cases occur because of integer overflow. The absolute value of `Integer.MIN_VALUE` and `Long.MIN_VALUE` cannot be represented in their respective types.

3. 0️⃣ **If the argument is positive zero or negative zero, the result is positive zero.**

```java
System.out.println(Math.abs(-0)); // 0
System.out.println(Math.abs(0)); // 0
System.out.println(Math.abs(-0.0)); // 0.0
System.out.println(Math.abs(0.0)); // 0.0
```

📤 **Output:**

```
0
0
0.0
0.0
```

4. ♾️ **If the argument is infinite, the result is positive infinity.**

```java
System.out.println(Math.abs(Double.POSITIVE_INFINITY));
System.out.println(Math.abs(Double.NEGATIVE_INFINITY));
```

📤 **Output:**

```
Infinity
Infinity
```

5. ❌️ **If the argument is NaN, the result is NaN.**

```java
System.out.println(Math.abs(Double.NaN));
System.out.println(Math.abs(Float.NaN));
```

📤 **Output:**

```
NaN
NaN
```

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

**Java Tutorial**

**Math Class in Java**
- [Java Math class & methods](078_Java_Math_Class_with_Examples.md)
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
