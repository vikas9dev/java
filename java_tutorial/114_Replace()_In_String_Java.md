# Replace() In String Java

**Replace() In String Java** | [Java string class](097_String_Class_Methods_In_Java.md) provides a `replace()` method to replace or remove unwanted strings or characters. The `replace()` method is introduced since JDK 1.5. There are two variations in `replace()` method.

- [Java replace() method Example](#java-replace-method-example)
- [Replace Method In Java](#replace-method-in-java)

---

## 1. Java replace() method Example

| Detail 📋 | Variant 1 🅰️ | Variant 2 🅱️ |
|-----------|-------------|-------------|
| **Signature** | `public String replace(char oldChar, char newChar)` | `public String replace(CharSequence target, CharSequence replacement)` |
| **Parameters** | `oldChar` - char to replace, `newChar` - replacement char | `target` - CharSequence to replace, `replacement` - new CharSequence |
| **Returns** | The replaced string | The replaced string |
| **Exception** | `NullPointerException` if target is `null` | `NullPointerException` if target is `null` |

Except for these two methods, the String class contains very similar other methods:

- 🔄 `replaceFirst(String regex, String replacement)` - Replaces only the **first occurrence** of regex in the given string. See replaceFirst().
- 🔁 `replaceAll(String regex, String replacement)` - Replaces **all occurrences** of regex in the given string. See [replaceAll()](118_String_replaceAll()_Java.md).

This program explains the first variation of the `replace()` method which takes the character as a parameter.

**Example of `replace(char oldChar, char newChar)`:**

```java
public class Main {
   public static void main(String args[]) {
      String string = "Jeve Progremming Lenguege";
      String replace = string.replace('e', 'a');
      System.out.println(replace);
   }
}
```

📤 **Output:**

```
Java Programming Languaga
```

In this `replace()` method if the given string doesn't contain the character which we want to replace, in that case it returns the reference of the string, but not the new copied string. But if the character occurs in the string then it replaces all existence of the character from the string with the new character and returns the new string.

**Identity hash code demonstration:**

```java
public class Main {
   public static void main(String args[]) {
      String str1 = "www knowprogram com";
      String replaceStr1 = str1.replace('@', '#');
      String replaceStr2 = str1.replace(' ', '.');

      System.out.println(System.identityHashCode(str1));
      System.out.println(System.identityHashCode(replaceStr1));
      System.out.println(System.identityHashCode(replaceStr2));

      str1 = "Hello";
      System.out.println(str1);
      System.out.println(replaceStr1);
      System.out.println(replaceStr2);
   }
}
```

📤 **Output:**

```
1143839598
1143839598
110718392
Hello
www knowprogram com
www.knowprogram.com
```

> 📝 **Note:** When the character to replace is not found in the string, both the original and the "replaced" string share the same identity hash code, confirming no new object was created.

---

## 2. Replace Method In Java

This program explains the `replace()` method which takes the string as a parameter.

**Example of `replace(CharSequence target, CharSequence replacement)`:**

```java
public class Main {
   public static void main(String args[]) {
      String string1 = "Java Programming Language";
      String replace = string1.replace("Program", "PROGRAM");
      System.out.println(replace);
   }
}
```

📤 **Output:**

```
Java PROGRAMming Language
```

**Replacing a character with a special character:**

```java
public class Main {
   public static void main(String args[]) {
      String string1 = "Java Programming Language";
      String replace = string1.replace("a", "@");
      System.out.println(replace);
   }
}
```

📤 **Output:**

```
J@v@ Progr@mming L@ngu@ge
```

This `replace()` method replaces from the beginning to the end of the string. Let us understand it through an example.

**Left-to-right replacement behavior:**

```java
public class Main {
   public static void main(String args[]) {
      String string1 = "Brrrh";
      String replace = string1.replace("rr", "@");
      System.out.println(replace);
   }
}
```

📤 **Output:**

```
B@rh
```

> 💡 **Tip:** Since `replace()` replaces from the beginning to the end of the string, the result is `B@rh` but not `Br@h`. The first match of `"rr"` starting at index 1 is replaced, leaving the remaining `"rh"` untouched.

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

**Java Tutorial**

**[String Class Methods](097_String_Class_Methods_In_Java.md)**
