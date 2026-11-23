# Java String equals() Method

**Java String equals() Method** | The `equals()` method of the String class is used to compare two strings. It returns `true` if both strings are content-wise equal and returns `false` if the given strings are not equal.

- [Java String equals() Method Example](#java-string-equals-method-example)
- [How To Check If Two Strings Are Equal In Java](#how-to-check-if-two-strings-are-equal-in-java)
- [How To Compare Two Strings In Java Without Using equals()](#how-to-compare-two-strings-in-java-without-using-equals)

The equals() method is mainly defined in the [Java Object class](069_Object_Class_in_Java.md), and it compares objects based on their reference. If we want to compare objects based on their content/data then we have to override the `equals()` method in our class. Java String class also follows the concept and overrides `equals()` method to compare strings content or data-wise.

Whereas [StringBuilder and StringBuffer](133_When_To_Use_StringBuffer_And_StringBuilder_In_Java.md) do not override the `equals()` method hence their objects are compared based on the reference. We have discussed it in detail in the Object class equals() method.

| Detail 📋 | Description ⚖️ |
|-----------|---------------|
| **Method Signature** | `public boolean equals(Object object)` |
| **Parameter** | A string that needs to be compared |
| **Return Type** | `boolean` (`true` or `false`) |

🧠 **In Simple Words:**

- ✅ `"Hey".equals("Hey")` => `true` (same content)
- ❌️ `"Hey".equals("Hi")` => `false` (different content)

---

## 1. Java String equals() Method Example

**Basic equals() comparison:**

```java
public class Main {
   public static void main(String args[]) {
      String str1 = "Java Programming";
      String str2 = "Java Programming";
      String str3 = "JAVA PROGRAMMING";
      String str4 = "Java";

      System.out.println(str1.equals(str2));
      System.out.println(str1.equals(str3));
      System.out.println(str1.equals(str4));
   }
}
```

📤 **Output:**

```
true
false
false
```

Not only two strings, but we can also compare strings with other objects but in that case, we will always get the result `false` because they are different objects and are not comparable with strings.

**Comparing string with other objects:**

```java
public class Main {
   public static void main(String args[]) {
      String string = "KnowProgram";
      StringBuilder sb = new StringBuilder("KnowProgram");
      StringBuffer sbf = new StringBuffer("KnowProgram");
      Main main = new Main();

      System.out.println(string.equals(sb));
      System.out.println(string.equals(sbf));
      System.out.println(string.equals(main));
   }
}
```

📤 **Output:**

```
false
false
false
```

> 📝 **Note:** The `equals()` method of the String class checks if the passed object is an instance of `String`. Since `StringBuilder`, `StringBuffer`, and custom objects are not `String` instances, the result is always `false`.

---

## 2. How To Check If Two Strings Are Equal In Java

There are multiple ways to check if two strings are equal in Java. Java String class contains `equals()`, [equalsIgnoreCase()](105_String_equalsIgnoreCase()_Java.md), [compareTo()](106_String_compareTo()_Java.md), and [compareToIgnoreCase()](107_String_compareToIgnoreCase()_Java.md) methods. But using the `equals()` method to check string equality in Java will be the easy and appropriate way.

**String equality check:**

```java
public class Main {
   public static void main(String[] args) {

      String str1 = "Know Program";
      String str2 = "Know Program";
      String str3 = "knowprogram";

      System.out.println(str1.equals(str2));

      if (str1.equals(str3)) {
         System.out.println("Both strings are equal");
      } else {
         System.out.println("Both strings are not equal");
      }
   }
}
```

📤 **Output:**

```
true
Both strings are not equal
```

---

## 3. How To Compare Two Strings In Java Without Using equals()

If we want to compare two strings without using the `equals()` method then we can use the [compareTo() method](106_String_compareTo()_Java.md). The `equals()` method returns a boolean value whereas `compareTo()` returns 0 if both strings are equal, or else returns the difference between the first unmatched characters.

**Using compareTo() instead of equals():**

```java
public class Main {
   public static void main(String[] args) {
      String str1 = "Know Program";
      String str2 = "Know Program";
      String str3 = "knowprogram";

      if (str1.compareTo(str2) == 0) {
         System.out.println("Strings str1 & str2 are equal");
      } else {
         System.out.println("Strings str1 & str2 are not equal");
      }

      if (str1.compareTo(str3) == 0) {
         System.out.println("Strings str1 & str3 are equal");
      } else {
         System.out.println("Strings str1 & str3 are not equal");
      }
   }
}
```

📤 **Output:**

```
Strings str1 & str2 are equal
Strings str1 & str3 are not equal
```

> 💡 **Tip:** Use `equals()` when you only need a `true`/`false` result. Use `compareTo()` when you also need to know the ordering relationship between strings.

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
