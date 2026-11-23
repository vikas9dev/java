# Math.ceil() Method in Java

**Math.ceil() Method in Java** | The `ceil()` method of [java.lang.Math class](078_Java_Math_Class_with_Examples.md) returns the smallest (closest to negative infinity) `double` value that is greater than or equal to the argument and is equal to a mathematical integer.

- [Java Math.ceil() Examples](#java-mathceil-examples)
- [Special cases](#special-cases)

The word CEIL is short for CEILING. The `Math.ceil()` method essentially rounds up to the nearest whole number and is the opposite of the `Math.floor()` method (which rounds down to the nearest whole number).

**Method prototype:**

```java
public static double ceil(double a)
```

---

## 1. Java Math.ceil() Examples

**Basic ceil example:**

```java
public class Test{
   public static void main(String[] args) {
      System.out.println(Math.ceil(2.0)); // 2.0
      System.out.println(Math.ceil(-2.0)); // -2.0

      System.out.println(Math.ceil(2.5)); // 3.0
      System.out.println(Math.ceil(-2.5)); // -2.0

      System.out.println(Math.ceil(2.9)); // 3.0
      System.out.println(Math.ceil(-2.9)); // -2.0
   }
}
```

📤 **Output:**

```
2.0
-2.0
3.0
-2.0
3.0
-2.0
```

**When the argument is positive:**

| Expression 🔢 | Result ⬆️ |
|-----------|--------|
| `Math.ceil(2.0)` | 2.0 |
| `Math.ceil(2.1)` | 3.0 |
| `Math.ceil(2.5)` | 3.0 |
| `Math.ceil(2.9)` | 3.0 |
| `Math.ceil(3.0)` | 3.0 |
| `Math.ceil(3.3)` | 4.0 |
| `Math.ceil(3.5)` | 4.0 |
| `Math.ceil(3.9)` | 4.0 |

**When the argument is negative:**

| Expression 🔢 | Result ⬆️ |
|-----------|--------|
| `Math.ceil(-2.0)` | -2.0 |
| `Math.ceil(-2.1)` | -2.0 |
| `Math.ceil(-2.5)` | -2.0 |
| `Math.ceil(-2.9)` | -2.0 |
| `Math.ceil(-3.0)` | -3.0 |
| `Math.ceil(-3.3)` | -3.0 |
| `Math.ceil(-3.5)` | -3.0 |
| `Math.ceil(-3.9)` | -3.0 |

If we import the Math class statically then we can invoke `ceil()` method without calling through its class name.

**Static import (all members):**

```java
import static java.lang.Math.*;
public class Test{
   public static void main(String[] args) {
      System.out.println(ceil(9.9)); // 10.0
      System.out.println(ceil(5.0)); // 5.0
   }
}
```

The `import static java.lang.Math.*;` statement will import all static members of the Math class. But if we want to import only the `ceil()` method of the Math class, not another static method and variables of Math class then we can use the `import static java.lang.Math.ceil;` statement. Learn more about [static import in Java](024_Static_Import_in_Java.md)

**Static import (ceil only):**

```java
import static java.lang.Math.ceil;
public class Test{
   public static void main(String[] args) {
      System.out.println(ceil(9.9)); // 10.0
      System.out.println(ceil(5.0)); // 5.0
   }
}
```

---

## 2. Special cases

1. 🔢 **If passed value is an integer then the same value is returned.**

```
Math.ceil(5)   => 5.0
Math.ceil(6.0) => 6.0
```

2. ♾️ **If the argument is zero (either positive or negative), infinity or NaN then also the same value is returned.**

**Zero argument:**

```
Math.ceil(0)  => 0.0
Math.ceil(-0) => 0.0
```

**Infinity argument:**

```
Math.ceil(Double.POSITIVE_INFINITY) => Infinity
Math.ceil(Double.NEGATIVE_INFINITY) => -Infinity
```

**NaN argument:**

```
Math.ceil(Double.NaN) => NaN
```

3. ⚠️ **If the argument value is less than zero but greater than -1.0, then the result is negative zero.**

| Expression 🔢 | Result 📤 |
|-----------|--------|
| `Math.ceil(-0.0)` | -0.0 |
| `Math.ceil(-0.1)` | -0.0 |
| `Math.ceil(-0.3)` | -0.0 |
| `Math.ceil(-0.5)` | -0.0 |
| `Math.ceil(-0.7)` | -0.0 |
| `Math.ceil(-0.9)` | -0.0 |
| `Math.ceil(-1.0)` | -1.0 |

> 📝 **Note:** The value of `Math.ceil(x)` is exactly the value of `-Math.floor(-x)`.

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
