# PI in Java -- Math.PI Java Example

**PI in Java -- Math.PI Java Example** | To get and use the PI (π) value in Java, we can use the `Math.PI` constant defined in the [java.lang.Math class](078_Java_Math_Class_with_Examples.md).

- [How to Use PI in Java](#how-to-use-pi-in-java)

The `Math.PI` is a `static final double` type variable having a double value that is closer than any other to [π](https://en.wikipedia.org/wiki/Pi), the ratio of the circumference of a circle to its diameter.

**Declaration:**

```java
public static final double PI = 3.14159265358979323846;
```

Since it is a static variable so, we can **directly access** it **through its class name** like `Math.PI`.

**Basic usage:**

```java
public class Test {
  public static void main(String[] args) {
     double x = Math.PI;
     System.out.println(x);
  }
}
```

📤 **Output:**

```
3.141592653589793
```

If we [import the Math class statically](077_Import_Math_Class_in_Java.md) then we can access `PI` without calling through its class name.

**Static import (all members):**

```java
import static java.lang.Math.*;
public class Test {
  public static void main(String[] args) {
    System.out.println(PI);
  }
}
```

The `import static java.lang.Math.*;` statement will import all static members of the Math class. But if we want to import only the `PI` variable of the Math class, not other static methods and variables of the Math class then we can use the `import static java.lang.Math.PI;` statement.

Learn more about: [static import in Java Language](024_Static_Import_in_Java.md)

**Static import (PI only):**

```java
import static java.lang.Math.PI;
public class Test {
  public static void main(String[] args) {
     System.out.println(PI);
  }
}
```

---

## 1. How to Use PI in Java

To use PI in Java, first, get the PI value by calling the `PI` variable of the `Math` class, and then use it in the program. Let us see this through an example.

**Java Program to Find the Area of a Circle using Math.PI:**

```java
public class Area {
  public static void main(String[] args) {
     double radius = 10;
     double area = Math.PI*radius*radius;
     System.out.println(area);
  }
}
```

📤 **Output:**

```
314.1592653589793
```

In this example, we are accessing the PI value through the class name directly. Using the import statement we can get the PI value without using its class name.

**Area of circle with static import (all members):**

```java
import static java.lang.Math.*;
public class Area {
  public static void main(String[] args) {
     double radius = 10;
     double area = PI*radius*radius;
     System.out.println(area);
  }
}
```

> 📝 **Note:** In this example, even though we need only the `PI` value but we are importing all the static methods and variables of the Math class which are not being used in this program. Therefore it is better to import only the `PI` variable of the Math class to get the π value.

If we import the `PI` variable of the Math class through static import then only the `PI` variable will be available to the class, other static methods and variables will not be there.

**Area of circle with static import (PI only):**

```java
import static java.lang.Math.PI;
public class Area {
  public static void main(String[] args) {
     double radius = 10;
     double area = PI*radius*radius;
     System.out.println(area);
  }
}
```

> 💡 **Tip:** For best practice, import only the specific members you need rather than using the wildcard `*` import.

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

**Java Tutorial**

**Math Class in Java**
- [Java Math class & methods](078_Java_Math_Class_with_Examples.md)
- [Import Math class in Java](077_Import_Math_Class_in_Java.md)
- Math.PI in Java Example
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
