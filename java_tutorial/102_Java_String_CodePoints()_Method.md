# Java String CodePoints() Method

**Java String CodePoints() Method** | This tutorial focuses on the Java built-in methods `codePoints()`, `codePointAt()`, `codePointBefore()`, `codePointCount()`, and `offsetByCodePoints()`. Each character in a programming language has been assigned an ASCII (American Standard Code for Information Exchange) value or Unicode value. To fetch those values for a particular character, we can use the codepoints methods.

- [Java String codePoints() Method Example](#java-string-codepoints-method-example)
- [Program to Remove Specific Character From String](#program-to-remove-specific-character-from-string)
- [Java String codePointAt() Method Example](#java-string-codepointat-method-example)
- [Java String codePointBefore() Method Example](#java-string-codepointbefore-method-example)
- [Java String codePointCount() Method Example](#java-string-codepointcount-method-example)
- [Java String offsetByCodePoints() Method Example](#java-string-offsetbycodepoints-method-example)

There are different [Unicode](017_Unicode_Character_Set_in_Java.md) values for small letters and capital letters:

- 🔠 A-Z = 65 - 90
- 🔡 a-z = 97 - 122

These Unicode values are a series of numbers where the capital letters start from 65 and end at 90 (i.e. 'A' has a Unicode value of 65 and 'Z' has 90), the same way 'a' starts from 97 and 'z' ends at 122.

Below are the different variations in the codepoints methods:

| Method 📋 | Description 🔤 |
|-----------|---------------|
| **`codePoints()`** | Returns a stream of code point values from this sequence |
| **`codePointAt(int index)`** | Returns the Unicode code point at the specified index |
| **`codePointBefore(int index)`** | Returns the Unicode code point before the specified index |
| **`codePointCount(int beginIndex, int endIndex)`** | Returns the number of Unicode code points in the specified text range |
| **`offsetByCodePoints(int index, int codePointOffset)`** | Returns the index offset from the given index by codePointOffset code points |

---

## 1. Java String codePoints() Method Example

The Java String class `codePoints()` method returns a stream of code point values from this sequence. Any surrogate pairs encountered in the sequence are combined as if by `Character.toCodePoint()` and the result is passed to the stream.

**codePoints() example:**

```java
import java.util.stream.IntStream;

public class Main {
   public static void main(String[] args) {
      String string = "Know Program";
      System.out.println("Input string value : " + string);
      IntStream intStream = string.codePoints();
      System.out.println("Printing each char from the string as an ASCII value: ");
      intStream.forEach(value -> System.out.print(value + " "));
   }
}
```

📤 **Output:**

```
Input string value: Know Program
Printing each char from the string as an ASCII value:
75 110 111 119 32 80 114 111 103 114 97 109
```

---

## 2. Program to Remove Specific Character From String

To remove a specific character from the given string we can apply the `filter()` method on the resultant `IntStream`.

**Remove character using codePoints():**

```java
import java.util.stream.IntStream;

public class Main {
   public static void main(String[] args) {
      String string = "Know Program";
      System.out.println("Input string value: " + string);
      IntStream intStream = string.codePoints();
      int character = 'o';
      String newString = intStream.filter(ch -> ch != character)
            .collect(StringBuilder::new, StringBuilder::appendCodePoint, StringBuilder::append)
            .toString();
      System.out.println("New String: " + newString);
   }
}
```

📤 **Output:**

```
Input string value: Know Program
New String: Knw Prgram
```

---

## 3. Java String codePointAt() Method Example

The `codePointAt()` method of the String class returns the character (Unicode code point) at the specified index.

**codePointAt() example 1:**

```java
public class Main {
   public static void main(String[] args) {
      String string = "Know Program";
      int value = string.codePointAt(1);
      System.out.println(value);
   }
}
```

📤 **Output:**

```
110
```

**codePointAt() example 2:**

```java
public class Main {
   public static void main(String[] args) {
      String string = "Better Late than Never...";
      int string1 = string.codePointAt(20);
      System.out.println(string1);
   }
}
```

📤 **Output:**

```
101
```

> ⚠️ **Caution:** If we pass an `int` value greater than the length of the string then we will get StringIndexOutOfBoundsException.

```java
int string1 = string.codePointAt(100);
```

```
Exception in thread "main" java.lang.StringIndexOutOfBoundsException: index 100, length 25
```

---

## 4. Java String codePointBefore() Method Example

The `codePointBefore()` method of the String class returns the character (Unicode code point) before the specified index.

**codePointBefore() example:**

```java
public class Main {
   public static void main(String[] args) {
      String string = "Actions speak louder than words";
      int string1 = string.codePointBefore(1);
      System.out.println(string1);
      int string2 = string.codePointBefore(5);
      System.out.println(string2);
   }
}
```

📤 **Output:**

```
65
111
```

---

## 5. Java String codePointCount() Method Example

The `codePointCount()` method of the Java String class returns the number of Unicode code points in the specified text range of this String.

**codePointCount() example:**

```java
public class Main {
   public static void main(String[] args) {
      String string = "Actions speak louder than words";
      int value1 = string.codePointCount(1, 5);
      System.out.println(value1);
      int value2 = string.codePointCount(7, 15);
      System.out.println(value2);
   }
}
```

📤 **Output:**

```
4
8
```

---

## 6. Java String offsetByCodePoints() Method Example

Java String class `offsetByCodePoints()` method returns the index within this String that is offset from the given index by `codePointOffset` code points.

**offsetByCodePoints() example:**

```java
public class Main {
   public static void main(String[] args) {
      String string = "Actions speak louder than words";
      int value1 = string.offsetByCodePoints(1, 5);
      System.out.println(value1);
      int value2 = string.offsetByCodePoints(7, 15);
      System.out.println(value2);
   }
}
```

📤 **Output:**

```
6
22
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
- [indexOf() Method](110_Java_String_indexOf()_Method.md)
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
