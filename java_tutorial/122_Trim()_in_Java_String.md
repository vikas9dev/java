# Trim() in Java String

**Trim() in Java String** | Here, we will see the `trim()` method defined in the [Java string class](097_String_Class_Methods_In_Java.md). This is a string method that omits the whitespaces in the string. The `trim()` method is present in the string class and returns the string after the removal of leading and trailing whitespace.

- [Example - Trim String In Java](#example--trim-string-in-java)
- [Java Trim All Strings In Object](#java-trim-all-strings-in-object)
- [String Trim In Java Example](#string-trim-in-java-example)

---

## 1. Example - Trim String In Java

- ✂️ `"  Java Coding Language  "` --> After `trim()` --> `"Java Coding Language"`

| Detail 📋 | Description 📝 |
|-----------|---------------|
| **Method Signature** | `public String trim()` |
| **Parameters** | None |
| **Returns** | A string whose value is this string, with all leading and trailing space removed |

**Internal implementation of the `trim()` method:**

```java
public String trim() {
   String ret = isLatin1() ? StringLatin1.trim(value)
                          : StringUTF16.trim(value);
   return ret == null ? this : ret;
}
```

**Basic `trim()` example:**

```java
public class Main {
   public static void main(String args[]) {
      String string = "  Java Programming   ";
      String newString = string.trim();
      System.out.println(newString);
   }
}
```

📤 **Output:**

```
Java Programming
```

The original string contains whitespaces. We have called the `trim()` method on the String object and it removes whitespace from the beginning and end of the string.

---

## 2. Java Trim All Strings In Object

Let us see another example of the `trim()` method of the Java String class.

**Trim with length comparison:**

```java
public class Main {
   public static void main(String[] args) {
      String str ="   Hello   Programmers   ";
      System.out.println(str.length());
      System.out.println(str);
      String str1 = str.trim();
      System.out.println(str1.length());
      System.out.println(str1);
   }
}
```

📤 **Output:**

```
25
   Hello   Programmers
19
Hello   Programmers
```

> 📝 **Note:** In the above program see the difference before using the `trim()` method and after using the `trim()` method. The length of the string before `trim()` is 25 and after using `trim()` is 19. That is, it has removed leading and trailing whitespace but the spaces **between** the words remain untouched.

Let us see another example for `String.trim()` in Java.

**Using `trim()` to check for non-whitespace content:**

```java
public class Main {

   public static void main(String argvs[]) {
      String string = " java ";
      if ((string.trim()).length() > 0) {
         System.out.println("The string contains characters other "
                           + "than white spaces");
      } else {
         System.out.println("The string contains only white spaces");
      }

      string = "   ";
      if ((string.trim()).length() > 0) {
         System.out.println("The string contains characters other "
                           + "than white spaces");
      } else {
         System.out.println("The string contains only white spaces");
      }
   }
}
```

📤 **Output:**

```
The string contains characters other than white spaces
The string contains only white spaces
```

---

## 3. String Trim In Java Example

**Hash code comparison after `trim()`:**

```java
public class Main {

   public static void main(String argvs[]) {

      String string = " java ";

      String string1 = string.trim();

      System.out.println(string.hashCode());
      System.out.println(string1.hashCode() + "\n");

      String str = "xyz";
      String str1 = str.trim();

      System.out.println(str.hashCode());
      System.out.println(str1.hashCode());

   }
}
```

📤 **Output:**

```
1017032222
3254818

119193
119193
```

> 💡 **Tip:** When the string has no leading or trailing whitespace, `trim()` returns the same string reference. Notice that `str` and `str1` have the **same hash code** because `"xyz"` has nothing to trim, so no new object is created.

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

**Java Tutorial**

**[String Class Methods](097_String_Class_Methods_In_Java.md)**
