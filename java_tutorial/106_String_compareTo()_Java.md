# String compareTo() Java

**String compareTo() Java** | In Java, two strings can be compared by using the `compareTo()` method. This method compares two strings lexicographically (in dictionary order).

- [String compareTo() Java Example](#string-compareto-java-example)
- [compareToIgnoreCase() In String Java](#comparetoignorecase-in-string-java)
- [Java String compareTo() vs equals()](#java-string-compareto-vs-equals)

Java String `compareTo()` method return type is an integer where it returns negative, positive, or 0 depending on the strings compared. If the first string is alphabetically greater than the second string then `compareTo()` returns a positive integer, if the first string is alphabetically lesser than the second string then `compareTo()` returns a negative integer, or else if the strings are equal then it returns 0.

| Detail 📋 | Description ⚖️ |
|-----------|---------------|
| **Method Signature** | `public int compareTo(String str)` |
| **Parameter** | `str` - the string to compare |
| **Return Type** | `int` |
| **Exception** | `NullPointerException` if specified object is null; `ClassCastException` if the object cannot be compared |

| Return Value ⚖️ | Meaning 📋 |
|-----------------|-----------|
| **0** | `str1` is equal to `str2` |
| **< 0** | `str1` is lexicographically less than `str2` |
| **> 0** | `str1` is lexicographically greater than `str2` |

🧠 **In Simple Words:**

- ✅ `"Hello".compareTo("Hello")` => 0
- 📈 `"Abc".compareTo("bca")` => positive (A < b in ASCII)
- 📉 `"Opl".compareTo("abc")` => negative

**How does String compareTo() work in Java?** The `compareTo()` method compares each character of the given strings based on its [Unicode value](017_Unicode_Character_Set_in_Java.md). The character sequence represented by this String object is compared lexicographically to the character sequence represented by the argument string.

---

## 1. String compareTo() Java Example

**Example 1 - Comparing multiple strings:**

```java
public class Main {
   public static void main(String args[]) {
      String str1 = "Orange";
      String str2 = "Orange";
      String str3 = "mango";
      String str4 = "Apple";
      String str5 = "lemon";
      System.out.println(str1.compareTo(str2));
      System.out.println(str1.compareTo(str3));
      System.out.println(str1.compareTo(str4));
      System.out.println(str1.compareTo(str5));
   }
}
```

📤 **Output:**

```
0
-30
14
-29
```

> 💡 **Tip:** The `str1` and `str2` contain the same strings therefore `compareTo()` returns 0. Among "Orange" and "mango" the 'O' is lesser than 'm'. The ASCII value of 'O' & 'm' is 79 & 109 respectively. When we subtract 79 - 109 it gives -30. Similarly, "Orange" vs "Apple" gives 79 - 65 = 14.

**Example 2 - Comparing with empty string:**

```java
public class Main {
   public static void main(String args[]) {
      String str1 = "apple";
      String str2 = "";
      String str3 = "apple";
      System.out.println(str1.compareTo(str2));
      System.out.println(str2.compareTo(str3));
      System.out.println(str1.compareTo(str3));
   }
}
```

📤 **Output:**

```
5
-5
0
```

---

## 2. compareToIgnoreCase() In String Java

Similar to the `compareTo()` method, the Java String class also contains the [compareToIgnoreCase() method](107_String_compareToIgnoreCase()_Java.md). It compares characters of string alphabetically without case-wise. It also returns an integer value.

**compareToIgnoreCase() example:**

```java
public class Main {
   public static void main(String args[]) {
      String str1 = "apple";
      String str2 = "Apple";
      String str3 = "apple";
      System.out.println(str1.compareToIgnoreCase(str2));
      System.out.println(str2.compareToIgnoreCase(str3));
      System.out.println(str1.compareToIgnoreCase(str3));
   }
}
```

📤 **Output:**

```
0
0
0
```

---

## 3. Java String compareTo() vs equals()

Java String class also contains the equals() method to compare the strings. But there is a lot of difference between the `compareTo()` and `equals()` methods of the Java String class.

| Feature ⚖️ | `equals()` 🅰️ | `compareTo()` 🅱️ |
|------------|--------------|-----------------|
| **Return Type** | `boolean` | `int` |
| **Equal Strings** | Returns `true` | Returns `0` |
| **Unequal Strings** | Returns `false` | Returns difference value |
| **Defined In** | `Object` class (overridden in `String`) | `String` class directly |
| **Use Case** | Equality check only | Equality + ordering |

**compareTo() vs equals() example:**

```java
public class Main {
   public static void main(String args[]) {
      String str1 = "apple";
      String str2 = "Apple";
      String str3 = "apple";

      System.out.println(str1.compareTo(str2));
      System.out.println(str1.compareTo(str3));

      System.out.println(str1.equals(str2));
      System.out.println(str1.equals(str3));
   }
}
```

📤 **Output:**

```
32
0
false
true
```

> 📝 **Note:** Java String class contains equals(), [equalsIgnoreCase()](105_String_equalsIgnoreCase()_Java.md), `compareTo()`, and [compareToIgnoreCase()](107_String_compareToIgnoreCase()_Java.md) methods to compare two string objects. Use one of them based on your requirement.

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

**Java Tutorial**

**[String Class Methods](097_String_Class_Methods_In_Java.md)**
- charAt() Method
- codePoints() Method
- compareTo() Method
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
