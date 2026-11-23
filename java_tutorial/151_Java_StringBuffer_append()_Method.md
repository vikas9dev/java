# Java StringBuffer append() Method

**Java StringBuffer append() Method** | Learn how to use the `append()` method in the `StringBuffer` class to concatenate strings, characters, and other data types.

- [Method Variations](#method-variations)
- [Java StringBuffer append() Example](#java-stringbuffer-append-example)
- [StringBuffer append() In Java Example](#stringbuffer-append-in-java-example)
- [Java StringBuffer Append New Line](#java-stringbuffer-append-new-line)
- [StringBuffer Java Append](#stringbuffer-java-append)
- [Related Links](#related-links)

---

## 1. Method Variations

The `append()` method appends two or more strings. The `append()` method of the `StringBuffer` class is very similar to the StringBuilder class append() method.

The `append()` method of the `StringBuffer` class has the following different variations:

| # | Method Signature 🔧 |
|---|---------------------|
| 1 | `public synchronized StringBuffer append(String str)` |
| 2 | `public synchronized StringBuffer append(Object obj)` |
| 3 | `public synchronized StringBuffer append(StringBuffer sb)` |
| 4 | `public synchronized StringBuffer append(CharSequence s)` |
| 5 | `public synchronized StringBuffer append(CharSequence s, int start, int end)` |
| 6 | `public synchronized StringBuffer append(char[] str)` |
| 7 | `public synchronized StringBuffer append(char[] str, int offset, int len)` |
| 8 | `public synchronized StringBuffer append(boolean b)` |
| 9 | `public synchronized StringBuffer append(char c)` |
| 10 | `public synchronized StringBuffer append(int i)` |
| 11 | `public synchronized StringBuffer append(long lng)` |
| 12 | `public synchronized StringBuffer append(float f)` |
| 13 | `public synchronized StringBuffer append(double d)` |

> 📝 **Note:** All `StringBuffer` methods are `synchronized`, making them thread-safe unlike `StringBuilder`.

---

## 2. Java StringBuffer append() Example

Let us see some examples of the `StringBuffer` class `append()` method. We will initialize an empty `StringBuffer` object and add some values to it.

**Appending multiple strings:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuffer sb = new StringBuffer();
      sb.append("Hi ");
      sb.append("John, ");
      sb.append("How ");
      sb.append("are ");
      sb.append("you?");
      System.out.println("Result = " + sb);
   }
}
```

📤 **Output:**

```
Result = Hi John, How are you?
```

Let us see an example of the `append()` method by appending the char array.

**Appending a char array:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuffer sb = new StringBuffer("Welcome to ");
      char[] ch = { 'K', 'n', 'o', 'w', 'P', 'r', 'o', 'g', 'r', 'a', 'm' };
      sb.append(ch);
      System.out.println("After appending = " + sb);
   }
}
```

📤 **Output:**

```
After appending = Welcome to KnowProgram
```

---

## 3. StringBuffer append() In Java Example

By using the `public StringBuffer append(boolean bool)` method of the `StringBuffer` class, we can append boolean values to the `StringBuffer` objects.

**Appending a boolean value:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuffer sb = new StringBuffer("Are you ok? ");
      sb.append(true);
      System.out.println("Result after appending = " + sb);

   }
}
```

📤 **Output:**

```
Result after appending = Are you ok? true
```

---

## 4. Java StringBuffer Append New Line

To append a new line we can use the `append(char ch)` method.

| Property 📋 | Details 📖 |
|-------------|-----------|
| **Syntax** | `public StringBuffer append(char ch)` |
| **Parameter** | `ch` — the character that needs to be appended |
| **Return type** | `StringBuffer` |
| **Returns** | The `StringBuffer` after appending the character |

**Appending a newline character:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuffer sb = new StringBuffer("Hello");
      sb.append('\n');
      sb.append("World");
      System.out.println("The result after appending = " + sb);
   }
}
```

📤 **Output:**

```
The result after appending = Hello
World
```

> 💡 **Tip:** Use `'\n'` to append a newline character, or `System.lineSeparator()` for platform-independent line breaks.

---

## 5. StringBuffer Java Append

From a given array of characters, we can also append only a few portions of the array to the `StringBuffer` object. The following method can be used for this purpose: `public StringBuffer append(char[] array, int index, int len)`

| Parameter 🏷️ | Description 📖 |
|--------------|---------------|
| **array** | The array which will be appended |
| **index** | Specifies the index of the first character to be appended |
| **len** | Says the number of characters to be appended |

**Appending partial char array:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuffer sb = new StringBuffer("Work ");
      System.out.println("StringBuffer before appending = " + sb);
      char[] array =
         { 'o', 'n', 'l', 'i', 'n', 'e', 'o', 'r', 'o', 'f', 'f', 'l', 'i', 'n', 'e' };
      sb.append(array, 0, 6);
      System.out.println("StringBuffer after appending = " + sb);
   }
}
```

📤 **Output:**

```
StringBuffer before appending = Work
StringBuffer after appending = Work online
```

---

## 6. Related Links

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
