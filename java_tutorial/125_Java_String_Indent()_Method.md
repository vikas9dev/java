# Java String Indent() Method

**Java String Indent() Method** | This tutorial explains the `indent()` method available in the Java String class. The `indent()` method is introduced in JDK 12 in the [java.lang.String class](097_String_Class_Methods_In_Java.md). It is helpful to adjust the indentation of the string or to add or remove white spaces to the string.

- [Java String Indent() Method Example](#java-string-indent-method-example)
- [Adding Indent In String Java](#adding-indent-in-string-java)

---

## 1. Java String Indent() Method Example

| Detail 📋 | Description 📝 |
|-----------|---------------|
| **Method Signature** | `public String indent(int n)` |
| **Parameter** | `n` - integer value for indentation |
| **Return Type** | `String` |
| **Returns** | String after indentation |
| **Since** | Java 12 |

The `indent()` method adjusts the indentation of each line of this string based on the value of `n`, and normalizes line termination characters. This string is conceptually separated into lines using `String.lines()`. **Each line is then adjusted as described below and then suffixed with a line feed `"\n"` (U+000A).** The resulting lines are then concatenated and returned.

| Condition 🏷️ | Behavior 📝 |
|-------------|------------|
| **n > 0** | `n` spaces (U+0020) are **inserted at the beginning** of each line |
| **n < 0** | Up to `n` whitespace characters are **removed from the beginning** of each line |
| **n == 0** | The line remains **unchanged**, but line terminators are still normalized |

> 📝 **Note:** If `n < 0` and a given line does not contain sufficient whitespace, then all leading whitespace characters are removed. Each whitespace character is treated as a single character. In particular, the tab character `"\t"` (U+0009) is considered a single character; it is not expanded.

**Basic `indent()` example:**

```java
public class Main {
   public static void main(String args[]) {
      String string =
         "Learn Java Programming - knowprogram.com.";
      System.out.println(string);
      System.out.println("Input String length: "
              + string.length());

      String string1 = string.indent(5);
      System.out.println(string1);
      System.out.println("New String length: "
              + string1.length());

      String string2 = string.indent(0);
      System.out.println(string2);
      System.out.println("New String length: "
              + string2.length());

      String string3 = string.indent(-3);
      System.out.println(string3);
      System.out.println("New String length: "
              + string3.length());
   }
}
```

📤 **Output:**

```
Learn Java Programming - knowprogram.com.
Input String length: 41
     Learn Java Programming - knowprogram.com.

New String length: 47
Learn Java Programming - knowprogram.com.

New String length: 42
Learn Java Programming - knowprogram.com.

New String length: 42
```

- 🔧 In `string1` we have used `string.indent(5)` where 5 > 0 therefore 5 spaces are added to the beginning of the line, and the line ends with a newline character.
- 🔧 In `string2` we have used `indent(0)` so it only added a newline character at the end of the line.
- 🔧 In `string3` we have used `indent(-3)` but the string doesn't have whitespace at the beginning of the line, therefore, it produces the same result as calling `indent(0)` on the given string. If the string contains whitespace at the beginning of the line, it will remove 3 whitespace characters from the beginning of each line.

---

## 2. Adding Indent In String Java

Let us see a few more examples of the String `indent()` method in Java.

**Multi-line `indent()` example:**

```java
public class Main {
   public static void main(String args[]) {
      String string = "     Hello World    \n"
                    + "     Know Program     ";
      System.out.println("Input String length: "
                    + string.length());
      System.out.println(string);

      String string1 = string.indent(3);
      System.out.println("String1 length: "
                    + string1.length());
      System.out.println(string1);

      String string2 = string.indent(0);
      System.out.println("String2 length: "
                    + string2.length());
      System.out.println(string2);

      String string3 = string.indent(-5);
      System.out.println("String3 length: "
                    + string3.length());
      System.out.println(string3);
   }
}
```

📤 **Output:**

```
Input String length: 43
     Hello World
     Know Program
String1 length: 50
        Hello World
        Know Program

String2 length: 44
     Hello World
     Know Program

String3 length: 34
Hello World
Know Program
```

> 💡 **Tip:** The `indent()` method is particularly useful when working with multi-line text blocks (introduced in Java 13) to programmatically adjust indentation levels for formatted output.

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

**Java Tutorial**

**[String Class Methods](097_String_Class_Methods_In_Java.md)**
