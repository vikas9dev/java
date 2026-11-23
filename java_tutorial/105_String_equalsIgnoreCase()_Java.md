# String equalsIgnoreCase() Java

**String equalsIgnoreCase() Java** | The `equalsIgnoreCase()` is a built-in method in the Java String class that compares two strings irrespective of their cases, i.e. even if the string cases are different, the cases will be ignored during the comparison.

- [Java String equalsIgnoreCase()](#java-string-equalsignorecase)
- [Example of String equalsIgnoreCase() In Java](#example-of-string-equalsignorecase-in-java)
- [equalsIgnoreCase() Method of String Java Example](#equalsignorecase-method-of-string-java-example)

It is the same as the equals() method of the String class. The `equalsIgnoreCase()` method is **not** case sensitive whereas the `equals()` method **is** case sensitive. The `equals()` method compares with the case but `equalsIgnoreCase()` compares ignoring the case.

Similar to the `equals()` method, `equalsIgnoreCase()` also has a boolean return type. It returns `true` if the strings are equal else `false` if the strings are not equal.

🧠 **In Simple Words:**

- ✅ `"REPEAT".equalsIgnoreCase("repeat")` => `true`
- ✅ `"null".equalsIgnoreCase("nULl")` => `true`
- ❌️ `"bored".equalsIgnoreCase("boring")` => `false`

---

## 1. Java String equalsIgnoreCase()

| Detail 📋 | Description ⚖️ |
|-----------|---------------|
| **Method Signature** | `public boolean equalsIgnoreCase(String anotherString)` |
| **Parameter** | `anotherString` - The string to compare with |
| **Return Value** | `true` if equivalent ignoring case; `false` otherwise |

**Internal implementation of Java String equalsIgnoreCase():**

```java
public boolean equalsIgnoreCase(String anotherString) {
   return (this == anotherString) ? true
      : (anotherString != null)
      && (anotherString.length() == length())
      && regionMatches(true, 0, anotherString, 0, length());
}
```

---

## 2. Example of String equalsIgnoreCase() In Java

Now let us see some programs to understand the String `equalsIgnoreCase()` method working principle. We will take multiple strings and compare them using the `equalsIgnoreCase()` method.

**Example 1 - Basic comparison:**

```java
public class Main {
   public static void main(String[] args) {
      String str1 = "angry bird";
      String str2 = "ANGRY BIRD";
      String str3 = "bird angry";

      boolean res1 = str2.equalsIgnoreCase(str1);
      System.out.println("str2 is equal to str1 = " + res1);

      boolean res2 = str2.equalsIgnoreCase(str3);
      System.out.println("str2 is equal to str3 = " + res2);
   }
}
```

📤 **Output:**

```
str2 is equal to str1 = true
str2 is equal to str3 = false
```

> 📝 **Note:** With respect to content, `str1` and `str2` contain the same characters but one is in uppercase and one is in lowercase. Since `equalsIgnoreCase()` ignores the cases while comparison, it returns `true`. But `str2` and `str3` are completely different from each other hence `equalsIgnoreCase()` returns `false`.

**Example 2 - Multiple case variations:**

```java
public class Main {
   public static void main(String args[]) {
      String str1 = "hello world";
      String str2 = "Hello WORLD";
      String str3 = "HeLlO WOrlD";
      String str4 = "JAVA";

      System.out.println(str1.equalsIgnoreCase(str2));
      System.out.println(str1.equalsIgnoreCase(str3));
      System.out.println(str1.equalsIgnoreCase(str4));
   }
}
```

📤 **Output:**

```
true
true
false
```

---

## 3. equalsIgnoreCase() Method of String Java Example

We have a list of strings, and we want to check whether the list contains a given string (ignoring the case) or not. To check whether a list contains a given object, `contains()` method is given, but it compares with the case. For string objects, if we want to compare by ignoring the case then we have to use the `equalsIgnoreCase()` method.

**List search with case-insensitive comparison:**

```java
import java.util.ArrayList;
public class Main{
   public static void main(String[] args) {
      ArrayList<String> list = new ArrayList<>();
      list.add("Happy");
      list.add("sad");
      list.add("angry");
      list.add("fear");

      String string1 = "ANGRY";
      System.out.println(list.contains(string1));

      boolean exist = false;
      for (String string : list) {
         if (string.equalsIgnoreCase(string1)) {
            exist = true;
            break;
         }
      }

      if(exist) {
       System.out.println("List contains given string");
      } else {
       System.out.println("List doesn't contain given string");
      }
   }
}
```

📤 **Output:**

```
false
List contains given string
```

> 💡 **Tip:** Apart from equals() and `equalsIgnoreCase()`, Java String class also contains [compareTo()](106_String_compareTo()_Java.md) and [compareToIgnoreCase()](107_String_compareToIgnoreCase()_Java.md) methods. We can use any of these methods to compare two string objects based on our requirement.

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
- equalsIgnoreCase()
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
