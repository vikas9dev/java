# StringBuilder capacity() Method In Java

**StringBuilder capacity() Method In Java** | Learn how the `capacity()` method works in the `StringBuilder` class and how capacity is calculated when characters are added.

- [Default Capacity of StringBuilder In Java](#default-capacity-of-stringbuilder-in-java)
- [Initial Capacity Of StringBuilder Java](#initial-capacity-of-stringbuilder-java)
- [StringBuilder capacity() Java Example](#stringbuilder-capacity-java-example)
- [Java StringBuilder capacity()](#java-stringbuilder-capacity)
- [Java StringBuilder capacity() Method Example](#java-stringbuilder-capacity-method-example)
- [Related Links](#related-links)

---

## 1. Default Capacity of StringBuilder In Java

The `capacity()` method of the `StringBuilder` class **returns the capacity of the given string**. The capacity is the total number of characters the `StringBuilder` object can contain.

| Property 📋 | Details 📖 |
|-------------|-----------|
| **Syntax** | `public int capacity()` |
| **Parameters** | None |
| **Return type** | `int` |
| **Returns** | The capacity of the string |

For any empty string, the **default capacity is 16 characters**. Once we call the `append()` method to add the characters and if the number of characters increases above 16 then the capacity can be calculated by the given formula:

🔑 **Key Point:** New capacity = **(old-capacity * 2) + 2**

**Default capacity example:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuilder sb = new StringBuilder();
      System.out.println("Default capacity = " + sb.capacity());
   }
}
```

📤 **Output:**

```
Default capacity = 16
```

---

## 2. Initial Capacity Of StringBuilder Java

The default capacity of `StringBuilder` is 16 when `StringBuilder` is empty. But if we initialize the `StringBuilder` object with some string then the **initial capacity = default capacity + length of the string.**

```mermaid
graph LR
    A["Default Capacity: 16"] --> B["+ String Length"]
    B --> C["= Initial Capacity"]

    classDef purple fill:#A162F7,stroke:#A162F7,color:#fff
    classDef cyan fill:#00b4d8,stroke:#00b4d8,color:#fff
    classDef green fill:#28C76F,stroke:#28C76F,color:#fff

    class A purple
    class B cyan
    class C green
```

**Example with "Java" (length 4):**

```java
public class Main {
   public static void main(String[] args) {
      String string = "Java";
      System.out.println("String length: " + string.length());

      StringBuilder sb = new StringBuilder(string);
      System.out.println("StringBuilder: " + sb);
      System.out.println("Capacity: " + sb.capacity());
   }
}
```

📤 **Output:**

```
String length: 4
StringBuilder: Java
Capacity: 20
```

🧠 **In Simple Words:** The default capacity = 16, length of the string = 4. Hence the initial capacity = 16 + 4 = 20

**Example with "Java Program" (length 12):**

```java
public class Main {
   public static void main(String[] args) {
      String string = "Java Program";
      System.out.println("String length: " + string.length());

      StringBuilder sb = new StringBuilder(string);
      System.out.println("StringBuilder: " + sb);
      System.out.println("Capacity: " + sb.capacity());
   }
}
```

📤 **Output:**

```
String length: 12
StringBuilder: Java Program
Capacity: 28
```

📝 **Note:** The default capacity = 16, length of the string = 12. Hence the initial capacity = 16 + 12 = 28

**Example with "Java Programming Language" (length 25):**

```java
public class Main {
   public static void main(String[] args) {
      System.out.println("Length: " + "Java Programming Language".length());
      StringBuilder sb = new StringBuilder("Java Programming Language");
      System.out.println("StringBuilder: " + sb);
      System.out.println("Capacity: " + sb.capacity());
   }
}
```

📤 **Output:**

```
Length: 25
StringBuilder: Java Programming Language
Capacity: 41
```

📝 **Note:** The default capacity = 16, length of the string = 25. Hence the initial capacity = 16 + 25 = 41.

---

## 3. StringBuilder capacity() Java Example

Let us see some examples of the `StringBuilder` `capacity()` method. The initial capacity will be 16 characters, and after inserting the 16 characters the capacity will be increased to 34. Similarly, once the number of characters reached 34 then the capacity will be increased to 70.

🔑 **Key Point:** New capacity = **(old-capacity * 2) + 2**

**Capacity growth example:**

```java
public class Main {
   public static void main(String[] args) {

      StringBuilder sb = new StringBuilder();
      System.out.println("StringBuilder: " + sb);
      System.out.println("Length: " + sb.length());
      System.out.println("Default capacity: " + sb.capacity());

      sb.append("Java Programming");
      System.out.println("StringBuilder: " + sb);
      System.out.println("Length: " + sb.length());
      System.out.println("Current capacity: " + sb.capacity());

      sb.append("-");
      System.out.println("StringBuilder: " + sb);
      System.out.println("Length: " + sb.length());
      System.out.println("Current capacity: " + sb.capacity());
   }
}
```

📤 **Output:**

```
StringBuilder:
Length: 0
Default capacity: 16
StringBuilder: Java Programming
Length: 16
Current capacity: 16
StringBuilder: Java Programming-
Length: 17
Current capacity: 34
```

> 💡 **Tip:** When the number of characters was 16 the capacity was still 16. But once we add one more character and the count exceeds 16, the capacity becomes `(16 * 2) + 2 = 34`.

---

## 4. Java StringBuilder capacity()

From the above examples, don't conclude that capacity will always be 16, 34, 70, and so on. The formula is `old-capacity * 2 + 2`. If the initial capacity is 20, then the new capacity will be `20 * 2 + 2 = 42`. The below example demonstrates it better.

**Capacity with initialized string:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuilder sb = new StringBuilder();
      System.out.println("Default capacity: " + sb.capacity());

      StringBuilder sb1 = new StringBuilder("Hello");
      System.out.println("Initial Capacity: " + sb1.capacity());

      sb1.append(", World! ");
      System.out.println("New capacity: " + sb1.capacity());

      sb1.append("Java Programing Language");
      System.out.println("New capacity: " + sb1.capacity());

      sb1.append("-KnowProgram");
      System.out.println("New capacity: " + sb1.capacity());
   }
}
```

📤 **Output:**

```
Default capacity: 16
Initial Capacity: 21
New capacity: 21
New capacity: 44
New capacity: 90
```

| Step 📏 | Content Length 🔢 | Capacity 📦 | Explanation 📖 |
|---------|-------------------|-------------|---------------|
| **Empty** | 0 | 16 | Default capacity |
| **"Hello"** | 5 | 21 | 16 + 5 = 21 |
| **+ ", World! "** | 14 | 21 | Still within capacity |
| **+ "Java Programing Language"** | 38 | 44 | (21 * 2) + 2 = 44 |
| **+ "-KnowProgram"** | 50 | 90 | (44 * 2) + 2 = 90 |

---

## 5. Java StringBuilder capacity() Method Example

From the above example, we may think that capacity of a given `StringBuilder` object will always increase but this is not true. If we change the `StringBuilder` object then the capacity of the `StringBuilder` object can also be decreased.

**Capacity decrease example:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuilder sb = new StringBuilder("Learn Java Programming Language");
      System.out.println("StringBuilder: " + sb);
      System.out.println("Capacity: " + sb.capacity());

      sb = new StringBuilder("Hi");
      System.out.println("StringBuilder: " + sb);
      System.out.println("Capacity: " + sb.capacity());
   }
}
```

📤 **Output:**

```
StringBuilder: Learn Java Programming Language
Capacity: 47
StringBuilder: Hi
Capacity: 18
```

> 📝 **Note:** When a new `StringBuilder` object is created with a shorter string, the capacity is recalculated based on the new string's length (16 + 2 = 18), not carried over from the old object.

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
