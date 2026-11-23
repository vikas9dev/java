# Java String replaceFirst() Method

**Java String replaceFirst() Method** | The `replaceFirst()` method is a built-in method in Java that enables us to **replace the first occurrence of the given regular expression which can be a character or a substring**. In some cases there might be a situation where we need to change only one occurrence of the character, and in that case we can use the `replaceFirst()` method.

- [Java String replaceFirst() Example](#java-string-replacefirst-example)
- [Regex Replacement with replaceFirst()](#regex-replacement-with-replacefirst)

---

## 1. Java String replaceFirst() Example

The `replaceFirst()` method is a variant of the [replace() method](114_Replace()_In_String_Java.md). The only difference is that `replace()` replaces **all** occurrences of the character or sub-string, but `replaceFirst()` only replaces the **first** occurrence. Apart from [replace()](114_Replace()_In_String_Java.md) and `replaceFirst()`, the Java string class also contains the [replaceAll() method](118_String_replaceAll()_Java.md).

- 🔄 `String = "vacation"` --> Replace first `'a'` with `'o'` --> Result: `"vocation"`

| Detail 📋 | Description 📝 |
|-----------|---------------|
| **Method Signature** | `public String replaceFirst(String regex, String substring)` |
| **Parameters** | `regex` - the regular expression to replace; `substring` - the replacement string |
| **Return Type** | `String` |
| **Returns** | A string after replacement |

**Example-1 - Basic `replaceFirst()` usage:**

```java
public class Main {
   public static void main(String[] args) {
      String string1 = "aaaabbbbaaaaaaccc";
      String string2 = "Java Programming";
      String str = "\\d+";

      System.out.println(string1.replaceFirst("aaaa", "zzzz"));
      System.out.println(string2.replaceFirst(str, " "));
   }
}
```

📤 **Output:**

```
zzzzbbbbaaaaaaccc
Java Programming
```

---

## 2. Regex Replacement with replaceFirst()

**Example-2 - Regex-based replacement:**

```java
public class Main {

   public static void main(String args[]) {
      String string = new String("Hi all, Goog morning..!");

      System.out.print("Return Value: ");
      System.out.println(string.replaceFirst("(.*)Goog(.*)", "Good"));

      System.out.print("Return Value: ");
      System.out.println(string.replaceFirst("Goog", "Good"));
   }
}
```

📤 **Output:**

```
Return Value: Good
Return Value: Hi all, Good morning..!
```

> 📝 **Note:** We called `replaceFirst("(.*)Goog(.*)", "Good")` so it finds the sub-string containing "Goog" and replaces the **entire match** with "Good". Therefore the result value is `"Good"`.

**Example-3 - Replacing only the first `#` character:**

```java
public class Main {
   public static void main(String[] args) {
      String string = "Hello ##ople";
      System.out.println(string.replaceFirst("#", "P"));
   }
}
```

📤 **Output:**

```
Hello P#ople
```

> 💡 **Tip:** Since `replaceFirst()` uses regex, special characters like `.`, `*`, `+`, `?` need to be escaped with `\\` if you want to match them literally. Use `Pattern.quote()` for safe literal matching.

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

**Java Tutorial**

**[String Class Methods](097_String_Class_Methods_In_Java.md)**
