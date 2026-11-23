# String compareToIgnoreCase() Java

**String compareToIgnoreCase() Java** | Java provides the `compareToIgnoreCase()` built-in method in the String class to compare two strings lexicographically (in dictionary order) by ignoring the case.

- [String compareToIgnoreCase() Java Example](#string-comparetoignorecase-java-example)

There might be a situation where we need to compare two strings ignoring their cases. In such a situation, we can use the `compareToIgnoreCase()` method of the Java String class. The `compareToIgnoreCase()` method return type is an integer. It returns 0 if the strings are equal or else returns some other integer if the strings are not equal.

- 📈 If this string is greater than the argument string, the method returns a **positive** number.
- 📉 If this string is lesser than the argument string, the method returns a **negative** number.
- ⚖️ If this string is equal to the argument string, it returns **zero**.

| Detail 📋 | Description ⚖️ |
|-----------|---------------|
| **Method Signature** | `int compareToIgnoreCase(String str)` |
| **Parameter** | String to be compared |
| **Return Type** | `int` |

| Return Value ⚖️ | Meaning 📋 |
|-----------------|-----------|
| **0** | `str1` is equal to `str2` (ignoring case) |
| **< 0** | `str1` is less than `str2` |
| **> 0** | `str1` is greater than `str2` |

Java String class also contains [compareTo()](106_String_compareTo()_Java.md) and equals() methods to compare the strings. But there are lots of differences between these three methods.

🧠 **In Simple Words:**

- ✅ `"Hello".compareToIgnoreCase("HELLO")` => 0
- ✅ `"HeLLo".compareToIgnoreCase("hellO")` => 0
- ❌️ `"Hello".compareToIgnoreCase("Hi")` => non-zero value

---

## 1. String compareToIgnoreCase() Java Example

**Example 1 - Basic comparison:**

```java
public class Main {

   public static void main(String args[]) {
      String string1 = "Strings once declared cannot be changed";
      String string2 = "Strings once declared CANNOT BE CHANGED";
      String string3 = "Integers are one of the datatype used in Java";

      int res = string1.compareToIgnoreCase(string2);
      System.out.println(res);

      res = string2.compareToIgnoreCase(string3);
      System.out.println(res);

      res = string3.compareToIgnoreCase(string1);
      System.out.println(res);
   }
}
```

📤 **Output:**

```
0
10
-10
```

> 📝 **Note:** `string1` and `string2` contain the same data but some words are in different cases. Whereas `string3` is completely different from `string1` and `string2`. When we call `string2.compareToIgnoreCase(string3)` it returns 10 and when we reverse the argument string, we get -10.

**Example 2 - Multiple case variations:**

```java
public class Main {
   public static void main(String[] args) {
      String string1 = "java";
      String string2 = "JAVA";
      String string3 = "JAva";
      String string4 = "Jaaava";
      String string5 = "JAAAVA";

      System.out.println(string1.compareToIgnoreCase(string2));
      System.out.println(string1.compareToIgnoreCase(string3));
      System.out.println(string1.compareToIgnoreCase(string4));
      System.out.println(string1.compareToIgnoreCase(string5));
   }
}
```

📤 **Output:**

```
0
0
21
21
```

> 💡 **Tip:** Java String class contains equals(), [equalsIgnoreCase()](105_String_equalsIgnoreCase()_Java.md), [compareTo()](106_String_compareTo()_Java.md), and `compareToIgnoreCase()` methods to compare two string objects. Use one of them based on your requirement.

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

**Java Tutorial**

**[String Class Methods](097_String_Class_Methods_In_Java.md)**
- charAt() Method
- codePoints() Method
- [compareTo() Method](106_String_compareTo()_Java.md)
- compareToIgnoreCase()
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
