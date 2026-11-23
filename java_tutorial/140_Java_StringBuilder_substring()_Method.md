# Java StringBuilder substring() Method

**Java StringBuilder substring() Method** | The `substring()` method returns a portion of the `StringBuilder` content from a given index, with two variations for flexible extraction.

- [Syntax and Parameters](#syntax-and-parameters)
- [Java StringBuilder substring() Method Example](#java-stringbuilder-substring-method-example)
- [How To Get Substring From StringBuilder In Java](#how-to-get-substring-from-stringbuilder-in-java)
- [How To See If StringBuilder Contains A Substring In Java](#how-to-see-if-stringbuilder-contains-a-substring-in-java)
- [Delete Substring StringBuilder Java](#delete-substring-stringbuilder-java)

---

## 1. Syntax and Parameters

The substring is a part of the string. For example, if the string is "Pen is mightier than the sword" then the words "than the" would be a substring. In the Java `StringBuilder` class, we have a method called `substring()` which returns the substring from the given index and extends till the end of the string or character sequence.

There are two variations of the `substring()` method in the `StringBuilder` class:

1. `public String substring(int start)`
2. `public String substring(int start, int end)`

| Parameter 🏷️ | Description 📋 |
|--------------|----------------|
| **`start`** | From which index to start (inclusive) |
| **`end`** | The ending index (exclusive) |
| **Return type** | `String` |
| **Returns** | The substring from the specified index |

**Exceptions:**

- 🚨 The `substring(int start)` method throws StringIndexOutOfBoundsException if the parameter `start` is less than 0 or more than the length of the string
- 🚨 The `substring(int start, int end)` method throws `StringIndexOutOfBoundsException` if start or end is negative or greater than `length()`, or start is greater than end

---

## 2. Java StringBuilder substring() Method Example

Let us see an example of the `public String substring(int start)` method. The start parameter is inclusive.

**substring(int start) example:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuilder string = new StringBuilder("Hello World! Java Programming Langauge");
      System.out.println("String = " + string);
      System.out.println("SubSequence = " + string.substring(13));
   }
}
```

📤 **Output:**

```
String = Hello World! Java Programming Langauge
SubSequence = Java Programming Langauge
```

Let us see an example of the `public String substring(int start, int end)` method. The start parameter is inclusive, but the end parameter is exclusive.

**substring(int start, int end) example:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuilder string = new StringBuilder("Hello World! Java Programming Langauge");
      System.out.println("String = " + string);
      System.out.println("SubSequence = " + string.substring(13, 18));
   }
}
```

📤 **Output:**

```
String = Hello World! Java Programming Langauge
SubSequence = Java Programming Langauge
```

---

## 3. How To Get Substring From StringBuilder In Java

In the below program, the string is "All is well" from this string we have extracted the substring "is well" which starts from index 4.

**Extracting a substring:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuilder string = new StringBuilder("All is well");
      System.out.println("String = " + string);
      System.out.println("SubSequence = " + string.substring(4));
   }
}
```

📤 **Output:**

```
String = All is well
SubSequence = is well
```

---

## 4. How To See If StringBuilder Contains A Substring In Java

To check whether the substring is present in the given `StringBuilder` or not we can use the [contains() method of the String class](116_String_contains()_Method_in_Java.md). The `contains()` method will not work for the `StringBuilder` class hence we have to convert the `StringBuilder` to the string. Then we can use `contains()` method on the string object. This `contains()` method checks for the substring in the string; if present then it returns `true`, else it returns `false`.

**Checking if substring exists:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuilder sb = new StringBuilder("All is well");
      System.out.println("StringBuilder  = " + sb);

      String string = sb.toString();
      System.out.println("StringBuilder contains \"is\"?: " + string.contains("is"));
   }
}
```

📤 **Output:**

```
StringBuilder = All is well
StringBuilder contains "is"?: true
```

> 💡 **Tip:** Always convert `StringBuilder` to `String` using `toString()` before using `String`-specific methods like `contains()`, `matches()`, or `split()`.

---

## 5. Delete Substring StringBuilder Java

Let us see how to delete a substring from `StringBuilder` in Java. The `delete()` method of the `StringBuilder` class removes the substring at the specified index. The syntax for the delete method is: `public String delete(int start, int end)`

**Deleting a substring:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuilder string = new StringBuilder("All is well");
      System.out.println("StringBuilder before deleting the substring: "
                         + string);
      System.out.println("StringBuilder after deleting the subtring: "
                         + string.delete(3, 6));
   }
}
```

📤 **Output:**

```
StringBuilder before deleting the substring: All is well
StringBuilder after deleting the subtring: All well
```

> ⚠️ **Caution:** The `delete()` method modifies the original `StringBuilder` object. If you need to preserve the original, create a copy before calling `delete()`.

---

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

**Java Tutorial**

- [Import StringBuffer Class](132_Import_StringBuffer_In_Java.md)
- [StringBuffer vs StringBuilder](133_When_To_Use_StringBuffer_And_StringBuilder_In_Java.md)
- String To StringBuilder
- StringBuilder To String
- [String To StringBuffer](136_Java_String_To_StringBuffer.md)
- [StringBuffer To String](136_Java_String_To_StringBuffer.md)

**StringBuilder Methods**
- [toString() Method](139_StringBuilder_toString()_Java.md)
- substring() Method
- [reverse() Method](141_StringBuilder_reverse()_In_Java.md)
- replace() Method
- length() Method
- indexOf() Method
- insert() Method
- append() Method
- capacity() Method
- charAt() Method

**StringBuffer Methods**
- append() Method
- insert() Method
- length() Method
- reverse() Method
