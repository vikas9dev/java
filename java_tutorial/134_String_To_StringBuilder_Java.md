# String To StringBuilder Java

**String To StringBuilder Java** | How to convert a `String` to `StringBuilder` using the constructor and `append()` method for mutable string operations.

- [How To Convert String To StringBuilder In Java](#how-to-convert-string-to-stringbuilder-in-java)
- [Java String To StringBuilder Example](#java-string-to-stringbuilder-example)
- [String Array To StringBuilder](#string-array-to-stringbuilder)

---

## 1. How To Convert String To StringBuilder In Java

Previously we have seen how to convert StringBuilder to String using the [toString() method](139_StringBuilder_toString()_Java.md) and `String` class constructor.

The `StringBuilder` class allows us to modify the string literal without creating a new `StringBuilder` object. And `StringBuilder` class also contains some string manipulating methods that the `String` class doesn't have, like the [reverse() method](141_StringBuilder_reverse()_In_Java.md). To use those methods we can convert `String` to `StringBuilder` and call those methods. The `StringBuilder` was introduced in Java 5 which has made programmers' tasks easy in order to manipulate strings.

To convert `String` to `StringBuilder` object we can take the help of the `StringBuilder` class constructor:

```java
public StringBuilder(String str)
```

It constructs a `StringBuilder` initialized to the contents of the specified string. The initial capacity of the StringBuilder is 16 plus the length of the string argument.

**Basic conversion example:**

```java
public class Main {
   public static void main(String[] args) {
      String string = "Java Programming";
      System.out.println("String: " + string);
      System.out.println("Type: " + string.getClass().getName());

      // convert String to StringBuilder
      StringBuilder sb = new StringBuilder(string);
      System.out.println("StringBuilder: " + sb);
      System.out.println("Type: " + sb.getClass().getName());
   }
}
```

📤 **Output:**

```
String: Java Programming
Type: java.lang.String
StringBuilder: Java Programming
Type: java.lang.StringBuilder
```

---

## 2. Java String To StringBuilder Example

Let us see another example of `String` to `StringBuilder` conversion in Java using the `StringBuilder` class constructor. This time we will call some methods of the `StringBuilder` class for demonstration.

**Using StringBuilder methods after conversion:**

```java
public class Main {
   public static void main(String[] args) {
      String string = "Enjoy each and every moment in life.";
      StringBuilder sb = new StringBuilder(string);

      System.out.println("StringBuilder: " + sb);
      System.out.println("Capacity: " + sb.capacity());
      System.out.println("Modified: " + sb.delete(6, 15));
      System.out.println("Reverse: " + sb.reverse());
   }
}
```

📤 **Output:**

```
StringBuilder: Enjoy each and every moment in life.
Capacity: 52
Modified: Enjoy every moment in life.
Reverse: .efil ni tnemom yreve yojnE
```

---

## 3. String Array To StringBuilder

Now let us convert the string array to the `StringBuilder`. First, we will create a string array and then create a `StringBuilder` object by appending each element. The `append()` method inserts elements to the `StringBuilder`.

**Converting String array to StringBuilder:**

```java
public class Main {
   public static void main(String[] args) {
      String string1[] =
        { "Enjoy", " each", " and", " every", " moment", " in", " life" };
      StringBuilder sb = new StringBuilder();
      for (String string : string1) {
         sb.append(string);
      }
      System.out.println(sb.toString());
   }
}
```

📤 **Output:**

```
Enjoy each and every moment in life
```

> 💡 **Tip:** Use the `StringBuilder` constructor for a single `String` conversion, and use the `append()` method when you need to build a `StringBuilder` from multiple strings or an array.

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
