# Java String To StringBuffer

**Java String To StringBuffer** | Converting an immutable `String` to a mutable `StringBuffer` using the constructor and `append()` method.

- [Java String To StringBuffer using Constructor](#java-string-to-stringbuffer-using-constructor)
- [String To StringBuffer In Java using append() Method](#string-to-stringbuffer-in-java-using-append-method)

---

## 1. Java String To StringBuffer using Constructor

We use `StringBuffer` when we want to modify and store the object in a multi-threading environment, whereas we use the `String` when we don't want to modify the string data or when we want to store an already modified string in a new object.

There are a few methods like the reverse() method which is available in the `StringBuffer` object but not in the `String` class. In that case, we can convert `String` to `StringBuffer` object and call `reverse()` method, later convert StringBuffer to String object.

The `StringBuffer` class has the following constructor to create a `StringBuffer` object from the given `String` object:

```java
public StringBuffer(String str)
```

It constructs a string buffer initialized to the contents of the specified string. The initial capacity of the string buffer is 16 plus the length of the string argument.

**Constructor conversion example:**

```java
public class Main {
    public static void main(String[] args) {
        String string = "We are learning Java programming language.";
        System.out.println("String: " + string);
        System.out.println(string.getClass().getName());

        // converting string to StringBuffer
        StringBuffer sb = new StringBuffer(string);
        System.out.println("StringBuffer: " + sb);
        System.out.println(sb.getClass().getName());
    }
}
```

📤 **Output:**

```
String: We are learning Java programming language.
java.lang.String
StringBuffer: We are learning Java programming language.
java.lang.StringBuffer
```

---

## 2. String To StringBuffer In Java using append() Method

Let us use the `append()` method to convert the string to the `StringBuffer`.

**Using append() for conversion:**

```java
public class Main {
    public static void main(String[] args) {

        String string = "Are you learning Java programming language? ";
        StringBuffer sb = new StringBuffer();
        sb.append(string);
        System.out.println("StringBuffer: " + sb);

        String string1 = "If you are new to programming, ";
        sb.append(string1);
        System.out.println("StringBuffer: " + sb);

        String string2 = "you can learn it from www.knowprogram.com";
        sb.append("\n" + string2);
        System.out.println("StringBuffer: " + sb);
    }
}
```

📤 **Output:**

```
StringBuffer: Are you learning Java programming language?
StringBuffer: Are you learning Java programming language? If you are new to programming,
StringBuffer: Are you learning Java programming language? If you are new to programming,
you can learn it from www.knowprogram.com
```

> 💡 **Tip:** Use the `StringBuffer(String str)` constructor for a single string conversion. Use the `append()` method when you need to build a `StringBuffer` from multiple strings incrementally.

---

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

**Java Tutorial**

- [Import StringBuffer Class](132_Import_StringBuffer_In_Java.md)
- [StringBuffer vs StringBuilder](133_When_To_Use_StringBuffer_And_StringBuilder_In_Java.md)
- String To StringBuilder
- StringBuilder To String
- String To StringBuffer
- StringBuffer To String

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
