# String isEmpty() Java with Examples

**String isEmpty() Java** | In the String class of Java, the `isEmpty()` method is given to check whether the String is empty or not. If the string is empty then this method returns `true` else it returns `false`. This method was introduced in **Java 1.6**.

- [isEmpty() Method Examples](#isempty-method-examples)
- [Scanner Input Example](#scanner-input-example)
- [MCQ on String isEmpty() Java](#mcq-on-string-isempty-java)

**Internal implementation of the Java String isEmpty() method:**

```java
public boolean isEmpty() {
   return value.length == 0;
}
```

| Detail 📋 | Description 🔤 |
|-----------|---------------|
| **Method Declaration** | `public boolean isEmpty()` |
| **Return - true** | ✅ If the length of the string is 0 |
| **Return - false** | ❌️ If the length of the string is greater than 0 |
| **Since** | Java 1.6 |

> 📝 **Note:** This method returns `true` if the String doesn't have a character, and it returns `false` if at least 1 character is available in this string object.

Also see: [isBlank() method in Java String class](124_String_isBlank()_Java_with_Examples.md), isBlank() vs isEmpty() in Java String, Different ways to check if String is Empty in Java

---

## 1. isEmpty() Method Examples

**Program to demonstrate String isEmpty() Java:**

```java
public class Test {

   public static void main(String[] args) {

      String s1 = "";
      System.out.println(s1.isEmpty());

      String s2 = " ";
      System.out.println(s2.isEmpty());

      String s3 = "java";
      System.out.println(s3.isEmpty());

      String s4 = new String();
      System.out.println(s4.isEmpty());

      String s5 = new String("");
      System.out.println(s5.isEmpty());

      String s6 = new String(" ");
      System.out.println(s6.isEmpty());

      String s7 = new String("java");
      System.out.println(s7.isEmpty());
   }
}
```

📤 **Output:**

```
true
false
false
true
true
false
false
```

In the string literal `""` there is no valid character, it contains only `'\0'`, and the length of this string literal is 0 therefore `isEmpty()` method returns `true`. But the string literal `" "` contains one space that is a valid character hence the length of this string literal is 1 and the `isEmpty()` method returns `false`.

| Value 🔤 | Result ✅ |
|----------|----------|
| `""` | `true` |
| `" "` | `false` |
| `"java"` | `false` |
| `new String()` | `true` |
| `new String("")` | `true` |
| `new String(" ")` | `false` |
| `new String("java")` | `false` |

---

## 2. Scanner Input Example

Let us demonstrate Java String `isEmpty()` method with one more example. This time, we will get input from the end user through the `Scanner` class.

**User input example:**

```java
import java.util.Scanner;

public class Test1 {

   public static void main(String[] args) {

      Scanner scan = new Scanner(System.in);

      System.out.println("Enter three Strings in three lines,");
      String s1 = scan.nextLine(); // directly press enter key
      String s2 = scan.nextLine(); // enter blank spaces or tabs
      String s3 = scan.nextLine(); // enter normal string

      System.out.println(s1.isEmpty() + " " + s1.length());
      System.out.println(s2.isEmpty() + " " + s2.length());
      System.out.println(s3.isEmpty() + " " + s3.length());
   }
}
```

📤 **Output:**

```
Enter three Strings in three lines,
->(Here directly enter key was pressed)
->(Here one space was entered)
Know Program
true 0
false 1
false 12
```

> 💡 **Tip:** In this program, the string `s1` is an empty string and it is similar to `String s5 = new String("");` from the previous program. Notice that it is different from `String s4 = new String();`

---

## 3. MCQ on String isEmpty() Java

Based on the above-discussed points find the valid answers for the given questions on String `isEmpty()` Java.

**Q1) Find the output of the below program.**

```java
package com.kp.test;
public class Q1 {

   public static String s1;

   public static void main(String[] args) {
      System.out.println(s1.isEmpty());
   }
}
```

- a) true
- b) false
- c) Compile time error
- d) NullPointerException

> 🔑 **Answer:** d) `NullPointerException`
>
> Explanation: If the string is not initialized then we can't perform any operation on it because there is no String object available. Due to this reason, we will get `NullPointerException`: Cannot invoke `String.isEmpty()` because `"com.kp.test.Test.s1"` is null.

---

**Q2) Find the output of the below program.**

```java
package com.kp.test;
public class Q2 {
   public static void main(String[] args) {
      String s2;
      System.out.println(s2.isEmpty());
   }
}
```

- a) true
- b) false
- c) Compile time error
- d) NullPointerException

> 🔑 **Answer:** c) Compile time error
>
> Explanation: In this program, before running, compile time itself gets an error because the local variable is not initialized. All the local variables must be initialized before using them. Hence we get a compile-time error: variable `s2` might not have been initialized.

---

**Q3) Find the output of the below program.**

```java
package com.kp.test;
public class Q3 {
   public static void main(String[] args) {
      String s3 = null;
      System.out.println(s3.isEmpty());
   }
}
```

- a) true
- b) false
- c) Compile time error
- d) NullPointerException

> 🔑 **Answer:** d) `NullPointerException`
>
> Explanation: The string is not initialized, and we are trying to call the `isEmpty()` method with `null` reference. Due to this reason, we will get a runtime error: `java.lang.NullPointerException`.

---

**Q4) Find the output of the below program.**

```java
package com.kp.test;
public class Q4 {
   public static void main(String[] args) {
      String s4 = "null";
      System.out.println(s4.isEmpty());
   }
}
```

- a) true
- b) false
- c) Compile time error
- d) NullPointerException

> 🔑 **Answer:** b) false
>
> Explanation: In this program, `"null"` is a String literal with characters 'n', 'u', 'l', 'l'. It is a simple string like "Hi", "Hello". Hence `s4.isEmpty()` gives result as `false`.

---

> ⚠️ **Caution:** The `null` and `"null"` are completely different things. The string `s3` has `null`, it is a reference that can be used for initializing any reference variable. The compiler will not give any error if the string is not `null` but JVM will give an exception when we try to access string data. The string reference is `null` so JVM gives an exception. But `"null"` is a String literal with 4 characters 'n', 'u', 'l', 'l'. It is a simple string literal like "Hi", "Hello", "java", etc. Hence `s4.isEmpty()` gives the result as `false`.

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

**Java Tutorial**

**[String Class Methods](097_String_Class_Methods_In_Java.md)**
- charAt() Method
- codePoints() Method
- [compareTo() Method](106_String_compareTo()_Java.md)
- [compareToIgnoreCase()](107_String_compareToIgnoreCase()_Java.md)
- [concat() Method](113_Concat_Strings_in_Java.md)
- [contains() Method](116_String_contains()_Method_in_Java.md)
- equals() Method
- [equalsIgnoreCase()](105_String_equalsIgnoreCase()_Java.md)
- format() Method
- getBytes() Method
- hashCode() Method
- indent() Method
- [indexOf() Method](110_Java_String_indexOf()_Method.md)
- intern() Method
- [isBlank() Method](124_String_isBlank()_Java_with_Examples.md)
- isEmpty() Method
- isBlank() vs isEmpty()
- [join() Method](098_String_join()_In_Java.md)
- [lastIndexOf() Method](111_String_lastIndexOf()_in_Java.md)
- [length() Method](099_How_to_Find_Length_of_String_in_Java.md)
- matches() Method
- repeat() Method
- [replace() Method](114_Replace()_In_String_Java.md)
- [replaceAll() Method](118_String_replaceAll()_Java.md)
- replaceFirst() Method
- replace() vs replaceAll()
- [split() Method](119_Split()_Method_In_Java.md)
- startsWith() & endsWith()
- strip() & stripLeading()
- [substring() Method](112_Substring_Method_In_Java.md)
- toCharArray() Method
- [toLowerCase() Method](120_Java_String_to_Lowercase.md)
- [toString() Method](126_String_toString()_Java.md)
- toUpperCase() Method
- [trim() Method](122_Trim()_in_Java_String.md)
- [trim() vs strip()](093_Java_String_trim()_Vs_strip().md)
- valueOf() Method
