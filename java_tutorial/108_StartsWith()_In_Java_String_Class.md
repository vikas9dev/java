# StartsWith() In Java String Class

**StartsWith() In Java String Class** | [Java String class](097_String_Class_Methods_In_Java.md) provides a way to check whether a string starts with a specified character/string or not by using the `startsWith()` method. This is a String class method that returns a boolean value `true` or `false`.

- [StartsWith In Java](#startswith-in-java)
- [Java String startsWith Ignore Case](#java-string-startswith-ignore-case)
- [Java startswith Regex](#java-startswith-regex)
- [The endswith In Java](#the-endswith-in-java)
- [Java String endswith Regex](#java-string-endswith-regex)

Similar to `startsWith()`, the String class also contains `endsWith()` method to check whether the string ends with the specified character/string or not. This method also returns a boolean value. In this post, we will cover the following methods:

1. `public boolean startsWith(String prefix)`
2. `public boolean startsWith(String prefix, int toffset)`
3. `public boolean endsWith(String suffix)`

**Quick startsWith() example:**

```java
String name = "Java";
System.out.println(name.startsWith("J"));
```

📤 **Output:**

```
true
```

**Quick endsWith() example:**

```java
String name = "Java";
System.out.println(name.endsWith("a"));
```

📤 **Output:**

```
true
```

---

## 1. StartsWith In Java

The `startsWith()` method has two variations. Let us demonstrate both:

**1) startsWith(String prefix)**

The `startsWith()` in Java takes only one parameter `prefix`. If the string starts with the same substring or character then it returns `true` or else `false`. The `startsWith()` method is case sensitive.

**Case-sensitive startsWith() example:**

```java
public class Main {
   public static void main(String args[]) {
      String web = "Know Program";
      System.out.println(web.startsWith("K"));
      System.out.println(web.startsWith("k"));
   }
}
```

📤 **Output:**

```
true
false
```

> ⚠️ **Caution:** The `startsWith()` method is case-sensitive. `"K"` and `"k"` are treated as different characters.

**2) startsWith(String prefix, int toffset)**

This `startsWith()` in Java takes two parameters `prefix` and `toffset`. The `toffset` is an integer value that takes an index of the string and searches the prefix at that particular index.

**startsWith with offset example:**

```java
public class Main {
   public static void main(String args[]) {
      String web = "Know Program";
      System.out.println(web.startsWith("P", 5));
      System.out.println(web.startsWith("P", 1));
      System.out.println(web.startsWith("n", 1));
      System.out.println(web.startsWith("r", 9));
      System.out.println(web.startsWith("m", web.length()));
      System.out.println(web.startsWith("m", web.length()-1));
   }
}
```

📤 **Output:**

```
true
false
true
true
false
true
```

---

## 2. Java String startsWith Ignore Case

As we know `startsWith()` is case sensitive, we can ignore the case by using toUpperCase() and [toLowerCase() methods](120_Java_String_to_Lowercase.md) which convert the specified string into upper or lower case. After that, we can search for the string.

**startsWith with case ignoring:**

```java
public class Main {
   public static void main(String args[]) {
      String name = "Know Program";
      System.out.println(name.toLowerCase().startsWith("k"));
      System.out.println(name.toUpperCase().startsWith("KNOW"));
      System.out.println(name.toLowerCase().startsWith("program"));
   }
}
```

📤 **Output:**

```
true
true
false
```

> 💡 **Tip:** Convert both the string and the prefix to the same case before calling `startsWith()` for case-insensitive matching.

---

## 3. Java startswith Regex

Now we use regular expressions to check for the pattern which starts from the specified character. For this, we need to import various classes of the Java library: `Locale`, `Set`, `TreeSet`, `regex.Matcher`, `regex.Pattern`. We find all the languages which start with 'K'.

**Regex-based startsWith:**

```java
import java.util.Locale;
import java.util.Set;
import java.util.TreeSet;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class Main {

   public static void main(String[] args) {

      Set<String> language = new TreeSet<>();
      Locale[] locales = Locale.getAvailableLocales();
      for (Locale locale : locales) {
         language.add(locale.getDisplayLanguage());
      }

      Pattern pattern = Pattern.compile("^K");
      System.out.println("Language name which have the pattern of "
                         + pattern.pattern() + ": ");

      for (String lang : language) {
         Matcher matcher = pattern.matcher(lang);
         if (matcher.lookingAt()) {
            System.out.println(lang);
         }
      }
   }
}
```

📤 **Output:**

```
Language name which have the pattern of ^K:
Kabuverdianu
Kabyle
Kako
Kalaallisut
Kalenjin
Kamba
Kannada
Kashmiri
Kazakh
Khmer
Kikuyu
Kinyarwanda
Konkani
Korean
Koyra Chiini
Koyraboro Senni
Kurdish
Kwasio
Kyrgyz
```

---

## 4. The endswith In Java

Now, we will check for the string which ends with a given character or substring by using the `endsWith()` method in Java.

**endsWith() example:**

```java
public class Main {
   public static void main(String args[]) {
      String name = "Know Program";
      System.out.println(name.endsWith("m"));
      System.out.println(name.endsWith("Program"));
      System.out.println(name.endsWith("program"));
      System.out.println(name.endsWith("now"));
   }
}
```

📤 **Output:**

```
true
true
false
false
```

---

## 5. Java String endswith Regex

Now we use regular expressions to check for the pattern which ends with the specified character. Here we search for languages that end with "da".

**Regex-based endsWith:**

```java
import java.util.Locale;
import java.util.Set;
import java.util.TreeSet;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class Main {

   public static void main(String[] args) {

      Set<String> language = new TreeSet<>();
      Locale[] locales = Locale.getAvailableLocales();
      for (Locale locale : locales) {
         language.add(locale.getDisplayLanguage());
      }

      Pattern pattern = Pattern.compile(".*da$");
      System.out.println("Language name which have the pattern of "
                         + pattern.pattern() + ": ");

      for (String lang : language) {
         Matcher matcher = pattern.matcher(lang);
         if (matcher.lookingAt()) {
            System.out.println(lang);
         }
      }
   }
}
```

📤 **Output:**

```
Language name which have the pattern of .*da$:
Ganda
Kannada
Kinyarwanda
```

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
