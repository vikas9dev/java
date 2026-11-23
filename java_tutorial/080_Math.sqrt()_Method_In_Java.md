# Math.sqrt() Method In Java

**Math.sqrt() Method In Java** | The `sqrt()` method of `java.lang.Math` class is given to calculate the square root value of a given number. It returns the correctly rounded positive square root of a `double` value.

- [Java Math.sqrt() Examples](#java-mathsqrt-examples)
- [Special Cases](#special-cases)

**Method prototype:**

```java
public static double sqrt(double a)
```

- 🔢 **Argument type:** `double`
- 📥 **Argument:** a number
- 📤 **Return type:** `double`
- ✅ **Return value:** positive square root of the passed argument

Since the `sqrt()` method is a static method so we can call it directly through its class name like `Math.sqrt()`. Or for convenience, we can import all static members of the Math class using the `import static` statement.

---

## 1. Java Math.sqrt() Examples

**Basic square root example:**

```java
public class SquareRoot {
   public static void main(String[] args) {

      // take a number
      int num1 = 25;

      // find square root value
      double result = Math.sqrt(num1);

      // display result
      System.out.println(result);
   }
}
```

📤 **Output:**

```
5.0
```

**More examples:**

| Expression 🔢 | Result 📤 |
|-----------|--------|
| `Math.sqrt(1)` | 1.0 |
| `Math.sqrt(2)` | 1.4142135623730951 |
| `Math.sqrt(3)` | 1.7320508075688772 |
| `Math.sqrt(4)` | 2.0 |
| `Math.sqrt(5)` | 2.23606797749979 |
| `Math.sqrt(6)` | 2.449489742783178 |
| `Math.sqrt(7)` | 2.6457513110645907 |
| `Math.sqrt(8)` | 2.8284271247461903 |
| `Math.sqrt(9)` | 3.0 |
| `Math.sqrt(10)` | 3.1622776601683795 |

If we import the Math class statically then we can invoke `sqrt()` method without calling through its class name.

**Static import (all members):**

```java
// static import
import static java.lang.Math.*;
public class SquareRoot {
   public static void main(String[] args) {

      // find square root value
      // invoke sqrt() without class name
      double result = sqrt(81);

      // display result
      System.out.println(result);
   }
}
```

📤 **Output:**

```
9.0
```

The `import static java.lang.Math.*;` statement will import all static members of the Math class. But if we want to import only the `sqrt()` method of the Math class, not another static method and variables of the Math class then we can use the `import static java.lang.Math.sqrt;` statement. Learn more about [static import in Java](024_Static_Import_in_Java.md)

**Static import (sqrt only):**

```java
// static import
import static java.lang.Math.sqrt;
public class SquareRoot {
   public static void main(String[] args) {

      // find square root value
      // invoke sqrt() without class name
      double result = sqrt(20);

      // display result
      System.out.println(result);
   }
}
```

📤 **Output:**

```
4.47213595499958
```

---

## 2. Special Cases

- ❌️ If the argument is `NaN` or less than zero, then the result is `NaN`.
- ♾️ If the argument is positive infinity, then the result is positive infinity.
- 0️⃣ If the argument is positive zero or negative zero, then the result is the same as the argument.
- ✅ Otherwise, the result is the double value closest to the true mathematical square root of the argument value.

**Negative argument:**

```java
System.out.println(sqrt(-81));
```

📤 **Output:** `NaN`

**NaN argument:**

```java
System.out.println(sqrt(Double.NaN));
```

📤 **Output:** `NaN`

**Positive infinity argument:**

```java
System.out.println(sqrt(Double.POSITIVE_INFINITY));
```

📤 **Output:** `Infinity`

**Negative infinity argument:**

```java
System.out.println(sqrt(Double.NEGATIVE_INFINITY));
```

📤 **Output:** `NaN`

**Zero argument:**

```java
System.out.println(sqrt(0));
```

📤 **Output:** `0.0`

> 💡 **Tip:** Also see: Java program to find the square root of a number without the sqrt method

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
