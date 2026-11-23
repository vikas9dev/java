# StringBuilder toString() Java

**StringBuilder toString() Java** | The `toString()` method in the `StringBuilder` class converts a `StringBuilder` object to an immutable `String` for use with `String` class methods.

- [Syntax and Parameters](#syntax-and-parameters)
- [Java StringBuilder toString() Example](#java-stringbuilder-tostring-example)
- [How To Change StringBuilder toString In Java](#how-to-change-stringbuilder-tostring-in-java)

---

## 1. Syntax and Parameters

Compared to the Java `String` class there are only a few methods in the `StringBuilder` class. Hence to use `String` class methods for the `StringBuilder` object we have to convert the `StringBuilder` object to `String`.

The `StringBuilder` class contains the `toString()` method which can be used to convert `StringBuilder` to `String`. Once `StringBuilder` is converted to the `String` then the methods of the string class can be used to manipulate the data of the `StringBuilder` object.

```java
public String toString()
```

| Detail 🏷️ | Description 📋 |
|-----------|----------------|
| **Parameters** | Does not accept any parameters |
| **Return type** | `String` |
| **Returns** | The converted String |

---

## 2. Java StringBuilder toString() Example

In the below program we have created a `StringBuilder` object and then converted it to a string by using the `toString()` method, and displayed the value with its type.

**Basic toString() example:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuilder sb = new StringBuilder("Java Programming Language");
      System.out.println("StringBuilder: " + sb);
      System.out.println("Type: " + sb.getClass().getName());

      // calling toString() method
      String string = sb.toString();
      System.out.println("String: " + string);
      System.out.println("Type: " + string.getClass().getName());
   }
}
```

📤 **Output:**

```
StringBuilder: Java Programming Language
Type: java.lang.StringBuilder
String: Java Programming Language
Type: java.lang.String
```

Content-wise both `String` and `StringBuilder` will contain the same data. But we can get their type by using the `getClass().getName()` method which will return the type of the class.

**Using String methods after conversion:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuilder sb = new StringBuilder("KnowProgram");
      String string = sb.toString();
      System.out.println("String: " + string);
      System.out.println("Length: " + string.length());
      System.out.println("After Replacement: " + string.replace('o', '@'));
      System.out.println("Repeat: " + string.repeat(2));
   }
}
```

📤 **Output:**

```
String: KnowProgram
Length: 11
After Replacement: Kn@wPr@gram
Repeat: KnowProgramKnowProgram
```

> 💡 **Tip:** After converting with `toString()`, you gain access to all `String` class methods like `replace()`, `repeat()`, `substring()`, `toUpperCase()`, and many more.

---

## 3. How To Change StringBuilder toString In Java

Now we will convert an array of strings in the `StringBuilder` class to a string. Here we first create an array of strings and then create a `StringBuilder` object, later we append the array to the `StringBuilder` and then use the `toString()` method to get the string representation of the `StringBuilder` object.

**Array to StringBuilder to String:**

```java
public class Main {
   public static void main(String[] args) {
      String array[] = { "Welcome", "to", "Java", "Programming", "Language" };
      StringBuilder sb = new StringBuilder();
      sb.append(array[0]);
      sb.append(" " + array[1]);
      sb.append(" " + array[2]);
      sb.append(" " + array[3]);
      sb.append(" " + array[4]);

      String string = sb.toString();
      System.out.println("String: " + string);
   }
}
```

📤 **Output:**

```
String: Welcome to Java Programming Language
```

> 📝 **Note:** The `toString()` method creates a new `String` object each time it is called. If you need the string value multiple times, store it in a variable rather than calling `toString()` repeatedly.

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
- toString() Method
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
