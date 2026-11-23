# String replaceAll() Java

**String replaceAll() Java** | In this section, we explore the `replaceAll()` method available in Java to replace a string with a given substring. Let us understand it through some examples.

---

## 1. Java replaceAll() String Demonstration

- 🔄 **Example-1:** `"Java the programming the"` --> `replaceAll("the", "XYZ")` --> `"Java XYZ programming XYZ"`
- 🔄 **Example-2:** `"Know………Program"` --> `replaceAll("………", " ")` --> `"Know Program"`

| Detail 📋 | Description 📝 |
|-----------|---------------|
| **Method Signature** | `public String replaceAll(String regex, String replacement)` |
| **Parameters** | `regex` - the regular expression to replace; `replacement` - the replacement substring |
| **Returns** | The replaced string |
| **Throws** | `PatternSyntaxException` if the regex syntax is not valid |

**Internal implementation:**

```java
public String replaceAll(String regex, String replacement){
   return Pattern.compile(regex)
                .matcher(this)
                .replaceAll(replacement);
}
```

> 📝 **Note:** Internally, `replaceAll()` of the String class calls the `replaceAll()` method of the `Matcher` class defined in `java.util.regex` package. Apart from `replaceAll()`, the Java String class also provides [replace() method](114_Replace()_In_String_Java.md) and replaceFirst() method.

Let us see a simple Java program to demonstrate how the `replaceAll()` method works. In the below program, we took a string and we are replacing the `"Language"` substring with the `"lang"` substring.

**Example-1 - Basic `replaceAll()` usage:**

```java
public class Main {
   public static void main(String args[]) {
      String str1 = "Java Language, Python Language, Go Language";
      String replace = str1.replaceAll("Language", "lang");
      System.out.println(replace);
   }
}
```

📤 **Output:**

```
Java lang, Python lang, Go lang
```

---

## 2. String.replaceAll() in Java Example

**Example-2 - Replace a character with another character:**

```java
public class Main {
   public static void main(String args[]) {
      String str1 = "JAvA ProgrAmming LAnguAge";
      String replace = str1.replaceAll("A", "a");
      System.out.println(replace);
   }
}
```

📤 **Output:**

```
Java Programming Language
```

In the above program, the character `"A"` is replaced with the new character `"a"`. Hence the original string `"JAvA ProgrAmming LAnguAge"` becomes `"Java Programming Language"`.

---

## 3. Java replaceAll() String Whitespace

Now, we will try to replace all the whitespace in the given string by using the `replaceAll()` method. The space and tab belong to whitespace.

**Example-3 - Remove all whitespace:**

```java
public class Main {
   public static void main(String args[]) {
      String str1 = "Learn Java Programming   Language"+
                    " - Know \t Program \n  Website";
      String replace = str1.replaceAll("\\s", "");
      System.out.println(replace);
   }
}
```

📤 **Output:**

```
LearnJavaProgrammingLanguage-KnowProgramWebsite
```

---

## 4. Java String.replaceAll()

In this section, we add whitespaces to the string by using the `replaceAll()` method.

**Example-4 - Adding spaces between characters:**

```java
public class Main {

   public static void main(String argvs[]) {
      String string = "KnowProgram";
      System.out.println(string);

      String regex = "";
      string = string.replaceAll(regex, " ");
      System.out.println(string);
   }
}
```

📤 **Output:**

```
KnowProgram
 K n o w P r o g r a m
```

> ⚠️ **Caution:** Using an empty string `""` as the regex matches every position in the string, inserting a space between every character. This is rarely the intended behavior.

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

**Java Tutorial**

**[String Class Methods](097_String_Class_Methods_In_Java.md)**
