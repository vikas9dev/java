# Import StringBuffer In Java

**Import StringBuffer In Java** | The `StringBuffer` class is present in the `java.lang` package. Since `java.lang` is the default package available to every Java program, there is no need to import `StringBuffer` explicitly.

- [StringBuffer Class Facts](#stringbuffer-class-facts)
- [How To Import StringBuffer In Java](#how-to-import-stringbuffer-in-java)
- [StringBuffer append() Method Example](#stringbuffer-append-method-example)

---

## 1. StringBuffer Class Facts

Let us see some examples of the `StringBuffer` class to demonstrate some methods. In Java, except the `String` class, there are two more string manipulation classes: `StringBuilder` and `StringBuffer`. The `StringBuffer` class is synchronized whereas the `StringBuilder` class is non-synchronized. `StringBuilder` is used for single threading and `StringBuffer` is best suited for multi-threading.

Some key facts about the `StringBuffer` class:

- 🏗️ The `StringBuffer` class is inherited from the [Object class](069_Object_Class_in_Java.md).
- 📦 `StringBuffer` class inherits all methods from the Object class: [clone()](074_Clone()_Method_in_Java.md), equals(), `finalize()`, getClass(), `notifyAll()`, `notify()`, [hashCode()](071_Hashcode_in_Java_–_hashCode()_Method.md)
- 🔗 The `StringBuffer` implements the following interfaces: `Serializable`, `Comparable`, `CharSequence`
- 🔒 All methods of the `StringBuffer` class are safe for using multithreading operations because they are synchronized

**Constructors of StringBuffer class:**

| Constructor 🏷️ | Description 📋 |
|----------------|----------------|
| **`StringBuffer()`** | Creates an empty StringBuffer with default capacity of 16 |
| **`StringBuffer(int size)`** | Creates an empty StringBuffer with specified capacity |
| **`StringBuffer(String str)`** | Creates a StringBuffer initialized with the given string |

---

## 2. How To Import StringBuffer In Java

Since the `StringBuffer` class is given in `java.lang` package, we don't need to import it explicitly. We can call methods of the `StringBuffer` class directly.

**StringBuffer basic methods:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuffer sb = new StringBuffer("Java Programming");
      System.out.println("Length: " + sb.length());
      System.out.println("Capacity: " + sb.capacity());

      sb.append(" Language");
      System.out.println("StringBuffer: " + sb);
   }
}
```

📤 **Output:**

```
Length: 16
Capacity: 32
StringBuffer: Java Programming Language
```

> 📝 **Note:** The `StringBuffer` class contains all the methods of the `StringBuilder` class. Both classes are very similar but the main difference is: the `StringBuffer` class is synchronized whereas the `StringBuilder` class is non-synchronized. All the methods of both classes perform the same operation.

---

## 3. StringBuffer append() Method Example

Let us see another example of the `StringBuffer` class `append()` method. The append() method is used to add primitives, strings, objects, and `CharSequence` to the `StringBuffer` class.

**Appending different types:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuffer sb = new StringBuffer("Java");
      sb.append(" Programming");
      sb.append(" Language");
      System.out.println(sb);

      sb.append("-");
      sb.append(2030);
      System.out.println(sb);
   }
}
```

📤 **Output:**

```
Java Programming Language
Java Programming Language-2030
```

> 💡 **Tip:** Since `StringBuffer` is in `java.lang`, you never need an import statement for it, just like `String`, `Integer`, `System`, and other core classes.

---

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

**Java Tutorial**

- Import StringBuffer Class
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
