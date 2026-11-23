# Java String toUpperCase() Method

**Java String toUpperCase() Method** | In this tutorial, we will see the purpose and work of the String `toUpperCase()` method. **This method is used to convert all the letters of the given string to upper case.** The `toUpperCase()` method has two variants.

- [String toUpperCase() Java Example](#string-touppercase-java-example)
- [String toUpperCase(Locale) Java Example](#string-touppercase-locale-java-example)

---

## 1. String toUpperCase() Java Example

| Variant 🏷️ | Signature 📋 |
|------------|-------------|
| **Without Locale** | `public String toUpperCase()` |
| **With Locale** | `public String toUpperCase(Locale locale)` |

- 📋 **Parameters:** `locale` is used to represent the `Locale` object.
- 📤 **Return Type:** `String`
- 🔠 **Returns:** String that is converted to upper case.

A `Locale` is a class object which represents a geographical, cultural, and political region. It is an identifier of an object but not the container of the object. It can have fields like country, language, extension script, and more.

Similar to the `toUpperCase()` method, the Java string class also contains the [toLowerCase() method](120_Java_String_to_Lowercase.md). Now see the examples:

- 🔠 `"hai"` --> `"HAI"`
- 🔠 `"WORLD"` --> `"WORLD"`
- 🔠 `"JAVA"` --> `"JAVA"`

Now, let us see some examples of String `toUpperCase()` methods. We will take a string and then call the `toUpperCase()` method on the given string.

**Basic `toUpperCase()` example:**

```java
public class Main {
   public static void main(String args[]) {
      String string = "Welcome to knowProgram";

      System.out.print("String: ");
      System.out.println(string.toUpperCase());
   }
}
```

📤 **Output:**

```
String: WELCOME TO KNOWPROGRAM
```

We can store the result string in a variable so that it can be used later in the programs. Let us see it through an example.

**Storing result in a variable:**

```java
public class Main {
   public static void main(String args[]) {
      String string = "Hello, World!";
      String uppercase = string.toUpperCase();
      System.out.println(uppercase);
   }
}
```

📤 **Output:**

```
HELLO, WORLD!
```

---

## 2. String toUpperCase(Locale) Java Example

If we want to convert the string based on some locale then the Java string class provides the `toUpperCase(Locale locale)` method. It converts the given string into uppercase based on the given locale. Let us see some examples of it.

**Locale-based `toUpperCase()` example:**

```java
import java.util.Locale;

public class Main {
   public static void main(String[] args) {
      String str = "Happy birthday.";

      String turkish = str.toUpperCase(Locale.forLanguageTag("tr"));
      String english = str.toUpperCase(Locale.forLanguageTag("en"));

      System.out.println(turkish);
      System.out.println(english);
   }
}
```

📤 **Output:**

```
HAPPY BİRTHDAY.
HAPPY BIRTHDAY.
```

**Another locale-based example with `toLowerCase()`:**

```java
import java.util.Locale;

public class Main {
   public static void main(String[] args) {
      String str = "ΙΧΘΥΣİ";

      Locale turkish = Locale.forLanguageTag("tr");
      Locale english = Locale.forLanguageTag("en");

      String string1 = str.toLowerCase(turkish);
      String string2 = str.toLowerCase(english);
      System.out.println("String: " + str);
      System.out.println("Turkish: " + string1);
      System.out.println("English: " + string2);
   }
}
```

📤 **Output:**

```
String: ΙΧΘΥΣİ
Turkish: ιχθυσi
English: ιχθυσi̇
```

> 💡 **Tip:** For [converting String to uppercase, lowercase, alternative case, sentence case, and title case](https://www.toolsmass.com/tools/convert-case) you can also take help from [online tools](https://www.toolsmass.com/).

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

**Java Tutorial**

**[String Class Methods](097_String_Class_Methods_In_Java.md)**
