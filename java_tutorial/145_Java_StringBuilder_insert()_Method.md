# Java StringBuilder insert() Method

**Java StringBuilder insert() Method** | Learn how to insert strings, characters, and other data types into a `StringBuilder` at a specified position using the `insert()` method.

- [Method Variations](#method-variations)
- [StringBuilder Java insert() Method Example](#stringbuilder-java-insert-method-example)
- [StringBuilder insert() Java Example](#stringbuilder-insert-java-example)
- [Related Links](#related-links)

---

## 1. Method Variations

The `StringBuilder` class in Java contains the `insert()` method that helps us to insert the string or the character. There are many variations of the `insert()` method:

| # | Method Signature 🔧 |
|---|---------------------|
| 1 | `public StringBuilder insert(int offset, float flt)` |
| 2 | `public StringBuilder insert(int offset, int i)` |
| 3 | `public StringBuilder insert(int offset, long lng)` |
| 4 | `public StringBuilder insert(int offset, Object objt)` |
| 5 | `public StringBuilder insert(int offset, String string)` |
| 6 | `public StringBuilder insert(int ind, char[] array, int offset, int len)` |
| 7 | `public StringBuilder insert(int dstOffset, CharSequence seq)` |
| 8 | `public StringBuilder insert(int dstOffset, CharSequence seq, int begin, int end)` |
| 9 | `public StringBuilder insert(int offset, double dbl)` |
| 10 | `public StringBuilder insert(int offset, boolean bool)` |
| 11 | `public StringBuilder insert(int offset, char c)` |
| 12 | `public StringBuilder insert(int offset, char[] array)` |

Internally the second argument is converted to string and **calls `insert(int, String)`** to insert the given values to the `StringBuilder` object. The `offset` argument must be greater than or equal to `0`, and less than or equal to the length of this sequence. Otherwise, it **throws StringIndexOutOfBoundsException if the offset is invalid**.

> ⚠️ **Caution:** If the offset value is negative or greater than the length of the `StringBuilder`, a `StringIndexOutOfBoundsException` will be thrown.

---

## 2. StringBuilder Java insert() Method Example

The below program demonstrates the `public StringBuilder insert(int offset, boolean bool)`. The offset value must be greater than or equal to `0`, and less than or equal to the length of this sequence.

**Inserting boolean values:**

```java
public class Main {
   public static void main(String[] args) {

      StringBuilder sb = new StringBuilder("Hello  Welcome");
      System.out.println("StringBuilder1 = " + sb);
      sb.insert(6, false);
      System.out.println("After insert = " + sb);
      System.out.println();

      StringBuilder sb1 = new StringBuilder("Two is greater than one? ");
      System.out.println("StringBuilder2 = " + sb1);
      sb1.insert(sb1.length(), true);
      System.out.println("After insert = " + sb1);
   }
}
```

📤 **Output:**

```
StringBuilder1 = Hello Welcome
After insert = Hello false Welcome

StringBuilder2 = Two is greater than one?
After insert = Two is greater than one? true
```

---

## 3. StringBuilder insert() Java Example

Let us see another example for `StringBuilder` `insert()`. We will demonstrate `insert(int offset, char c)`, `insert(int offset, char[] str)`, and `insert(int dstOffset, CharSequence cs)` methods.

**Inserting char, char array, and CharSequence:**

```java
public class Main {
   public static void main(String[] args) {

      StringBuilder sb = new StringBuilder("Jungl");
      System.out.println("StringBuilder1: " + sb);
      char c = 'e';
      // insert(int offset, char c)
      sb.insert(5, c);
      System.out.println("After insert = " + sb);
      System.out.println();

      StringBuilder sb1 = new StringBuilder("Java");
      System.out.println("StringBuilder2: " + sb1);
      char[] array = { 'P', 'r', 'o', 'g', 'r', 'a', 'm' };
      // insert(int offset, char[] str)
      sb1.insert(0, array);
      System.out.println("After insert = " + sb1);
      System.out.println();

      StringBuilder sb3 = new StringBuilder("App");
      System.out.println("StringBuilder3: " + sb3);
      CharSequence ch = "le";
      // insert(int dstOffset, CharSequence cs)
      sb3.insert(3, ch);
      System.out.println("After insert = " + sb3);
   }
}
```

📤 **Output:**

```
StringBuilder1: Jungl
After insert = Jungle

StringBuilder2: Java
After insert = ProgramJava

StringBuilder3: App
After insert = Apple
```

If the passed offset value is invalid then `insert()` methods throw **StringIndexOutOfBoundsException**. The below Java program demonstrates it:

**Inserting String and handling exception:**

```java
public class Main {
   public static void main(String[] args) {

      StringBuilder sb = new StringBuilder("Learn Java  Language");
      System.out.println("StringBuilder1: " + sb);
      String string = "Programming";
      sb.insert(11, string);
      System.out.println("After insert = " + sb);
      System.out.println();

      StringBuilder sb1 = new StringBuilder("Java");
      System.out.println("StringBuilder2: " + sb1);
      sb1.insert(-5, string);
      System.out.println("After insert = " + sb1);
   }
}
```

📤 **Output:**

```
StringBuilder1: Learn Java Language
After insert = Learn Java Programming Language

StringBuilder2: Java
Exception in thread "main" java.lang.StringIndexOutOfBoundsException: offset -5, length 4
```

> 🚨 **Note:** Passing a negative offset (`-5`) causes a `StringIndexOutOfBoundsException` because offset must be between `0` and `length()`.

```mermaid
graph LR
    A["StringBuilder: 'Java'"] --> B["insert(-5, 'Programming')"]
    B --> C["StringIndexOutOfBoundsException"]

    classDef purple fill:#A162F7,stroke:#A162F7,color:#fff
    classDef cyan fill:#00b4d8,stroke:#00b4d8,color:#fff
    classDef red fill:#EA5455,stroke:#EA5455,color:#fff

    class A purple
    class B cyan
    class C red
```

---

## 4. Related Links

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
