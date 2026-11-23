# Java StringBuffer insert() Method

**Java StringBuffer insert() Method** | Learn how to insert characters, strings, and other data types into a `StringBuffer` at a specified index using the `insert()` method.

- [Method Variations](#method-variations)
- [How To Insert String To StringBuffer Java](#how-to-insert-string-to-stringbuffer-java)
- [Insert String To StringBuffer Java](#insert-string-to-stringbuffer-java)
- [Insert StringBuffer In Java](#insert-stringbuffer-in-java)
- [Related Links](#related-links)

---

## 1. Method Variations

The `insert()` method in the `StringBuffer` class is used to insert the given character or the string at the said index. There are many variations of the `insert()` method:

| # | Method Signature 🔧 |
|---|---------------------|
| 1 | `public synchronized StringBuffer insert(int offset, String str)` |
| 2 | `public synchronized StringBuffer insert(int offset, Object obj)` |
| 3 | `public synchronized StringBuffer insert(int offset, char[] str)` |
| 4 | `public synchronized StringBuffer insert(int index, char[] str, int offset, int len)` |
| 5 | `public StringBuffer insert(int dstOffset, CharSequence s)` |
| 6 | `public synchronized StringBuffer insert(int dstOffset, CharSequence s, int start, int end)` |
| 7 | `public StringBuffer insert(int offset, boolean b)` |
| 8 | `public synchronized StringBuffer insert(int offset, char c)` |
| 9 | `public StringBuffer insert(int offset, int i)` |
| 10 | `public StringBuffer insert(int offset, long l)` |
| 11 | `public StringBuffer insert(int offset, float f)` |
| 12 | `public StringBuffer insert(int offset, double d)` |

All of the above `insert()` methods **throw StringIndexOutOfBoundsException**. As we know `StringBuffer` class is synchronized and all its methods are also synchronized. But in the above list of `insert()` methods, some methods don't contain the `synchronized` keyword in the method declaration — don't think that they are non-synchronized methods. Actually internally they call the **`insert(int, String)`** method which is synchronized. Hence synchronization is achieved via invocations of other `StringBuffer` methods.

> 🔒 **Note:** See more: [When To Use StringBuffer And StringBuilder In Java?](133_When_To_Use_StringBuffer_And_StringBuilder_In_Java.md)

🔍 **Example:**
- String: `"Bok"`, Insert `'o'` at 2nd position — After insertion: `"Book"`
- String: `"Hello"`, Insert `"World"` at 6th position — After insertion: `"Hello World"`

---

## 2. How To Insert String To StringBuffer Java

Let us see how to insert a string to `StringBuffer` in Java using the `insert()` method.

**Inserting a string:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuffer sb = new StringBuffer("Learning Java Language");
      System.out.println("StringBuffer: " + sb);
      sb.insert(14, "Programming ");
      System.out.println("StringBuffer after appending: " + sb);
   }
}
```

📤 **Output:**

```
StringBuffer: Learning Java Language
StringBuffer after appending: Learning Java Programming Language
```

Now we are demonstrating the `insert()` method with a boolean value.

| Parameter 🏷️ | Description 📖 |
|--------------|---------------|
| **pos** | The position from where to insert |
| **bool** | The boolean value `true` or `false` |
| **Returns** | The `StringBuffer` after insertion |

**Inserting a boolean value:**

```java
public class Main {
   public static void main(String[] args) {
      String string = "Programmers typically define the boolean "
                          + " terms to have values 1.";
      StringBuffer sb = new StringBuffer(string);
      System.out.println("StringBuffer = " + sb);
      sb.insert(41, true);
      System.out.println("StringBuffer after insertion = " + sb);
   }
}
```

📤 **Output:**

```
StringBuffer = Programmers typically define the boolean  terms to have values 1.
StringBuffer after insertion = Programmers typically define the boolean true terms to have values 1.
```

---

## 3. Insert String To StringBuffer Java

Let us see an example to insert the character to the `StringBuffer`.

| Parameter 🏷️ | Description 📖 |
|--------------|---------------|
| **pos** | The position from where to insert |
| **ch** | The character needed to be inserted |
| **Returns** | The `StringBuffer` after insertion |

**Inserting a character:**

```java
public class Main {
   public static void main(String[] args) {
      String string = "insert ethod is used to insert the characters";
      StringBuffer sb = new StringBuffer(string);
      System.out.println("StringBuffer = " + sb);
      sb.insert(7, 'm');
      System.out.print("After insertion = " + sb);
   }
}
```

📤 **Output:**

```
StringBuffer = insert ethod is used to insert the characters
After insertion = insert method is used to insert the characters
```

---

## 4. Insert StringBuffer In Java

Now we are inserting the character array into the `StringBuffer`.

| Parameter 🏷️ | Description 📖 |
|--------------|---------------|
| **pos** | The position from where to insert |
| **charray** | The character array needed to be inserted |
| **Returns** | The `StringBuffer` after insertion |

**Inserting a char array:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuffer string = new StringBuffer(" garden");
      System.out.println("StringBuffer = " + string);
      char array[] = { 'p', 'a', 'p', 'a', 'y', 'a' };
      string.insert(0, array);
      System.out.print("After insertion = " + string);
   }
}
```

📤 **Output:**

```
StringBuffer = garden
After insertion = papaya garden
```

> 💡 **Tip:** The `insert()` method is very versatile — it can insert `boolean`, `char`, `char[]`, `String`, `Object`, `CharSequence`, `int`, `long`, `float`, and `double` values at any valid position.

```mermaid
graph LR
    A["StringBuffer: ' garden'"] --> B["insert(0, 'papaya')"]
    B --> C["Result: 'papaya garden'"]

    classDef purple fill:#A162F7,stroke:#A162F7,color:#fff
    classDef cyan fill:#00b4d8,stroke:#00b4d8,color:#fff
    classDef green fill:#28C76F,stroke:#28C76F,color:#fff

    class A purple
    class B cyan
    class C green
```

---

## 5. Related Links

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
