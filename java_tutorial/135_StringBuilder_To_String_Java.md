# StringBuilder To String Java

**StringBuilder To String Java** | Converting a mutable `StringBuilder` to an immutable `String` using the `toString()` method and the `String` class constructor.

- [Conversion Methods](#conversion-methods)
- [Java StringBuilder To String Using toString() Method](#java-stringbuilder-to-string-using-tostring-method)
- [StringBuilder To String Java using String class Constructor](#stringbuilder-to-string-java-using-string-class-constructor)

---

## 1. Conversion Methods

The `StringBuilder` in Java is the mutable sequence of characters. The string is immutable which means we cannot make any changes to the string object once created; after any changes, it will create a new object. But the `StringBuilder` allows us to edit the string literal without creating a new object. The `StringBuilder` is non-synchronized and it is single-threaded.

The conversion of `StringBuilder` to `String` can be done in two ways:

- 🔄 Using the `toString()` method of the `StringBuilder` class
- 🏗️ Using the `String` class constructor

The first method we use is the [StringBuilder toString() method](139_StringBuilder_toString()_Java.md), it converts the `StringBuilder` object to `String`. The syntax of the `toString` method is: `public String toString()`

---

## 2. Java StringBuilder To String Using toString() Method

Let us see some examples for conversion of `StringBuilder` to `String` using the `toString()` method.

**Basic toString() conversion:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuilder sb = new StringBuilder("Hello, Good Morning.");
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
StringBuilder: Hello, Good Morning.
Type: java.lang.StringBuilder
String: Hello, Good Morning.
Type: java.lang.String
```

**Compact toString() example:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuilder sb = new StringBuilder("Java Programmer");
      System.out.println("String: " + sb.toString());
   }
}
```

📤 **Output:**

```
String: Java Programmer
```

---

## 3. StringBuilder To String Java using String class Constructor

We can use the `String` class constructor `String(StringBuilder builder)` to convert `StringBuilder` to `String`. This constructor creates a new string and allocates the character sequence of the `StringBuilder` class to the new string.

**Using String constructor:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuilder str = new StringBuilder("Know Program");
      String str1 = new String(str);
      System.out.println(str1);
   }
}
```

📤 **Output:**

```
Know Program
```

**Another String constructor example:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuilder str = new StringBuilder();
      str.append("Life is too short to argue just say ok and move on.");
      String str1 = new String(str);
      System.out.println(str1);
   }
}
```

📤 **Output:**

```
Life is too short to argue just say ok and move on.
```

> 💡 **Tip:** The `toString()` method is the most commonly used approach. The `String` constructor is an alternative that produces the same result. Both methods create a new `String` object from the `StringBuilder` content.

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
