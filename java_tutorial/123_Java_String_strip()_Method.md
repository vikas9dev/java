# Java String strip() Method

**Java String strip() Method** | The `strip()` method of the [Java String class](097_String_Class_Methods_In_Java.md) is used to remove leading and trailing spaces in the string. It can remove all unwanted spaces. The three variations of this method are shown below.

- [Java String strip() Method Example](#java-string-strip-method-example)
- [Java String stripLeading() Method Example](#java-string-stripleading-method-example)
- [Java String stripTrailing() Method Example](#java-string-striptrailing-method-example)

---

## 1. Java String strip() Method Example

| Variant 🏷️ | Signature 📋 | Behavior 📝 |
|------------|-------------|------------|
| **`strip()`** | `public String strip()` | Removes whitespace at **both** start and end |
| **`stripLeading()`** | `public String stripLeading()` | Removes whitespace at the **start** only |
| **`stripTrailing()`** | `public String stripTrailing()` | Removes whitespace at the **end** only |

Below are the examples for all three variations of String Strip Java:

- ✂️ `" Hello people good evening "` --> `strip()` --> `"Hello people good evening"` (removes both leading and trailing)
- ✂️ `" Hey this is Java programming language "` --> `stripLeading()` --> `"Hey this is Java programming language "` (removes only leading)
- ✂️ `" Strip method has three variants "` --> `stripTrailing()` --> `" Strip method has three variants"` (removes only trailing)

Now let us see an example of the Java string class **`strip()`** method to understand the working of the `strip()` method.

**`strip()` method example:**

```java
public class Main {
   public static void main(String[] args) {
      String string = "   Know Program   ";
      System.out.println("Input string length: " + string.length());
      String str = string.strip();
      System.out.println("Resultant string: \"" + str + "\"");
      System.out.println("Stripped string length: " + str.length());
   }
}
```

📤 **Output:**

```
Input string length: 18
Resultant string: "Know Program"
Stripped string length: 12
```

> 📝 **Note:** The `strip()` method removed both leading and trailing white spaces but it doesn't remove the spaces between the words.

---

## 2. Java String stripLeading() Method Example

This example shows the working of the leading strip.

**`stripLeading()` method example:**

```java
public class Main {
   public static void main(String[] args) {
      String string = "   Know Program   ";
      System.out.println("Input string length: " + string.length());
      String str = string.stripLeading();
      System.out.println("Resultant string: \"" + str + "\"");
      System.out.println("Stripped string length: " + str.length());
   }
}
```

📤 **Output:**

```
Input string length: 18
Resultant string: "Know Program   "
Stripped string length: 15
```

---

## 3. Java String stripTrailing() Method Example

This method shows the working of the trailing strip.

**`stripTrailing()` method example:**

```java
public class Main {
   public static void main(String[] args) {
      String string = "   Know Program   ";
      System.out.println("Input string length: " + string.length());
      String str = string.stripTrailing();
      System.out.println("Resultant string: \"" + str + "\"");
      System.out.println("Stripped string length: " + str.length());
   }
}
```

📤 **Output:**

```
Input string length: 18
Resultant string: "   Know Program"
Stripped string length: 15
```

> 💡 **Tip:** The `strip()` method (introduced in Java 11) is Unicode-aware and removes all Unicode whitespace characters, whereas `trim()` only removes characters with code points less than or equal to `U+0020` (space). Prefer `strip()` for modern Java applications.

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

**Java Tutorial**

**[String Class Methods](097_String_Class_Methods_In_Java.md)**
