# Java Predicate Functional Interface

**Java Predicate Functional Interface** | The `java.util.function` contains many pre-defined functional interfaces. Some examples of pre-defined functional interfaces are Predicate, Function, Consumer, and Supplier.

- [Java Predicate Functional Interface Examples](#java-predicate-functional-interface-examples)
- [Java Predicate - and(), or(), negate() Methods](#java-predicate--and-or-negate-methods)
- [Java Predicate - isEqual() Method](#java-predicate--isequal-method)
- [Java Predicate - not() Method](#java-predicate--not-method)

---

In mathematics, Predicate is a normal function that returns a boolean value based on some condition. Predicate functions are functions that return a single TRUE or FALSE. We use predicate functions to check if your input meets some conditions. For example, `is.character()` is a predicate function that returns TRUE if its input is of type character and FALSE otherwise.

Java contains Predicate pre-defined functional interface which can be used to check some conditions.

- 🔍 Predicate is a function with a single argument and returns a boolean value.
- 📦 To implement predicate functions in Java, Oracle people introduced the Predicate interface (`Predicate<T>`) in the 1.8 version.
- 📋 Predicate interface present in the `java.util.function` package.
- ⚡ It's a [functional interface](212_Functional_Interface_In_Java.md) and contains one abstract `test()` method which returns a boolean value.

**Predicate interface definition:**

```java
public interface Predicate<T> {
  boolean test(T t);
  default Predicate<T> and(Predicate<? super T> other) { }
  default Predicate<T> negate() { }
  default Predicate<T> or(Predicate<? super T> other) { }
  static <T> Predicate<T> isEqual(Object targetRef) { }
  static <T> Predicate<T> not(Predicate<? super T> target) { }
}
```

As the predicate is a [functional interface](212_Functional_Interface_In_Java.md) (because it contains exactly one abstract method) and hence it can refer to [lambda expression](213_Lambda_Expression_in_Java.md). Except for the `test()` method Predicate also contains some default and static methods. Let us first see some examples using the `test()` method. Also see: Java-8 Predicate MCQ

---

## 1. Java Predicate Functional Interface Examples

**Ex-1: Write a predicate to check whether the given integer is greater than 20 or not.**

**Normal method:**

```java
public boolean test(Integer I) {
   if (I > 20) {
      return true;
   }
   else {
      return false;
   }
}
```

**Using lambda expression it can be written as:**

```java
(Integer I) -> {
   if(I > 20)
      return true;
   else
      return false;
};
```

**It can be further simplified as:**

```java
I -> (I > 20);
```

**Complete example:**

```java
import java.util.function.Predicate;

public class Test {
    public static void main(String[] args) {
        Predicate<Integer> pre = i -> i > 20;
        System.out.println(pre.test(10));
        System.out.println(pre.test(20));
        System.out.println(pre.test(30));
    }
}
```

📤 **Output:**

```
false
false
true
```

**Example-2: Write a predicate to check the length of the given string is greater than 6 or not.**

```java
import java.util.function.Predicate;

public class Test {
    public static void main(String[] args) {
        Predicate<String> pre = s -> (s.length() > 6);
        System.out.println(pre.test("Java"));
        System.out.println(pre.test("Hello World!"));
        System.out.println(pre.test("Know Program"));
    }
}
```

📤 **Output:**

```
false
true
true
```

**Example-3: Write a predicate to check whether the given collection is empty or not.**

```java
import java.util.ArrayList;
import java.util.Collection;
import java.util.LinkedList;
import java.util.function.Predicate;

public class Test {
    public static void main(String[] args) {
        Predicate<Collection> pre = c -> c.isEmpty();
        System.out.println(pre.test(new ArrayList<>()));
        LinkedList<Integer> linkedList = new LinkedList<Integer>();
        linkedList.add(10);
        System.out.println(pre.test(linkedList));
    }
}
```

📤 **Output:**

```
true
false
```

**Example-4: Program to display names starts with 'K' by using Predicate.**

```java
import java.util.function.Predicate;

public class Test {
    public static void main(String[] args) {
        String[] names = { "Hello", "Know", "Program", "Java", "K++" };
        Predicate<String> pre = name -> name.charAt(0) == 'K';
        for (String string : names) {
            System.out.println(string + ": " + pre.test(string));
        }
    }
}
```

📤 **Output:**

```
Hello: false
Know: true
Program: false
Java: false
K++: true
```

**Example-5: Predicate Example to remove null values and empty strings from the given list:**

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.function.Predicate;

public class Test {
    public static void main(String[] args) {
        List<String> strings =
         Arrays.asList("Hello", null, "", "Hello", null, "Program", "", null, "Java");
        Predicate<String> pre = s -> s != null && !s.isEmpty();

        List<String> newList = new ArrayList<>();
        for (String string : strings) {
            if (pre.test(string)) {
                newList.add(string);
            }
        }
        System.out.println("Original List: " + strings);
        System.out.println("New List: " + newList);
    }
}
```

📤 **Output:**

```
Original List: [Hello, null, , Hello, null, Program, , null, Java]
New List: [Hello, Hello, Program, Java]
```

**Example-6: Program for Basic User Authentication by using Predicate**

**User class:**

```java
class User {

    private String name;
    private String pwd;

    public User(String name, String pwd) {
        this.name = name;
        this.pwd = pwd;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getPwd() {
        return pwd;
    }

    public void setPwd(String pwd) {
        this.pwd = pwd;
    }
}
```

**Authentication test:**

```java
import java.util.Scanner;
import java.util.function.Predicate;

public class Test {
    public static void main(String[] args) {

        // read user name and password from UI/form
        Scanner scan = new Scanner(System.in);
        System.out.print("Enter username: ");
        String username = scan.next();
        System.out.print("Enter password: ");
        String pwd = scan.next();
        scan.close();

        // create user
        User u1 = new User(username, pwd);

        String originalUser = "Amelia";
        String originalPWD = "password";

        Predicate<User> pre = user ->
                user.getName().equals(originalUser) &&
                user.getPwd().equals(originalPWD);

        if (pre.test(u1)) {
            System.out.println("Valid");
        } else {
            System.out.println("Invalid");
        }
    }
}
```

📤 **Output:**

```
Enter username: Amelia
Enter password: password
Valid

Enter username: James
Enter password: abcd
Invalid
```

---

## 2. Java Predicate - and(), or(), negate() Methods

It's possible to join predicates into a single predicate by using the following methods.

- 🔗 **`and()`**
- 🔀 **`or()`**
- 🔄 **`negate()`**

These are exactly the same as logical AND, OR, and complement operators. These 3 methods are defined as the **default method** in the Predicate interface. Assume we have two Predicates:

1. `p1` - Predicate to find a given number is greater than 10.
2. `p2` - Predicate to find a given number is an even number or not.

- 🔄 **`negate():`** It checks negation (exactly opposite) of `test()`.
  - `p1.negate()` - find the number is less than 10 or not.
  - `p2.negate()` - find whether the given number is odd or not.

- 🔗 **`and():`** To check 2 predicates (both) conditions.
  - `p1.and(p2)` - It will check whether number > 10 and number is even or not.

- 🔀 **`or():`** To check 1st predicate or 2nd predicate condition.
  - `p1.or(p2)` - It will check whether number > 10 or number is even or not.

**Complete example with and(), or(), negate():**

```java
import java.util.function.Predicate;

public class Test {
    public static void main(String[] args) {
        int[] array = { 0, 5, 10, 15, 20, 25, 30 };

        Predicate<Integer> p1 = i -> i > 10;
        Predicate<Integer> p2 = i -> i % 2 == 0;

        System.out.println("The Numbers Greater Than 10:");
        m1(p1, array);

        System.out.println("\nThe Even Numbers Are:");
        m1(p2, array);

        System.out.println("\nThe Numbers Not Greater Than 10:");
        m1(p1.negate(), array);

        System.out.println("\nThe Odd Numbers Are:");
        m1(p2.negate(), array);

        System.out.println("\nThe Numbers Greater Than 10 And Even Are:");
        m1(p1.and(p2), array);

        System.out.println("\nThe Numbers Greater Than 10 OR Even:");
        m1(p1.or(p2), array);

        System.out.println("\nThe Numbers Greater Than 10 And Odd Are:");
        m1(p1.and(p2.negate()), array);
    }

    public static void m1(Predicate<Integer> p, int[] arr) {
        for (int a : arr) {
            if (p.test(a)) {
                System.out.print(a + " ");
            }
        }
    }
}
```

📤 **Output:**

```
The Numbers Greater Than 10:
15 20 25 30
The Even Numbers Are:
0 10 20 30
The Numbers Not Greater Than 10:
0 5 10
The Odd Numbers Are:
5 15 25
The Numbers Greater Than 10 And Even Are:
20 30
The Numbers Greater Than 10 OR Even:
0 10 15 20 25 30
The Numbers Greater Than 10 And Odd Are:
15 25
```

---

## 3. Java Predicate - isEqual() Method

**The `Predicate.isEqual()` checks whether the given value is the same as Predicate or not.**

```java
import java.util.function.Predicate;

public class Test {
    public static void main(String[] args) {
        Predicate<String> p = Predicate.isEqual("KnowProgram");
        System.out.println(p.test("Software")); // false
        System.out.println(p.test("KnowProgram")); // true
    }
}
```

📤 **Output:**

```
false
true
```

---

## 4. Java Predicate - not() Method

**The `Predicate.not()` returns a predicate that is the negation of the supplied predicate. This is accomplished by returning the result of the calling `target.negate()`.**

```java
import java.util.function.Predicate;

public class Test {
    public static void main(String[] args) {
        Predicate<Integer> p1 = i -> i % 2 == 0;
        Predicate<Integer> p2 = Predicate.not(p1);
        System.out.println(p1.test(10));
        System.out.println(p1.test(11));
        System.out.println(p2.test(10));
        System.out.println(p2.test(11));
    }
}
```

📤 **Output:**

```
true
false
false
true
```
