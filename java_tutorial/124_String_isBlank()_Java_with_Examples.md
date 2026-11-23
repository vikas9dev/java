# String isBlank() Java with Examples

**String isBlank() Java with Examples** | In the String class of Java, the `isBlank()` method is given to check whether the given String is blank or not. A string is treated as blank if it doesn't contain any character or contains only blank spaces.

- [isBlank() Method Details](#isblank-method-details)
- [isBlank() Demonstration with Scanner](#isblank-demonstration-with-scanner)
- [MCQ on String isBlank() Java Method](#mcq-on-string-isblank-java-method)

---

## 1. isBlank() Method Details

| Detail 📋 | Description 📝 |
|-----------|---------------|
| **Method Signature** | `public boolean isBlank()` |
| **Since** | Java 11 |
| **Returns `true`** | If the string is empty or contains only whitespace (space, tab) |
| **Returns `false`** | If the string is not empty and contains valid characters except whitespace |

Also see: isBlank() vs isEmpty() in Java String, Different ways to check if String is Empty in Java

**Internal implementation of `isBlank()` method:**

```java
public boolean isBlank() {
   return indexOfNonWhitespace() == length();
}
```

**Program to demonstrate `isBlank()` method:**

```java
public class Test {
   public static void main(String[] args) {
      String s1 = "";
      System.out.println(s1.isBlank());

      String s2 = " ";
      System.out.println(s2.isBlank());

      String s3 = "Program";
      System.out.println(s3.isBlank());

      String s4 = new String();
      System.out.println(s4.isBlank());

      String s5 = new String("");
      System.out.println(s5.isBlank());

      String s6 = new String(" ");
      System.out.println(s6.isBlank());

      String s7 = new String("Program");
      System.out.println(s7.isBlank());
   }
}
```

📤 **Output:**

```
true
true
false
true
true
true
false
```

- 📖 The first string literal `""` doesn't contain any valid characters, and contains only `'\0'` therefore the length of this string is zero (0). Hence `s1.isBlank()` method returns `true`.
- 📖 The string literal `" "` contains one space, and the length of the string is 1. But the `isBlank()` method returns `true` when the string contains only whitespace.
- 📖 The string literal `"Program"` contains 7 valid characters. Since the length of the string is greater than 0 and doesn't contain only whitespace, `s3.isBlank()` method returns `false`.

| Value 🏷️ | `isBlank()` Result ✅/❌️ |
|----------|----------------------|
| `""` | ✅ `true` |
| `" "` | ✅ `true` |
| `"Program"` | ❌️ `false` |
| `new String()` | ✅ `true` |
| `new String("")` | ✅ `true` |
| `new String(" ")` | ✅ `true` |
| `new String("Program")` | ❌️ `false` |

---

## 2. isBlank() Demonstration with Scanner

Let us see another program to demonstrate `isBlank()` method by taking String input values from the end-user through the Scanner class.

**Scanner-based `isBlank()` example:**

```java
import java.util.Scanner;

public class Test {
   public static void main(String[] args) {

      Scanner scan = new Scanner(System.in);

      System.out.println("Enter three Strings in three lines,");
      String s1 = scan.nextLine(); // directly press enter key
      String s2 = scan.nextLine(); // enter blank spaces or tabs
      String s3 = scan.nextLine(); // enter normal string

      System.out.println(s1.isBlank() + " " + s1.length());
      System.out.println(s2.isBlank() + " " + s2.length());
      System.out.println(s3.isBlank() + " " + s3.length());
   }
}
```

📤 **Output:**

```
Enter three Strings in three lines,
->(Here directly enter key was pressed)
->(Here one space was entered)
KnowProgram
true 0
true 1
false 11
```

In this program, the string `s1` is an empty string and it is similar to `new String("")`. Notice that it is different from `new String()`.

---

## 3. MCQ on String isBlank() Java Method

Based on the above-discussed points let us solve some quick questions on the `isBlank()` method. Find the outputs of the below Java programs.

**Q1) Find the output of the below Java program.**

```java
package com.kp.test;
public class Q1 {
   public static void main(String[] args) {
      String s1 = "     "; // five spaces
      System.out.println(s1.isBlank());
   }
}
```

a) true
b) false
c) Compile time error
d) NullPointerException

> 🔑 **Answer:** a) `true` -- The string literal is a valid string of length 5, but it contains only whitespaces, therefore, the `isBlank()` method returns `true`.

---

**Q2) Find the output of the below Java program.**

```java
package com.kp.test;
public class Q2 {
   public static void main(String[] args) {
      String s2 = "Know Program";
      System.out.println(s2.isBlank());
   }
}
```

a) true
b) false
c) Compile time error
d) NullPointerException

> 🔑 **Answer:** b) `false` -- The string literal `"Know Program"` is a valid string of length 12, and doesn't contain only white spaces therefore `isBlank()` method returns `false`. Note that if any string literal contains spaces with other characters then `isBlank()` will not return `true`, but if string literal contains only white spaces then it will return `true`.

---

**Q3) Find the output of the below Java program.**

```java
package com.kp.test;
public class Q3 {
   public static String s3;
   public static void main(String[] args) {
      System.out.println(s3.isBlank());
   }
}
```

a) true
b) false
c) Compile time error
d) NullPointerException

> 🔑 **Answer:** d) `NullPointerException` -- If the string is not initialized then we can't perform any operation on it because there is no String object available. We will get `NullPointerException` at runtime.

---

**Q4) Find the output of the below Java program.**

```java
package com.kp.test;
public class Q4 {
   public static void main(String[] args) {
      String s4;
      System.out.println(s4.isBlank());
   }
}
```

a) true
b) false
c) Compile time error
d) NullPointerException

> 🔑 **Answer:** c) Compile time error -- In this program, the local variable is not initialized before use. All local variables must be initialized before using them. Hence we get a compile-time error: `variable s4 might not have been initialized`.

---

**Q5) Find the output of the below Java program.**

```java
package com.kp.test;
public class Q5 {
   public static void main(String[] args) {
      String s5 = null;
      System.out.println(s5.isBlank());
   }
}
```

a) true
b) false
c) Compile time error
d) NullPointerException

> 🔑 **Answer:** d) `NullPointerException` -- The string is initialized with `null`, and we are trying to call the `isBlank()` method with `null` reference. We will get a runtime error: `java.lang.NullPointerException`.

---

**Q6) Find the output of the below Java program.**

```java
package com.kp.test;
public class Q6 {
   public static void main(String[] args) {
      String s6 = "null";
      System.out.println(s6.isBlank());
   }
}
```

a) true
b) false
c) Compile time error
d) NullPointerException

> 🔑 **Answer:** b) `false` -- In this program, `"null"` is a String literal with characters 'n', 'u', 'l', 'l'. It is a simple string like `"java"`, `"Know Program"`. Hence `s6.isBlank()` gives the result as `false`.

---

> ⚠️ **Caution:** The `null` keyword and `"null"` string literal are completely different things. `null` is a reference that can be used for initializing any reference variable. The compiler will not give any error if the string is `null` but JVM will give an exception when we try to access string data. But `"null"` is a String literal with 4 characters 'n', 'u', 'l', 'l'. It is a simple string literal like `"Java"`, `"program"`, `"learn"`, etc.

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

**Java Tutorial**

**[String Class Methods](097_String_Class_Methods_In_Java.md)**
