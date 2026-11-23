# Java String trim() Vs strip()

**Java String trim() Vs strip()** | In this section, we will discuss the difference between `trim()` and `strip()` methods. Both are built-in methods in the [Java String class](097_String_Class_Methods_In_Java.md) but their functionalities are different.

- [Java String trim() Vs strip() Example](#java-string-trim-vs-strip-example)
- [Related Links](#related-links)

---

## 1. Overview

The [**trim() method**](122_Trim()_in_Java_String.md) removes the leading and trailing white spaces in the given string whereas the **strip() method** is Unicode charset aware - it removes the white spaces according to the Unicode specification. There are three variations in the strip method:

1. `strip()`
2. `stripLeading()`
3. `stripTrailing()`

The `strip()` method is used to remove all the white spaces in the string, the `stripLeading()` method removes all the leading spaces, and the `stripTrailing()` method removes all the spaces that are at the end of the string. Both the functions `trim()` and `strip()` are used to remove the white spaces but the major difference is that by using the `trim()` function we can't remove all the white spaces but by using `strip()` we can remove the white spaces wherever required.

| Feature | `trim()` 🅰️ | `strip()` 🅱️ |
|---------|-------------|--------------|
| **Introduced in** | Java 1.0 | Java 11 |
| **Unicode aware** | ❌️ Only ASCII (codepoint <= U+0020) | ✅ Full Unicode whitespace |
| **Handles `\u2003`** | ❌️ Cannot remove | ✅ Removes it |
| **Variants** | None | `stripLeading()`, `stripTrailing()` |

> 🔑 **Key Point:** `trim()` only considers characters with codepoint <= `U+0020` as whitespace, while `strip()` uses `Character.isWhitespace()` which covers all Unicode whitespace characters.

---

## 2. Java String trim() Vs strip() Example

Observe the output which shows the difference between `trim()` and `strip()` methods.

**Example 1 - Unicode whitespace character:**

```java
public class Main {
   public static void main(String[] args) {
      String string1 = '\u2003' + "Java";
      System.out.println("String: " + string1);
      System.out.println("String length: " + string1.length());

      String string2 = string1.trim();
      System.out.println("After using trim() function: " + string2);
      System.out.println("Length: " + string2.length());

      String string3 = string1.strip();
      System.out.println("After using strip() function: " + string3);
      System.out.println("Length: " + string3.length());
   }
}
```

📤 **Output:**

```
String:  Java
String length: 5
After using trim() function:  Java
Length: 5
After using strip() function: Java
Length: 4
```

From the above example, we can understand that `trim()` method doesn't remove the `\u2003` from the beginning of the string whereas the `strip()` method was able to remove this character from the given string. Let us see what happens if the string contains the normal space character.

**Example 2 - Mixed whitespace characters:**

```java
public class Main {
   public static void main(String[] args) {
      String string1 = "   Java   " + "\u2003\u2003\u2003";
      System.out.println("String: " + string1);
      System.out.println("String length: " + string1.length());

      String string2 = string1.trim();
      System.out.println("After using trim() function: " + string2);
      System.out.println("Length: " + string2.length());

      String string3 = string1.strip();
      System.out.println("After using strip() function: " + string3);
      System.out.println("Length: " + string3.length());
   }
}
```

📤 **Output:**

```
String: Java
String length: 13
After using trim() function: Java
Length: 10
After using strip() function: Java
Length: 4
```

The string starts with space characters and ends with `\u2003\u2003\u2003` but before this, it also contains 3 more spaces. The actual length of the string "Java" is 4. The `trim()` method removes spaces only at the beginning because string ends with the character `\u2003`. But the `strip()` method removes all whitespace and produces the result "Java".

> 💡 **Tip:** Always prefer `strip()` over `trim()` when working with Java 11+ as it handles all Unicode whitespace characters correctly.

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

---

## 3. Related Links

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
- trim() vs strip()
- valueOf() Method
