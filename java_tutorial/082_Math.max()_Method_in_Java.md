# Math.max() Method in Java

**Math.max() Method in Java** | In Java to find the max of two numbers, we can use the `max()` method defined in the [java.lang.Math class](078_Java_Math_Class_with_Examples.md). There are several overloaded forms that all return the greater of two arguments.

- [Math.max() Examples in Java](#mathmax-examples-in-java)
- [Special Cases of Java Math.max()](#special-cases-of-java-mathmax)

The overloaded forms of `Math.max()` methods are:

- `public static int max(int a, int b)`
- `public static long max(long a, long b)`
- `public static float max(float a, float b)`
- `public static double max(double a, double b)`

**Implementation:**

```java
public static int max(int a, int b) {
   return (a >= b) ? a : b;
}
```

---

## 1. Math.max() Examples in Java

**Basic max example:**

```java
public class Test {
   public static void main(String[] args) {
      System.out.println(Math.max(10, 20));
      System.out.println(Math.max(15, 15));
      System.out.println(Math.max(25, 15));
   }
}
```

📤 **Output:**

```
20
15
25
```

If we import the Math class statically then we can invoke the `max()` method without calling through its class name.

**Static import (all members):**

```java
import static java.lang.Math.*;
public class Test {
   public static void main(String[] args) {
      System.out.println(max(10, 20)); // 20
   }
}
```

The `import static java.lang.Math.*;` statement will import all static members of the Math class. But if we want to import only the `max()` method of the Math class, not another static method and variables of the Math class then we can use the `import static java.lang.Math.max;` statement. Learn more about [static import in Java](024_Static_Import_in_Java.md)

**Static import (max only):**

```java
import static java.lang.Math.max;
public class Test {
   public static void main(String[] args) {
      System.out.println(max(10, 20));
   }
}
```

---

## 2. Special Cases of Java Math.max()

1. ⚖️ If the arguments have the same value, the result is the same value.

```java
System.out.println(Math.max(10, 10));
```

📤 **Output:** `10`

2. ❌️ If either value is `NaN`, then the result is `NaN`.

```java
import static java.lang.Math.max;
public class Test {
   public static void main(String[] args) {
      System.out.println(Math.max(Double.NaN, 20));
      System.out.println(Math.max(10, Double.NaN));
      System.out.println(Math.max(Double.NaN, Double.NaN));
   }
}
```

📤 **Output:**

```
NaN
NaN
NaN
```

3. 0️⃣ Unlike the numerical comparison operators, this method considers negative zero to be strictly smaller than positive zero. If one argument is positive zero and the other negative zero, the result is positive zero.

```java
public class Test {
   public static void main(String[] args) {
      System.out.println(Math.max(0, -0));
      System.out.println(Math.max(-0, 0));
   }
}
```

📤 **Output:**

```
0
0
```

> 💡 **Tip:** To find the maximum of more than two values, chain `Math.max()` calls: `Math.max(a, Math.max(b, c))`.

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
