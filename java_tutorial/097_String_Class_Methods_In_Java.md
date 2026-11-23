# String Class Methods In Java

**String Class Methods In Java** | The `java.lang.String` class given in Java programming language contains many built-in methods for string manipulation and string handling. In this blog, we will discuss those string class methods in Java with examples. If you want to be a good Java programmer then String class methods are essential and they will help you a lot while coding.

- [Length, charAt, indexOf, lastIndexOf](#length-charat-indexof-lastindexof)
- [isEmpty, isBlank, contains, startsWith, endsWith](#isempty-isblank-contains-startswith-endswith)
- [hashCode, toString, equals, compareTo](#hashcode-tostring-equals-compareto)
- [getChars, getBytes, toCharArray, substring](#getchars-getbytes-tochararray-substring)
- [join, concat, repeat](#join-concat-repeat)
- [replace, replaceFirst, replaceAll](#replace-replacefirst-replaceall)
- [split, toUpperCase, toLowerCase](#split-touppercase-tolowercase)
- [trim, strip, stripLeading, stripTrailing](#trim-strip-stripleading-striptrailing)
- [valueOf, format, copyValueOf](#valueof-format-copyvalueof)
- [codePoints, codePointAt, codePointBefore](#codepoints-codepointat-codepointbefore)
- [Other String Methods](#other-string-methods)
- [Related Links](#related-links)

---

## 1. Length, charAt, indexOf, lastIndexOf

String class methods in Java to find the length, fetch the character at some given index, finding the index of the given characters are as follows:

| Method 🏷️ | Description 📋 |
|-----------|----------------|
| [int **length()**](099_How_to_Find_Length_of_String_in_Java.md) | Returns the length of the given string. |
| char **charAt(int index)** | Returns character at the given index. |
| [int **indexOf(-)**](110_Java_String_indexOf()_Method.md) | Gives the first index of a given character or string either from start or from the given position. |
| [int **lastIndexOf(-)**](111_String_lastIndexOf()_in_Java.md) | Gives the last index of a given character or string either from start or from the given position. |

There are many variations of [indexOf()](110_Java_String_indexOf()_Method.md) and [lastIndexOf()](111_String_lastIndexOf()_in_Java.md) methods. The four overloaded forms of the `indexOf()` methods are:

- `public int indexOf(int ch)`
- `public int indexOf(int ch, int fromIndex)`
- `public int indexOf(String str)`
- `public int indexOf(String str, int fromIndex)`

The four overloaded forms of the [lastIndexOf() methods](111_String_lastIndexOf()_in_Java.md) are:

- `public int lastIndexOf(int ch)`
- `public int lastIndexOf(int ch, int fromIndex)`
- `public int lastIndexOf(String str)`
- `public int lastIndexOf(String str, int fromIndex)`

**Demonstration of length, charAt, indexOf, lastIndexOf:**

```java
public class Main {
    public static void main(String[] args) {

        String string = "Hello World";
        System.out.println(string.length()); // 11

        System.out.println(string.charAt(0)); // 'H'
        System.out.println(string.charAt(6)); // 'W'

        System.out.println(string.indexOf('l')); // 2
        System.out.println(string.indexOf('l', 5)); // 9

        System.out.println(string.lastIndexOf('o')); // 7
        System.out.println(string.lastIndexOf('o', 5)); // 4
    }
}
```

📤 **Output:**

```
11
H
W
2
9
7
4
```

---

## 2. isEmpty, isBlank, contains, startsWith, endsWith

String class methods in Java to check whether a string is empty, blank, contains some character, starts or ends with some specific character/string, or not.

| Method 🏷️ | Description 📋 |
|-----------|----------------|
| [boolean **isEmpty()**](100_String_isEmpty()_Java_with_Examples.md) | Returns `true` if, and only if, [length()](099_How_to_Find_Length_of_String_in_Java.md) is 0. |
| [boolean **isBlank()**](124_String_isBlank()_Java_with_Examples.md) | It returns `true` if the string is empty or contains only white space codepoints, otherwise returns `false`. |
| [boolean **contains**(CharSequence s)](116_String_contains()_Method_in_Java.md) | Returns `true` if and only if this string contains the specified sequence of char values. |
| boolean **startsWith**(String prefix) | Test if this string starts with the specified prefix. |
| boolean **startsWith**(String prefix, int toffset) | Tests if the substring of this string beginning at the specified index starts with the specified prefix. |
| boolean **endsWith**(String suffix) | Test if this string ends with the specified suffix. |

**Program to demonstrate String class methods in Java:**

```java
public class Main {
    public static void main(String[] args) {
        String string = "Know Program";
        System.out.println(string.isEmpty()); // false
        System.out.println(string.isBlank()); // false

        System.out.println(string.startsWith("K")); // true
        System.out.println(string.startsWith("m")); // false
        System.out.println(string.startsWith("Know")); // true
        System.out.println(string.startsWith("Program")); // false

        System.out.println(string.endsWith("K")); // false
        System.out.println(string.endsWith("m")); // true
        System.out.println(string.endsWith("Know")); // false
        System.out.println(string.endsWith("Program")); // true
    }
}
```

📤 **Output:**

```
false
false
true
false
true
false
false
true
false
true
```

The `isBlank()` vs `isEmpty()` methods of the Java String class may look very similar but there are some major differences between them. See more here: isBlank() vs isEmpty() in Java String, [StringUtils isEmpty() Vs isBlank()](160_StringUtils_isEmpty()_Vs_isBlank().md)

---

## 3. hashCode, toString, equals, compareTo

Like any other classes in Java, `String` is also a child class of [java.lang.Object class](069_Object_Class_in_Java.md). And string class overrides some methods of the Object class like `hashCode()`, `toString()`, and `equals()` methods.

| Method 🏷️ | Description 📋 |
|-----------|----------------|
| int **hashCode()** | Returns a hash code for this string. |
| [String **toString()**](126_String_toString()_Java.md) | Return the string itself. |
| boolean **equals**(Object anObject) | Compares this string to the specified object. The result is `true` if and only if the argument is not `null` and is a String object that represents the same sequence of characters as this object. |
| [boolean **equalsIgnoreCase**(String anotherString)](105_String_equalsIgnoreCase()_Java.md) | Same as the above `equals()` method, ignoring case considerations. |
| [int **compareTo()**](106_String_compareTo()_Java.md) | Compares two strings lexicographically. |
| [int **compareToIgnoreCase()**](107_String_compareToIgnoreCase()_Java.md) | Compares two strings lexicographically, ignoring case considerations. |
| boolean **contentEquals**(StringBuffer sb) | Compares this string to the specified StringBuffer. |
| boolean **contentEquals**(CharSequence cs) | Compares this string to the specified CharSequence. |

**hashCode and toString demonstration:**

```java
public class Main {
    public static void main(String[] args) {
        String str1 = "Know Program";
        String str2 = "Hello World!";

        System.out.println(str1.hashCode());
        System.out.println(str2.hashCode());

        System.out.println(str1.toString());
        System.out.println(str2.toString());
    }
}
```

📤 **Output:**

```
1608858095
-969099747
Know Program
Hello World!
```

**equals and compareTo demonstration:**

```java
public class Main {
    public static void main(String[] args) {

        String str1 = "Know Program";
        String str2 = "know program";
        String str3 = "KP";

        System.out.println(str1.equals(str2));
        System.out.println(str1.equals(str3));
        System.out.println(str1.equalsIgnoreCase(str2));
        System.out.println(str1.equalsIgnoreCase(str3));

        System.out.println(str1.compareTo(str2));
        System.out.println(str1.compareTo(str3));
        System.out.println(str1.compareToIgnoreCase(str2));
        System.out.println(str1.compareToIgnoreCase(str3));
    }
}
```

📤 **Output:**

```
false
false
true
false
-32
30
0
-2
```

**contentEquals demonstration:**

```java
public class Main {
    public static void main(String[] args) {
        String str = "Know Program";
        StringBuffer sb = new StringBuffer("Know Program");
        CharSequence cs = new StringBuilder("Know Program");
        System.out.println(str.contentEquals(sb));
        System.out.println(str.contentEquals(cs));
    }
}
```

📤 **Output:**

```
true
true
```

---

## 4. getChars, getBytes, toCharArray, substring

| Method 🏷️ | Description 📋 |
|-----------|----------------|
| void **getChars**(int srcBegin, int srcEnd, char dst[], int dstBegin) | Copies characters from this string into the destination character array. |
| byte[] **getBytes**(String charsetName) | Encodes this String into a sequence of bytes using the named charset, storing the result into a new byte array. |
| byte[] **getBytes**(Charset charset) | Encodes this String into a sequence of bytes using the given charset, storing the result into a new byte array. |
| char[] **toCharArray()** | Converts this string to a new character array. |
| [String **substring**(int beginIndex)](112_Substring_Method_In_Java.md) | Returns a string that is a substring of this string. |
| String **substring**(int beginIndex, int endIndex) | Returns a string that is a substring of this string. |
| CharSequence **subSequence**(int beginIndex, int endIndex) | Returns a character sequence that is a subsequence of this sequence. |

**getChars demonstration:**

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        String str = "Know Program";
        char[] ch = new char[str.length()];

        str.getChars(0, str.length(), ch, 0);
        System.out.println(Arrays.toString(ch));
    }
}
```

📤 **Output:**

```
[K, n, o, w, , P, r, o, g, r, a, m]
```

**getBytes demonstration:**

```java
import java.io.UnsupportedEncodingException;
import java.nio.charset.StandardCharsets;
import java.util.Arrays;

public class Main {
    public static void main(String[] args) throws UnsupportedEncodingException {
        String string = "Know Program";

        byte[] byteArray1 = string.getBytes("UTF-16");
        System.out.println(Arrays.toString(byteArray1));

        byte[] arrayUTF8 = string.getBytes(StandardCharsets.UTF_8);
        System.out.println(Arrays.toString(arrayUTF8));
    }
}
```

📤 **Output:**

```
[-2, -1, 0, 75, 0, 110, 0, 111, 0, 119, 0, 32, 0, 80, 0, 114, 0, 111, 0, 103, 0, 114, 0, 97, 0, 109]
[75, 110, 111, 119, 32, 80, 114, 111, 103, 114, 97, 109]
```

**toCharArray demonstration:**

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        String string = "Know Program";
        char[] charArray = string.toCharArray();
        System.out.println(Arrays.toString(charArray));
    }
}
```

📤 **Output:**

```
[K, n, o, w, , P, r, o, g, r, a, m]
```

**substring and subSequence demonstration:**

```java
public class Main {
    public static void main(String[] args) {
        String string = "Know Program";
        System.out.println(string.substring(5));
        System.out.println(string.substring(5, 8));
        System.out.println(string.subSequence(8, string.length()));
    }
}
```

📤 **Output:**

```
Program
Pro
gram
```

---

## 5. join, concat, repeat

String class methods in Java to join or concatenate strings together or repeat some string multiple times are as follows:

| Method 🏷️ | Description 📋 |
|-----------|----------------|
| [String **join**(CharSequence delimiter, CharSequence... elements)](098_String_join()_In_Java.md) | Returns a new String composed of copies of the CharSequence elements joined together with a copy of the specified delimiter. |
| String **join**(CharSequence delimiter, Iterable<? extends CharSequence> elements) | Returns a new String composed of copies of the CharSequence elements joined together with a copy of the specified delimiter. |
| [String **concat**(String str)](113_Concat_Strings_in_Java.md) | Concatenates the specified string to the end of this string. |
| String **repeat**(int count) | Returns a string whose value is the concatenation of this string repeated count times. |

**join, concat, and repeat demonstration:**

```java
public class Main {
    public static void main(String args[]) {
        String string = String.join(".", "www", "knowprogram", "com");
        System.out.println(string);

        String string1 = "Know".concat("Program");
        System.out.println(string1);

        String string2 = "www".concat(".")
                              .concat("knowprogram")
                              .concat(".")
                              .concat("com");
        System.out.println(string2);

        String string3 = "Hi".repeat(3);
        System.out.println(string3);
    }
}
```

📤 **Output:**

```
www.knowprogram.com
KnowProgram
www.knowprogram.com
HiHiHi
```

---

## 6. replace, replaceFirst, replaceAll

String class methods to replace or remove some character or substring from the given string is as follows:

| Method 🏷️ | Description 📋 |
|-----------|----------------|
| [String **replace**(char oldChar, char newChar)](114_Replace()_In_String_Java.md) | Returns a string resulting from replacing all occurrences of oldChar in this string with newChar. |
| String **replaceFirst**(String regex, String replacement) | Replaces the first substring of this string that matches the given regular expression with the given replacement. |
| [String **replaceAll**(String regex, String replacement)](118_String_replaceAll()_Java.md) | Replaces each substring of this string that matches the given regular expression with the given replacement. |

Both `replace()` and `replaceAll()` methods seem to replace all occurrences but they are different from each other. See the difference between replace() and replaceAll() methods in Java. Let us see an example of it.

**replace, replaceFirst, and replaceAll demonstration:**

```java
public class Main {
    public static void main(String args[]) {
        String string = "Hello World";

        String string1 = string.replace('l', '@');
        System.out.println(string1);

        String string2 = string.replaceFirst("l", "#");
        System.out.println(string2);

        String string3 = string.replaceAll("o", "9");
        System.out.println(string3);
    }
}
```

📤 **Output:**

```
He@@o Wor@d
He#lo World
Hell9 W9rld
```

---

## 7. split, toUpperCase, toLowerCase

| Method 🏷️ | Description 📋 |
|-----------|----------------|
| [String[] **split**(String regex)](119_Split()_Method_In_Java.md) | Splits this string around matches of the given regular expression. |
| String[] **split**(String regex, int limit) | Splits this string around matches of the given regular expression. |
| String **toUpperCase()** | Converts all of the characters in this String to upper case using the rules of the default locale. |
| String **toUpperCase**(Locale locale) | Converts all of the characters in this String to upper case using the rules of the given Locale. |
| [String **toLowerCase()**](120_Java_String_to_Lowercase.md) | Converts all of the characters in this String to lowercase using the rules of the default locale. |
| String **toLowerCase**(Locale locale) | Converts all of the characters in this String to lower case using the rules of the given Locale. |

**split, toUpperCase, and toLowerCase demonstration:**

```java
import java.util.Arrays;

public class Main {
    public static void main(String args[]) {
        String string = "Hi How are you?";

        String[] array1 = string.split(" ");
        System.out.println(Arrays.toString(array1));

        String[] array2 = string.split(" ", 2);
        System.out.println(Arrays.toString(array2));

        System.out.println(string.toUpperCase());
        System.out.println(string.toLowerCase());
    }
}
```

📤 **Output:**

```
[Hi, How, are, you?]
[Hi, How are you?]
HI HOW ARE YOU?
hi how are you?
```

---

## 8. trim, strip, stripLeading, stripTrailing

| Method 🏷️ | Description 📋 |
|-----------|----------------|
| [String **trim()**](122_Trim()_in_Java_String.md) | Returns a string whose value is this string, with all leading and trailing space removed, where space is defined as any character whose codepoint is less than or equal to `U+0020` (the space character). |
| String **strip()** | Returns a string whose value is this string, with all leading and trailing white space removed. |
| String **stripLeading()** | Returns a string whose value is this string, with all leading white space removed. |
| String **stripTrailing()** | Returns a string whose value is this string, with all trailing white space removed. |
| String **stripIndent()** | Returns a string whose value is this string, with incidental white space removed from the beginning and end of every line. |

We have discussed strip(), stripLeading(), stripTrailing(), and stripIndent() in detail. Also, see the [difference between the trim() and strip() methods in Java](093_Java_String_trim()_Vs_strip().md). Let us see an example of the above methods.

**trim, strip, stripLeading, and stripTrailing demonstration:**

```java
public class Main {
    public static void main(String args[]) {
        String string = "  Hi How are you?    ";
        System.out.println("Original length: " + string.length());

        String str1 = string.trim();
        System.out.println(str1.length());

        String str2 = string.strip();
        System.out.println(str2.length());

        String str3 = string.stripLeading();
        System.out.println(str3.length());

        String str4 = string.stripTrailing();
        System.out.println(str4.length());

        String str5 = string.stripIndent();
        System.out.println(str5.length());
    }
}
```

📤 **Output:**

```
Original length: 21
15
15
19
17
15
```

---

## 9. valueOf, format, copyValueOf

| Method 🏷️ | Description 📋 |
|-----------|----------------|
| static String **valueOf(-)** | Returns the string representation of the given argument. |
| static String **copyValueOf**(char data[]) | Equivalent to `valueOf(char[])`. |
| static String **copyValueOf**(char data[], int offset, int count) | Equivalent to `valueOf(char[], int, int)`. |
| static String **format**(String format, Object... args) | Returns a formatted string using the specified format string and arguments. |
| static String **format**(Locale l, String format, Object... args) | Returns a formatted string using the specified locale, format string, and arguments. |
| String **formatted**(Object... args) | Formats using this string as the format string, and the supplied arguments. |

There are many overloaded forms of valueOf() method which is used to convert primitive, char arrays and objects to String format. The `format()` method is very similar to Java `printf()` method, and C language `printf()` method. We have discussed the String.format() method with examples in detail.

**valueOf demonstration:**

```java
public class Main {
    public static void main(String args[]) {
        int num = 10;
        System.out.println(String.valueOf(num));
        System.out.println(String.valueOf(99.999));
        System.out.println(String.valueOf(true));
        System.out.println(String.valueOf(new char[] { 'K', 'n', 'o', 'w' }));
    }
}
```

📤 **Output:**

```
10
99.999
true
Know
```

---

## 10. codePoints, codePointAt, codePointBefore

String class methods for codePoints(), codePointAt(), codePointBefore(), codePointCount(), and offsetByCodePoints():

| Method 🏷️ | Description 📋 |
|-----------|----------------|
| public IntStream **codePoints()** | Returns a stream of code point values from this sequence. |
| public int **codePointAt(int index)** | Returns the character (Unicode code point) at the specified index. |
| public int **codePointBefore(int index)** | Returns the character (Unicode code point) before the specified index. |
| public int **codePointCount**(int beginIndex, int endIndex) | Returns the number of Unicode code points in the specified text range of this String. |
| public int **offsetByCodePoints**(int index, int codePointOffset) | Returns the index within this String that is offset from the given index by codePointOffset code points. |

---

## 11. Other String Methods

| Method 🏷️ | Description 📋 |
|-----------|----------------|
| Stream<String> **lines()** | Returns a stream of lines extracted from this string, separated by line terminators. |
| String **indent(int n)** | Adjusts the indentation of each line of this string based on the value of n, and normalizes line termination characters. |
| String **translateEscapes()** | Returns a string whose value is this string, with escape sequences translated as if in a string literal. |
| <R> R **transform**(Function<? super String, ? extends R> f) | This method allows the application of a function to this string. The function should expect a single String argument and produce an R result. |
| IntStream **chars()** | Returns a stream of int zero-extending the char values from this sequence. Any char which maps to a surrogate codepoint is passed through uninterpreted. |
| String **intern()** | Returns a canonical representation for the string object. |
| Optional<String> **describeConstable()** | Returns an Optional containing the nominal descriptor for this instance, which is the instance itself. |
| String **resolveConstantDesc**(MethodHandles.Lookup lookup) | Resolves this instance as a ConstantDesc, the result of which is the instance itself. |
| boolean **matches**(String regex) | Tells whether or not this string matches the given regular expression. |
| boolean **regionMatches**(int toffset, String other, int ooffset, int len) | Test if two string regions are equal. |
| boolean **regionMatches**(boolean ignoreCase, int toffset, String other, int ooffset, int len) | Test if two string regions are equal. |

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

---

## 12. Related Links

**Java Tutorial**

**String Class Methods**
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
