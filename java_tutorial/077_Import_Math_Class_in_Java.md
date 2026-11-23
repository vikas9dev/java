# Import Math Class in Java

**Import Math Class in Java** | The [Math class in Java](078_Java_Math_Class_with_Examples.md) is available in the `java.lang` package. Since `java.lang` package is the default package to every Java program, there is no need to import the Math class explicitly.

- [Static Import Math class in Java](#static-import-math-class-in-java)

But all variables and methods of `Math` class are `static`. There are two ways to access static variables or methods of Math class:

- 🔧 Directly through its class name (like Math.pow(), Math.sqrt())
- 📦 Using [static import statement](024_Static_Import_in_Java.md) to import all static members of the class

**Using class name directly:**

```java
public class Test {
   public static void main(String[] args) {

      System.out.println(Math.PI); // 3.141592653589793
      System.out.println(Math.E); // 2.718281828459045

      System.out.println(Math.pow(2, 3)); // 8.0
      System.out.println(Math.exp(1)); // 2.718281828459045
      System.out.println(Math.log10(10)); // 1.0

      System.out.println(Math.sqrt(64)); // 8.0
      System.out.println(Math.cbrt(64)); // 4.0

      System.out.println(Math.abs(-20)); // 20
      System.out.println(Math.max(10, -20)); // 10
      System.out.println(Math.min(10, -20)); // -20
   }
}
```

📤 **Output:**

```
3.141592653589793
2.718281828459045
8.0
2.718281828459045
1.0
8.0
4.0
20
10
-20
```

Let us see a Java program to demonstrate how to import math class in Java and use them in our program.

**Java Program to Find the Area of a Circle:**

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

> 💡 **Tip:** See all variables and methods of Math class in Java with many examples: [Math class in Java](078_Java_Math_Class_with_Examples.md). Also see: Top 100+ Java Programming Examples With Output, [Top 40+ Array Programs in Java](026_Java_Array_[With_Examples].md)

---

## 1. Static Import Math class in Java

We can import the Math class statically and then invoke static members without calling through its class name. Learn more about how static import works, and the difference between normal import vs static import in Java: [Static import in Java](024_Static_Import_in_Java.md).

Statement to import Math class all static members: `import static java.lang.Math.*;`

The `import static java.lang.Math.*;` statement will import all static variables and methods of the Math class.

**Static import example (all members):**

```java
import static java.lang.Math.*;
public class Test {
   public static void main(String[] args) {

      System.out.println(PI); // 3.141592653589793
      System.out.println(E); // 2.718281828459045

      System.out.println(pow(2, 3)); // 8.0
      System.out.println(exp(1)); // 2.718281828459045
      System.out.println(log10(10)); // 1.0

      System.out.println(sqrt(64)); // 8.0
      System.out.println(cbrt(64)); // 4.0

      System.out.println(abs(-20)); // 20
      System.out.println(max(10, -20)); // 10
      System.out.println(min(10, -20)); // -20
   }
}
```

If we want to import only a particular static member using the static import concept then we have to use the following syntax: `import static package.className.staticMember;`

It will import only a particular static member. Example: `import static Math.PI;` to import only PI variable, `import static Math.sqrt;` to import only `sqrt()` method.

**Static import example (specific members):**

```java
import static java.lang.Math.PI;
import static java.lang.Math.pow;
public class Test{
   public static void main(String[] args) {
      int radius = 10;

      // circle area = π * r * r
      double area = PI * pow(radius, 2);

      // display area
      System.out.println(area);
   }
}
```

📤 **Output:**

```
314.1592653589793
```

> 📝 **Note:** The Math class contains several methods having multiple overloaded forms. For example abs(), max() and `min()` methods contain 4 overloaded forms per method.

The overloaded forms of Math.max() are:

- `public static int max(int a, int b)`
- `public static long max(long a, long b)`
- `public static float max(float a, float b)`
- `public static double max(double a, double b)`

If the method contains several overloaded forms and we are using static import to import only that particular method then all of its overloaded forms are also imported.

**Overloaded max() with static import:**

```java
import static java.lang.Math.max;
public class Test{
   public static void main(String[] args) {

      // int max(int a, int b)
      System.out.println(max(10, 20)); // 20

      // long max(long a, long b)
      System.out.println(max(40L, 30L)); // 40

      // float max(float a, float b)
      System.out.println(max(10.5F, 19.9F)); // 19.9

      // double max(double a, double b)
      System.out.println(max(25.0, 15.5)); // 25.0
   }
}
```

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

**Java Tutorial**

**Math Class in Java**
- [Java Math class & methods](078_Java_Math_Class_with_Examples.md)
- Import Math class in Java
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
