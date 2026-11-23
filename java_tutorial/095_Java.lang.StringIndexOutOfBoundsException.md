# Java.lang.StringIndexOutOfBoundsException

**Java.lang.StringIndexOutOfBoundsException** | In Java, `StringIndexOutOfBoundsException` arises when the string length is lesser than the given index. Usually, the index range should be between 0 to the string size. For example, if we have a string "Java" then we can access string elements from 0 to 3. If we try to access an element at a negative index or value greater than 4 in that case we will get `java.lang.StringIndexOutOfBoundsException`.

- [StringIndexOutOfBoundsException Example](#stringindexoutofboundsexception-example)
- [How to Handle StringIndexOutOfBoundsException](#how-to-handle-stringindexoutofboundsexception)
- [Related Links](#related-links)

---

## 1. Overview

The `string.charAt()` method returns the character at the specified index of the string. If the specified index value is lesser than 0 or greater than the string size then the `String.charAt()` throws `java.lang.StringIndexOutOfBoundsException`. Here are some of the examples which throw `StringIndexOutOfBoundsException`:

**Negative index example:**

```java
public class Main {
   public static void main(String[] args) {
      String string = "Java";
      System.out.println(string.charAt(-1));
   }
}
```

🚨 **Exception:**

```
Exception in thread "main" java.lang.StringIndexOutOfBoundsException: String index out of range: -1
at java.base/java.lang.StringLatin1.charAt(StringLatin1.java:48)
at java.base/java.lang.String.charAt(String.java:711)
at Main.main(Main.java:4)
```

In the mentioned example the index is lesser than the size of the string hence it throws `java.lang.StringIndexOutOfBoundsException: string index out of range: -1` exception. Let us see some more examples:

**More negative index:**

```java
String string = "Java";
System.out.println(string.charAt(-2));
```

🚨 **Exception:** `java.lang.StringIndexOutOfBoundsException: String index out of range: -2`

**Index exceeding length:**

```java
String string = "Java";
System.out.println(string.charAt(10));
```

🚨 **Exception:** `java.lang.StringIndexOutOfBoundsException: String index out of range: 10`

### Methods that throw StringIndexOutOfBoundsException

Now we would like to list some of the Java String class methods which throw the `java.lang.StringIndexOutOfBoundsException`:

| # | Method 🏷️ |
|---|-----------|
| 1 | `charAt(int index)` |
| 2 | `codePointAt(int index)` |
| 3 | `codePointBefore(int index)` |
| 4 | `codePointCount(int beginIndex, int endIndex)` |
| 5 | `offsetByCodePoints(int index, int codePointOffset)` |
| 6 | `getChars(int srcBegin, int srcEnd, char dst[], int dstBegin)` |
| 7 | `substring(int beginIndex)` |
| 8 | `substring(int beginIndex, int endIndex)` |
| 9 | `subSequence(int beginIndex, int endIndex)` |
| 10 | `valueOf(char data[], int offset, int count)` |
| 11 | `copyValueOf(char data[], int offset, int count)` |

### Constructors that throw StringIndexOutOfBoundsException

| # | Constructor 🏷️ |
|---|----------------|
| 1 | `String(char value[], int offset, int count)` |
| 2 | `String(int[] codePoints, int offset, int count)` |
| 3 | `String(byte bytes[], int offset, int length, String charsetName)` |
| 4 | `String(byte bytes[], int offset, int length, Charset charset)` |
| 5 | `String(byte bytes[], int offset, int length)` |

> 📝 **Note:** `StringIndexOutOfBoundsException` extends from `IndexOutOfBoundsException`. In arrays we get `IndexOutOfBoundsException`, but when it comes to strings then we get `StringIndexOutOfBoundsException`.

**Class definition:**

```java
public class StringIndexOutOfBoundsException extends IndexOutOfBoundsException { ... }
```

---

## 2. StringIndexOutOfBoundsException Example

**Substring with invalid index:**

```java
public class Main {
   public static void main(String[] args) {
      String string = "Java Programming Language";
      String str1 = string.substring(0, 13);
      System.out.println("String1 : " + str1);
      String str2 = string.substring(14, 36);
      System.out.println("String2 : " + str2);
   }
}
```

📤 **Output:**

```
String1 : Java Programm
Exception in thread "main" java.lang.StringIndexOutOfBoundsException: begin 14, end 36, length 25
at java.base/java.lang.String.checkBoundsBeginEnd(String.java:3751)
at java.base/java.lang.String.substring(String.java:1907)
at Main.main(Main.java:6)
```

In the above program, the first substring works fine but the second one throws the exception. Because the first `substring()` method has an index value within the string range but the second one exceeds the range.

---

## 3. How to Handle StringIndexOutOfBoundsException

### Using length check

**Handling by checking for the string length using `string.length()` method:**

```java
public class Main {
   public static void main(String[] args) {
      String string = "Java Programming Language";
      System.out.println("Length of string is: "
                         + string.length());

      int index = 12;
      if (index < string.length()) {
         String str1 = string.substring(0, index);
         System.out.println("str1 : " + str1);
      }

      index = 36;
      if (index <= string.length()) {
         String str2 = string.substring(14, 36);
         System.out.println("index : " + str2);
      }
   }
}
```

📤 **Output:**

```
Length of string is: 25
str1 : Java Program
```

### Using try-catch block

**Handle StringIndexOutOfBoundsException using try and catch block:**

```java
public class Main {
   public static void main(String[] args) {
      String string = "Java Programming Language ";
      try {
         String str1 = string.substring(0, 13);
         System.out.println("str1 : " + str1);
      } catch (StringIndexOutOfBoundsException e) {
         System.out.println(e.toString());
      }
      try {
         String str2 = string.substring(14, 36);
         System.out.println("str2 : " + str2);
         System.out.println(str2);
      } catch (StringIndexOutOfBoundsException e) {
         System.out.println(e.toString());
      }
   }
}
```

📤 **Output:**

```
str1 : Java Programm
java.lang.StringIndexOutOfBoundsException: begin 14, end 36, length 26
```

In the above example, we have used the `toString()` method to get the exception name and the reason for the exception. There are more ways to get the exception message in Java. See more: Different ways to get the exception message in Java

> 💡 **Tip:** Always validate your index values against `string.length()` before accessing string characters to prevent `StringIndexOutOfBoundsException`.

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

---

## 4. Related Links

**String Programs**
- Sum of digits in a String
- Count No of Vowels String
- String Pattern Programs in Java
- Take String Input In Java
- Take Multiple String Input in Java
- How To Reverse a String In Java
- Remove Special Characters
- String - Remove Character
- String Palindrome In Java
- Sort String In Java
- How to Compare Strings In Java
- Second Occurrence of Character
- Replace nth Occurrence String
- Last Occurrence of Character
- Uppercase & Lowercase
- Java Check If Char is Uppercase
- Check If String is Uppercase
- Swap Characters in String Java
- [Java String indexOf() Method](110_Java_String_indexOf()_Method.md)
- How to Replace Dot in Java?
- [How to Find Length of String](099_How_to_Find_Length_of_String_in_Java.md)
- [Substring Method In Java](112_Substring_Method_In_Java.md)
- [Split Method In Java](119_Split()_Method_In_Java.md)
