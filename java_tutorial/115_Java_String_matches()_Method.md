# Java String matches() Method

**Java String matches() Method** | The `matches()` method of the [Java string class](097_String_Class_Methods_In_Java.md) is used to **check whether the given string matches the substring or not**. It basically works on regular expressions. We give some regular expressions as a parameter to the `matches()` method and it checks for the same word in the string.

- [Java String matches() Method Example](#java-string-matches-method-example)
- [Java Matching Strings](#java-matching-strings)
- [Java Match Character In String](#java-match-character-in-string)

---

## 1. Java String matches() Method Example

📝 **Note:** In regular expressions, `.` represents any/all characters, `^` represents the starting of the string, `$` represents the ending of the string, and `+` means one or more times.

- 🔍 **Example-1:** `String1 = "APply"`, `String2 = "AP..y"` --> `true`. String1 starts with "AP", ends with "y", and has two characters in-between.
- 🔍 **Example-2:** `String1 = "KP"`, `String2 = "^K"` --> `true`. The string1 starts with 'K'.
- 🔍 **Example-3:** `String1 = "Man"`, `String2 = "n$"` --> `true`. The string1 ends with 'n'.
- ❌️ **Example-4:** `String1 = "Monkey"`, `String2 = "^o"` --> `false`. The string1 starts with 'M' but not with 'o'.

| Detail 📋 | Description 📝 |
|-----------|---------------|
| **Method Signature** | `public boolean matches(String regex)` |
| **Parameters** | `regex` - the regular expression which needs to be matched |
| **Return Type** | `boolean` |
| **Returns** | `true` if the regex matches, `false` otherwise |

**Basic `matches()` example:**

```java
public class Main {
   public static void main(String[] args) {
      String str = "^J..a$";
      System.out.println("Java".matches(str));
   }
}
```

📤 **Output:**

```
true
```

In the above string, we are searching for the character 'J' in the first and character 'a' in the last. There can be any two characters in between 'J' and 'a'. Hence the given string matches the regular expression.

---

## 2. Java Matching Strings

**Checking if string contains a substring using regex:**

```java
public class Main {
   public static void main(String args[]) {
      String string = new String("Java Programming Language");
      System.out.print("Does string contains regex:- (.*)Java(.*)?: ");
      System.out.println(string.matches("(.*)Java(.*)"));
   }
}
```

📤 **Output:**

```
Does string contains regex (.*)Java(.*) ? : true
```

It will check whether the string contains "Java" or not. There can be any character any number of times before or after the "Java" sub-string. The given string matches this regular expression therefore it gives the result `true`.

---

## 3. Java Match Character In String

**Checking if string contains only digits:**

```java
public class Main {
   public static void main(String[] args) {
      String str = "^[1-9]+$";
      System.out.println("a123".matches(str));
      System.out.println("98416".matches(str));
      System.out.println("98 41".matches(str));
   }
}
```

📤 **Output:**

```
false
true
false
```

The given regular expression checks whether the string contains only digits 0-9 or not. The first and third strings don't match the regular expression therefore `matches()` returns `false` for them. Whereas for the second string `matches()` method returns `true`.

> 💡 **Tip:** The `matches()` method checks if the **entire string** matches the regex. If you want to check for a partial match, use `Pattern` and `Matcher` classes from `java.util.regex` package.

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

**Java Tutorial**

**[String Class Methods](097_String_Class_Methods_In_Java.md)**
