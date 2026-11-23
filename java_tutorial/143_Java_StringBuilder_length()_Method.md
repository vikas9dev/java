# Java StringBuilder length() Method

**Java StringBuilder length() Method** | The `length()` method returns the number of characters in a `StringBuilder` object, useful for counting characters in sentences or strings.

- [Syntax and Parameters](#syntax-and-parameters)
- [Java StringBuilder length() Method Example](#java-stringbuilder-length-method-example)
- [StringBuilder Length Java Example](#stringbuilder-length-java-example)
- [Java StringBuilder Length Example](#java-stringbuilder-length-example)
- [NullPointerException with length()](#nullpointerexception-with-length)

---

## 1. Syntax and Parameters

In some situations, we need to find the length of a given sentence. Instead of counting each letter manually, Java provides the `length()` method to count the number of characters in the `StringBuilder` object.

```java
public int length()
```

| Detail 🏷️ | Description 📋 |
|-----------|----------------|
| **Parameters** | Does not take any parameters |
| **Return type** | `int` |
| **Returns** | The length of the string |

🛠️ **Examples:**

- 🔤 String: `"Doll"` → Length: `4`
- 🔤 String: `"Paper"` → Length: `5`

---

## 2. Java StringBuilder length() Method Example

We have passed the sentence to the `StringBuilder` constructor. Then called the `length()` method and stored the result in the variable called `len` and printed the `len` to see the result.

**Basic length example:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuilder string = new StringBuilder("Papaya Garden");
      System.out.println("StringBuilder = " + string);
      int len = string.length();
      System.out.println("Length = " + len);
   }
}
```

📤 **Output:**

```
StringBuilder = Papaya Garden
Length = 13
```

---

## 3. StringBuilder Length Java Example

Let us see another example of the `StringBuilder` `length()` method in Java. We will follow the same approach: passing a sentence to the `StringBuilder` class, converting it to a string using the `toString()` method, and storing the length in the `len` variable.

**Another length example:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuilder string = new StringBuilder("God is Great");
      System.out.println("String = " + string.toString());
      int len = string.length();
      System.out.println("Length of String = " + len);
   }
}
```

📤 **Output:**

```
String = God is Great
Length of String = 12
```

---

## 4. Java StringBuilder Length Example

If the given `StringBuilder` object is empty then the `length()` method will return 0.

**Empty StringBuilder length:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuilder string = new StringBuilder("Passwords");
      System.out.println("Length = " + string.length());
      string = new StringBuilder("");
      System.out.println("Length = " + string.length());
   }
}
```

📤 **Output:**

```
Length = 9
Length = 0
```

---

## 5. NullPointerException with length()

If the given `StringBuilder` object is `null` then on calling the `length()` method we will get `NullPointerException`.

**Null StringBuilder example:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuilder string = null;
      System.out.println("Length = " + string.length());
   }
}
```

📤 **Output:**

```
Exception in thread "main" java.lang.NullPointerException: Cannot invoke "java.lang.StringBuilder.length()" because "string" is null
at Main.main(Main.java:4)
```

> ⚠️ **Caution:** Always check for `null` before calling `length()` on a `StringBuilder` object to avoid `NullPointerException`. Use a null check like `if (string != null)` before accessing any methods.

> 💡 **Tip:** The `length()` method counts all characters including spaces, special characters, and digits. It is different from `capacity()` which returns the total allocated storage, not the actual content length.

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
