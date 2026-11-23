# Math.pow() Method in Java

**Math.pow() Method in Java** | To find power value in Java, the `pow()` method is given in the `java.lang.Math` class. It accepts two `double`-type arguments and returns the value of the first argument raised to the power of the second argument.

- [Math.pow() Examples](#mathpow-examples)
- [Special Cases](#special-cases)

**Method prototype:**

```java
public static double pow(double a, double b)
```

---

## 1. Math.pow() Examples

**Basic power example:**

```java
public class Test{
   public static void main(String[] args) {
      System.out.println(Math.pow(2, 3));
   }
}
```

📤 **Output:**

```
8.0
```

If we import the Math class statically then we can invoke the `pow()` method without calling through its class name.

**Static import (all members):**

```java
import static java.lang.Math.*;
public class Test{
   public static void main(String[] args) {
      System.out.println(pow(2, 3)); // 8
   }
}
```

The `import static java.lang.Math.*;` statement will import all static members of the Math class. But if we want to import only the `pow()` method of the Math class, not another static method and variables of the Math class then we can use the `import static java.lang.Math.pow;` statement. Learn more about [static import in Java](024_Static_Import_in_Java.md)

**Static import (pow only):**

```java
import static java.lang.Math.pow;
public class Test{
   public static void main(String[] args) {
      System.out.println(pow(2, 3)); // 8
   }
}
```

📤 **Output:**

```
8
```

**Java program to find the area of a circle:**

```java
public class CircleArea{
   public static void main(String[] args) {
      int radius = 10;

      // circle area = π * r * r
      double area = Math.PI * Math.pow(radius, 2);

      // display area
      System.out.println(area);
   }
}
```

📤 **Output:**

```
314.1592653589793
```

---

## 2. Special Cases

Assume `x` is any number:

| First argument 🔹 | Second argument 🔸 | Return value by pow() 📤 |
|------------|-------------|-------------------|
| **positive or negative zero** | x | 1.0 |
| **x** | 1.0 | x |
| **x** | NaN | NaN |
| **NaN** | Non zero number | NaN |
| **Math.abs(x) > 1** | positive infinity | positive infinity |
| **Math.abs(x) < 1** | negative infinity | positive infinity |
| **Math.abs(x) > 1** | negative infinity | 0.0 |
| **Math.abs(x) < 1** | positive infinity | 0.0 |
| **Math.abs(x) = 1** | infinity | NaN |
| **positive zero** | x > 0 | 0.0 |
| **positive infinity** | x < 0 | 0.0 |
| **positive zero** | x < 0 | positive infinity |
| **positive infinity** | x > 0 | positive infinity |

> 💡 **Tip:** The `pow()` method always returns a `double` value. If you need an integer result, cast it explicitly: `(int) Math.pow(2, 3)`.

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
