# Java StringBuilder append() Method

**Java StringBuilder append() Method** | Learn how to use the `append()` method to add primitives, strings, objects, and character sequences to a `StringBuilder`.

- [Method Variations](#method-variations)
- [StringBuilder Append Java Example](#stringbuilder-append-java-example)
- [Example of StringBuilder Java Append](#example-of-stringbuilder-java-append)
- [Related Links](#related-links)

---

## 1. Method Variations

The `append()` method is used to append the `StringBuilder` to primitives, strings, objects, and character sequences. The different variations of the `append()` method are:

| # | Method Signature 🔧 |
|---|---------------------|
| 1 | `public StringBuilder append(Object obj)` |
| 2 | `public StringBuilder append(String str)` |
| 3 | `public StringBuilder append(StringBuffer sb)` |
| 4 | `public StringBuilder append(CharSequence s)` |
| 5 | `public StringBuilder append(CharSequence s, int start, int end)` |
| 6 | `public StringBuilder append(char[] str)` |
| 7 | `public StringBuilder append(char[] str, int offset, int len)` |
| 8 | `public StringBuilder append(boolean b)` |
| 9 | `public StringBuilder append(char c)` |
| 10 | `public StringBuilder append(int i)` |
| 11 | `public StringBuilder append(long lng)` |
| 12 | `public StringBuilder append(float f)` |
| 13 | `public StringBuilder append(double d)` |

---

## 2. StringBuilder Append Java Example

Let us see an example of the `StringBuilder` class `append()` method by appending different types of values like `int`, `float`, `double`, `String`, etc.

**Appending multiple types:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuilder sb = new StringBuilder("");
      sb.append("Hello");
      sb.append(20);
      sb.append('K');
      sb.append(true);
      sb.append(50.90);
      System.out.println(sb);
   }
}
```

📤 **Output:**

```
Hello20Ktrue50.9
```

In the below program we are using `StringBuilder append(boolean bool)` variation. The syntax for this method is: **`public StringBuilder append(boolean bool)`**

**Appending boolean values:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuilder sb = new StringBuilder("Are you ready? ");
      System.out.println("Before appending: " + sb);
      sb.append(true);
      System.out.println("After appending: " + sb);

      StringBuilder sb1 = new StringBuilder("Are you ok? ");
      System.out.println("Before appending: " + sb1);
      sb1.append(false);
      System.out.println("After appending: " + sb1);
   }
}
```

📤 **Output:**

```
Before appending: Are you ready?
After appending: Are you ready? true
Before appending: Are you ok?
After appending: Are you ok? false
```

---

## 3. Example of StringBuilder Java Append

Let us see a program to append a character to the `StringBuilder` object. The method syntax to append the character is: **`public StringBuilder append(char ch)`**

**Appending a character:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuilder sb = new StringBuilder("Welcome Boy");
      System.out.println(sb);
      sb.append('s');
      System.out.println("After appending = " + sb);

      sb = new StringBuilder("Hello world");
      System.out.println(sb);
      sb.append('#');
      System.out.println("After appending = " + sb);
   }
}
```

📤 **Output:**

```
Welcome Boy
After appending = Welcome Boys
Hello world
After appending = Hello world#
```

We can also append an array to `StringBuilder`. The `append()` method syntax for it is: **`public StringBuilder append(char[] charray)`**

**Appending a char array:**

```java
public class Main {
   public static void main(String[] args) {

      StringBuilder sb = new StringBuilder("We are ");
      System.out.println(sb);
      char[] array = { 'P', 'R', 'O', 'G', 'R', 'A', 'M', 'M', 'E', 'R', 'S' };
      sb.append(array);
      System.out.println("After appending = " + sb);

      sb = new StringBuilder("Let us say together - ");
      System.out.println(sb);
      array = new char[] { 'a', 'b', 'c', 'd', 'e', 'f', 'g' };
      sb.append(array);
      System.out.println("After appending = " + sb);
   }
}
```

📤 **Output:**

```
We are
After appending = We are PROGRAMMERS
Let us say together –
After appending = Let us say together – abcdefg
```

The `StringBuilder` class also contains **`public StringBuilder append(char[] str, int offset, int len)`** which can be used to append only some portion of the char array.

**Appending partial char array:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuilder sb = new StringBuilder("Java ");
      System.out.println("String Builder = " + sb);
      char[] array = { 'P', 'r', 'o', 'g', 'r', 'a', 'm', 'm', 'i', 'n', 'g' };
      sb.append(array, 0, 7);
      System.out.println("After appending StringBuilder = " + sb);
   }
}
```

📤 **Output:**

```
String Builder = Java
After appending StringBuilder = Java Program
```

> 💡 **Tip:** Use `append(char[] str, int offset, int len)` when you only need a portion of a character array appended to the `StringBuilder`.

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
