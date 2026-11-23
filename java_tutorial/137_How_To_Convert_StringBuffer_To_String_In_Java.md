# How To Convert StringBuffer To String In Java

**How To Convert StringBuffer To String In Java** | Converting a `StringBuffer` to `String` using the `toString()` method and the `String` class constructor.

- [How To Convert A StringBuffer To String In Java using the toString() Method](#how-to-convert-a-stringbuffer-to-string-in-java-using-the-tostring-method)
- [How To Convert A StringBuffer To String In Java using the String Constructor](#how-to-convert-a-stringbuffer-to-string-in-java-using-the-string-constructor)

---

## 1. How To Convert A StringBuffer To String In Java using the toString() Method

There are built-in methods available to convert the `StringBuffer` to a string object. First, we see the `toString()` method which directly converts the `StringBuffer` to a string. The `String` class also contains a constructor to create a `String` object from the `StringBuffer` class object. Also see: [Java String To StringBuffer](136_Java_String_To_StringBuffer.md)

The syntax of the `toString()` method of `StringBuffer` class:

```java
public String toString()
```

| Detail 🏷️ | Description 📋 |
|-----------|----------------|
| **Parameters** | No parameters accepted |
| **Returns** | The string converted from a StringBuffer object |
| **Return type** | `String` |

**toString() conversion example:**

```java
public class Main {
    public static void main(String[] args) {
        StringBuffer sb = new StringBuffer("KnowProgram");
        System.out.println("StringBuffer: " + sb);
        System.out.println(sb.getClass().getName());

        String string = sb.toString();
        System.out.println("String: " + string);
        System.out.println(string.getClass().getName());
    }
}
```

📤 **Output:**

```
StringBuffer: KnowProgram
java.lang.StringBuffer
String: KnowProgram
java.lang.String
```

First, in the main class and in the main method we create an object of `StringBuffer` and pass the string "KnowProgram" to it. Then we convert the `StringBuffer` to the string object by using the `toString()` method and print the same using the print statement.

> 📝 **Note:** The getClass() method is used to find the current class and the `getName()` method returns the name of the class. In case of `StringBuffer` object `getClass().getName()` returns `java.lang.StringBuffer` and in the case of `String` object it returns `java.lang.String`.

---

## 2. How To Convert A StringBuffer To String In Java using the String Constructor

The `String` class has the following constructor to create a `String` object from the `StringBuffer` object:

```java
public String(StringBuffer buffer)
```

It allocates a new string that contains the sequence of characters currently contained in the string buffer argument. The contents of the string buffer are copied; subsequent modification of the string buffer does not affect the newly created string.

**String constructor conversion example:**

```java
public class Main {
    public static void main(String[] args) {
        StringBuffer sb = new StringBuffer("Hello World");
        System.out.println("StringBuffer: " + sb);
        System.out.println(sb.getClass().getName());

        String string = new String(sb);
        System.out.println("String: " + string);
        System.out.println(string.getClass().getName());
    }
}
```

📤 **Output:**

```
StringBuffer: Hello World
java.lang.StringBuffer
String: Hello World
java.lang.String
```

> 💡 **Tip:** Both `toString()` and the `String` constructor produce the same result. The `toString()` method is more concise and commonly preferred.

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
