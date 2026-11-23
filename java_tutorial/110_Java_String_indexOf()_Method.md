# Java String indexOf() Method

**Java String indexOf() Method** | The `indexOf()` methods return the index of the first occurrence of the specified character or return -1 if the character does not occur. The syntax for the `indexOf()` method in the String class is: `int indexOf(char ch)`

- [The lastIndexOf In Java](#the-lastindexof-in-java)
- [Find Character In String Java](#find-character-in-string-java)
- [Get Char From String Java](#get-char-from-string-java)
- [How To Get Particular Word From String In Java](#how-to-get-particular-word-from-string-in-java)
- [Getting A Substring From A String After A Particular Word In Java](#getting-a-substring-from-a-string-after-a-particular-word-in-java)

There are also many overloaded methods that can be used for our convenience.

**Quick example:**

```java
String string = "I Love programming";
System.out.println(string.indexOf('a'));
```

The above code returns 12 because the character 'a' exists at the 12th index in the given string. Here count or index starts from 0.

| Method 📋 | Parameter 🔤 | Returns 🔍 |
|-----------|-------------|-----------|
| **`indexOf(int ch)`** | A character | Index of first occurrence |
| **`indexOf(int ch, int fromIndex)`** | Character + start index | Index from given position |
| **`indexOf(String str)`** | A substring | Index of first occurrence of substring |
| **`indexOf(String str, int fromIndex)`** | Substring + start index | Index from given position |
| **`lastIndexOf(int ch)`** | A character | Index of last occurrence |
| **`lastIndexOf(int ch, int fromIndex)`** | Character + start index | Last occurrence before given index |

> 📝 **Note:** All methods throw `IndexOutOfBoundsException` if the given index is more than the string length.

---

## 1. The lastIndexOf In Java

The [lastIndexOf() method](111_String_lastIndexOf()_in_Java.md) returns the last occurrence of the specified character. Java provides many other ways to find the last index of the character.

**i) Using lastIndexOf(int ch):**

```java
public class Main {
   public static void main(String args[]) {
      String string = "I Love programming";
      System.out.println(string.lastIndexOf('g'));
   }
}
```

📤 **Output:**

```
17
```

**ii) Using lastIndexOf(int ch, int fromIndex):**

This method takes an extra argument integer `fromIndex` - it returns the last occurrence of the character at or before the specified index.

```java
public class Main {
   public static void main(String args[]) {
      String s = "I Love programming";
      System.out.println(s.lastIndexOf('g', 10));
   }
}
```

📤 **Output:**

```
10
```

**iii) Using lastIndexOf(String str):**

This method accepts the whole string as an argument and returns the index of the first character of the last matching substring.

```java
public class Main {
   public static void main(String args[]) {
      String s = "I Love programming";
      System.out.println(s.lastIndexOf("Love"));
   }
}
```

📤 **Output:**

```
2
```

**iv) Using lastIndexOf(String str, int fromIndex):**

This method searches for a string at or before the specified index. If not present, it returns -1.

```java
public class Main {
   public static void main(String args[]) {
      String s = "I Love programming";
      System.out.println(s.lastIndexOf("Java", 3));
   }
}
```

📤 **Output:**

```
-1
```

---

## 2. Find Character In String Java

To find a character in a string we usually use the `indexOf()` method which returns the first occurrence of the character. There are various ways to find this.

**i) Using indexOf(int ch):**

It returns the index position of the given character at its first occurrence. In the below example, there are many 'a' characters but `indexOf()` returns the index of the first occurrence.

```java
public class Main {
   public static void main(String args[]) {
      String string = "Java is a good pogramming language";
      System.out.println(string.indexOf("a"));
   }
}
```

📤 **Output:**

```
1
```

**ii) Using indexOf(int ch, int fromIndex):**

For this method, we need to pass two parameters: the character and the index from which the search should begin.

**Find first occurrence from a given index:**

```java
public class Main {
   public static void main(String args[]) {
      String string = "Java is a good rpogramming language";
      System.out.println(string.indexOf("a", 7));
   }
}
```

📤 **Output:**

```
8
```

**iii) Using indexOf(String str):**

This method takes a string as a parameter and returns the position of the given substring.

```java
public class Main {
   public static void main(String args[]) {
      String string = "Java is a good pogramming language";
      System.out.println(string.indexOf("good"));
   }
}
```

📤 **Output:**

```
10
```

**iv) Using indexOf(String str, int fromIndex):**

This method takes two parameters: a string and a starting index, and returns the string from that index.

```java
public class Main {
   public static void main(String args[]) {
      String s = "Java is a good pogramming is language";
      System.out.println(s.indexOf("is", 25));
   }
}
```

📤 **Output:**

```
26
```

---

## 3. Get Char From String Java

To get a character from a string we use the `charAt()` method. This method takes one parameter (an integer index) and returns the character at that index.

**charAt() example:**

```java
public class Main {
   public static void main(String args[]) {
      String string = "Java is a good pogramming is language";
      System.out.println(string.charAt(0));
   }
}
```

📤 **Output:**

```
J
```

---

## 4. How To Get Particular Word From String In Java

Here, we extract words from the string in Java by using the `split()` method.

**Splitting a string into words:**

```java
public class Main {
   public static void main(String args[]) {
      String string = "Java Programming";
      String[] words = string.split(" ", 3);
      for (String word : words) {
         System.out.println(word);
      }
   }
}
```

📤 **Output:**

```
Java
Programming
```

---

## 5. Getting A Substring From A String After A Particular Word In Java

In this section we extract a substring after a given substring, using a user-defined function that takes two string parameters `value` and `a`.

**Extract substring after a word:**

```java
public class Main {
   public static String after(String value, String a) {
      int posA = value.lastIndexOf(a);
      if (posA == -1) {
         return "";
      }
      int adjustedPosA = posA + a.length();
      if (adjustedPosA >= value.length()) {
         return "";
      }
      return value.substring(adjustedPosA);
   }

   public static void main(String args[]) {
      String s = "I Love Programming";
      System.out.println(after(s, "I "));
      System.out.println(after(s, "I Love "));
   }
}
```

📤 **Output:**

```
Love Programming
Programming
```

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

**Java Tutorial**

**[String Class Methods](097_String_Class_Methods_In_Java.md)**
- charAt() Method
- codePoints() Method
- [compareTo() Method](106_String_compareTo()_Java.md)
- [compareToIgnoreCase()](107_String_compareToIgnoreCase()_Java.md)
- [concat() Method](113_Concat_Strings_in_Java.md)
- [contains() Method](116_String_contains()_Method_in_Java.md)
- equals() Method
- [equalsIgnoreCase()](105_String_equalsIgnoreCase()_Java.md)
- format() Method
- getBytes() Method
- hashCode() Method
- indent() Method
- indexOf() Method
- intern() Method
- [isBlank() Method](124_String_isBlank()_Java_with_Examples.md)
- [isEmpty() Method](100_String_isEmpty()_Java_with_Examples.md)
- isBlank() vs isEmpty()
- [join() Method](098_String_join()_In_Java.md)
- [lastIndexOf() Method](111_String_lastIndexOf()_in_Java.md)
- [length() Method](099_How_to_Find_Length_of_String_in_Java.md)
- matches() Method
- repeat() Method
- [replace() Method](114_Replace()_In_String_Java.md)
- [replaceAll() Method](118_String_replaceAll()_Java.md)
- replaceFirst() Method
- replace() vs replaceAll()
- [split() Method](119_Split()_Method_In_Java.md)
- startsWith() & endsWith()
- strip() & stripLeading()
- [substring() Method](112_Substring_Method_In_Java.md)
- toCharArray() Method
- [toLowerCase() Method](120_Java_String_to_Lowercase.md)
- [toString() Method](126_String_toString()_Java.md)
- toUpperCase() Method
- [trim() Method](122_Trim()_in_Java_String.md)
- [trim() vs strip()](093_Java_String_trim()_Vs_strip().md)
- valueOf() Method
