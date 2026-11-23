# Java String to Lowercase

**Java String to Lowercase** | Sometimes there might be a scenario to convert all the letters or words to lowercase. In this case, retyping each and every word might be time-consuming so to avoid that Java has brought a method called **`toLowerCase()`**. And to convert the string to uppercase, [Java String class](097_String_Class_Methods_In_Java.md) contains the toUpperCase() method.

- [How to Make a String Lowercase in Java](#how-to-make-a-string-lowercase-in-java)
- [Java Convert String To Lowercase](#java-convert-string-to-lowercase)
- [Java How To Make String Lowercase](#java-how-to-make-string-lowercase)

---

## 1. How to Make a String Lowercase in Java

In this tutorial, we convert the string to lowercase using the `toLowerCase()` method. This method is a built-in method in the Java String class that helps us to convert the characters to lowercase.

| Variant 🏷️ | Signature 📋 | Description 📝 |
|------------|-------------|---------------|
| **Without Locale** | `public String toLowerCase()` | Converts all characters to lowercase using default locale |
| **With Locale** | `public String toLowerCase(Locale locale)` | Converts using the rules of the given `Locale` |

See the below examples:

- 🔡 `"HAPPY"` --> `"happy"`
- 🔡 `"Parrot"` --> `"parrot"`
- 🔡 `"aNiMal"` --> `"animal"`

For [converting String to uppercase, lowercase, alternative case, sentence case, and title case](https://www.toolsmass.com/tools/convert-case) you can also take help from the [online tools](https://www.toolsmass.com/).

Let us see a Java program to make a String lowercase in Java using the `toLowerCase()` method defined in the Java String class. We will define a string and call the `toLowerCase()` method on the given string.

**Java String to Lowercase Program using `toLowerCase()`:**

```java
public class Main {
   public static void main(String args[]) {
      String string = "JAVA PROGRAMMING LANGUAGE";
      System.out.println("String: " + string);
      string = string.toLowerCase();
      System.out.println("Resultant String: " + string);
   }
}
```

📤 **Output:**

```
String: JAVA PROGRAMMING LANGUAGE
Resultant String: java programming language
```

---

## 2. Java Convert String To Lowercase

In the previous example we used string literal, but this time we will use a String class constructor and then call the `toLowerCase()` method to convert the given string to lowercase.

**Program to convert a string to all lowercase in Java:**

```java
public class Main {
   public static void main(String args[]) {
      String string = new String("Java PrOGRAmmING lANGUAge");
      System.out.println("Lowercase string: " + string.toLowerCase());
   }
}
```

📤 **Output:**

```
Lowercase string: java programming language
```

---

## 3. Java How To Make String Lowercase

We can also convert the string to lowercase using the rules of the given `Locale`. First, we have to create an object for the `Locale` and pass it to the `toLowerCase()` method as a parameter.

**Locale-based `toLowerCase()` example:**

```java
import java.util.Locale;

public class Main {
   public static void main(String args[]) {
      String str = "ΙΧΘΥΣ" + "\u0130";
      String str1 = "TITLE";
      Locale turkish = Locale.forLanguageTag("tr");
      Locale english = Locale.forLanguageTag("en");

      String string1 = str.toLowerCase(turkish);
      String string2 = str.toLowerCase(english);
      System.out.println("String: " + str);
      System.out.println("Turkish: " + string1);
      System.out.println("English: " + string2);

      System.out.println("String: " + str1);
      System.out.println("Turkish: " + str1.toLowerCase(turkish));
      System.out.println("English: " + str1.toLowerCase(english));
   }
}
```

📤 **Output:**

```
String: ΙΧΘΥΣİ
Turkish: ιχθυσi
English: ιχθυσi̇
String: TITLE
Turkish: tıtle
English: title
```

In the above example, `"\u0130"` is a Unicode character set. Unicode stands for universal characters code, which contains all countries' speaking languages' character codes. See more: [Unicode character set in Java](017_Unicode_Character_Set_in_Java.md).

> 💡 **Tip:** Notice that the string `"TITLE"` is converted to `"tıtle"` in the Turkish locale whereas it is converted to `"title"` in the English locale. The Turkish language has a dotless `ı` which is the lowercase form of `I`.

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

**Java Tutorial**

**[String Class Methods](097_String_Class_Methods_In_Java.md)**
