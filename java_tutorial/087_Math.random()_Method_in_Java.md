# Math.random() Method in Java

**Math.random() Method in Java** | The `Math.random()` method in Java returns a double value with a positive sign, greater than or equal to 0.0 and less than 1.0. The returned values are chosen pseudorandomly with (approximately) uniform distribution from that range.

- [Java Math.random() Example](#java-mathrandom-example)
- [Java Math.random() between 1 to N](#java-mathrandom-between-1-to-n)
- [Generate Numbers within a given range in Java](#generate-numbers-within-a-given-range-in-java)
- [Other Uses of Math.random() Method in Java](#other-uses-of-mathrandom-method-in-java)
- [How Math.random() is implemented](#how-mathrandom-is-implemented)
- [Related Links](#related-links)

---

## 1. Java Math.random() Example

📐 **Method prototype:**

```java
public static double random()
```

🎲 **Math.random() Java Range:** Greater than or equal to 0.0 and less than 1.0

Java program to demonstrate `Math.random()` method. We will take a loop and call the `Math.random()` method multiple times. In each execution, it gives a different double value with a positive sign, greater than or equal to 0.0 and less than 1.0.

**Basic random() demonstration:**

```java
public class Test {
  public static void main(String[] args) {

     // generate numbers
     double d1 = Math.random();
     double d2 = Math.random();

     // display generated numbers
     System.out.println(d1);
     System.out.println(d2);
  }
}
```

📤 **Output:**

```
0.6192157696340133
0.08796048507589238
```

Each time we get different floating-point values ranging from 0.0 to 1.0.

> 📝 **Note:** There are infinite floating-point numbers that are possible between 0.0 to 1.0, but the double data type gives only up to 15 to 16 decimal point precision.

If we import the Math class statically and then we can invoke the `random()` method without calling through its class name.

**Using static import (all members):**

```java
import static java.lang.Math.*;
public class Test {
  public static void main(String[] args) {
     double d = random();
     System.out.println(d);
  }
}
```

📤 **Output:**

```
0.2644603504223617
```

The `import static java.lang.Math.*;` statement will import all static members of the Math class. But if we want to import only the `random()` method of the Math class, not another static method and variables of the Math class then we can use the `import static java.lang.Math.random;` statement. Learn more about [static import in Java](024_Static_Import_in_Java.md)

**Using static import (random only):**

```java
import static java.lang.Math.random;
public class Test {
  public static void main(String[] args) {
     System.out.println(random());
  }
}
```

---

## 2. Java Math.random() between 1 to N

By default `Math.random()` always generates numbers between 0.0 to 1.0, but if we want to get numbers within a specific range then we have to multiply the return value by the magnitude of the range.

💡 **Tip:** If we want to generate a number between 1 to 100 using the `Math.random()` then we must multiply the returned value by 100.

**Generate floating-point numbers between 1 to 100:**

```java
public class Test {
  public static void main(String[] args) {

     // generate floating-point number b/w 1 to 100
     double d1 = Math.random()*100;
     double d2 = Math.random()*100;

     // display generated floating-point numbers
     System.out.println(d1);
     System.out.println(d2);
  }
}
```

📤 **Output:**

```
10.485508101155204
81.26887023085449
```

The above program generates floating-point numbers but if we want to generate integer numbers then we must type cast the result value.

**Generate integer numbers between 1 to 100:**

```java
public class Test {
  public static void main(String[] args) {

     // generate integer number b/w 1 to 100
     int n1 = (int) (Math.random()*100);
     int n2 = (int) (Math.random()*100);

     // display generated integer numbers
     System.out.println(n1);
     System.out.println(n2);
  }
}
```

📤 **Output:**

```
20
70
```

---

## 3. Generate Numbers within a given range in Java

The above programs generate numbers between 1 to N, but if we want to generate a number between two numbers or a given range then we must follow the below expressions.

**Range formula:**

```java
int range = (max-min) + 1;
(Math.random() * range) + min;
```

**Generate a number between 100 to 1000:**

```java
public class Test {
  public static void main(String[] args) {

     // declare max and min
     int min = 100;
     int max = 1000;

     // calculate range
     int range = (max-min) + 1;

     // generate floating-point number b/w 100 to 1000
     double d1 = Math.random()*range + min;

     // generate integer number b/w 100 to 1000
     int n1 = (int)(Math.random()*range + min);

     // display result
     System.out.println(d1);
     System.out.println(n1);
  }
}
```

📤 **Output:**

```
310.60949353170884
977
```

**Generate integer numbers between 10 to 100 and 1000 to 10000:**

```java
public class Test {
  public static int randomWithRange(int min, int max) {
     int range = (max-min) + 1;
     return (int)(Math.random()*range + min);
  }

  public static void main(String[] args) {

     // generate integer number b/w 10 to 100
     System.out.println(randomWithRange(10, 100));

     // generate integer number b/w 1000 to 10000
     System.out.println(randomWithRange(1000, 10000));
  }
}
```

📤 **Output:**

```
47
1703
```

---

## 4. Other Uses of Math.random() Method in Java

We can use the `Math.random()` number to get a random element from an array.

**Get a random element from an array:**

```java
public class Test {
  public static void main(String[] args) {
     int[] arr = {12, 546, 87, 878, 44, 30, 99, 35, 80};

     // declare min, max
     int lower = 0;
     int upper = arr.length;

     // calculate range value (don't add 1)
     int range = (upper - lower);

     for(int i=0; i<5; i++) {
        // get random index
        int index = (int) (Math.random()*range + lower);

        // display array element at that index
        System.out.print(arr[index]+" ");
     }
  }
}
```

📤 **Output:**

```
35 99 878 80 546
```

---

## 5. How Math.random() is implemented

The `Math.random()` method internally creates a single new pseudorandom-number generator, exactly as if by the expression `new java.util.Random()`. This new pseudorandom-number generator is used thereafter for all calls to this method and is used nowhere else. The `nextDouble()` method of the Random class is called on this pseudorandom-number generator object.

**Internal implementation:**

```java
public static double random() {
   return RandomNumberGeneratorHolder.randomNumberGenerator.nextDouble();
}
private static final class RandomNumberGeneratorHolder {
   static final Random randomNumberGenerator = new Random();
}
```

This method is properly synchronized to allow correct use by more than one thread. However, if many threads need to generate pseudorandom numbers at a great rate, it may reduce contention for each thread to have its own pseudorandom-number generator.

As the largest double value less than 1.0 is `Math.nextDown(1.0)`, a value x in the closed range [x1,x2] where x1<=x2 may be defined by the statements.

**Closed range formula:**

```java
double f = Math.random()/Math.nextDown(1.0);
double x = x1*(1.0 - f) + x2*f;
```

```mermaid
graph LR
    A["🎲 Math.random()"] --> B["0.0 <= x < 1.0"]
    B --> C["Multiply by range"]
    C --> D["Add min offset"]
    D --> E["Cast to int if needed"]

    classDef purple fill:#A162F7,stroke:#A162F7,color:#fff
    classDef cyan fill:#00b4d8,stroke:#00b4d8,color:#fff
    classDef green fill:#28C76F,stroke:#28C76F,color:#fff
    classDef orange fill:#FF9F43,stroke:#FF9F43,color:#fff

    class A purple
    class B cyan
    class C orange
    class D orange
    class E green
```

---

## 6. Related Links

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
