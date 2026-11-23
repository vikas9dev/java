# StringUtils lowerCase() Method

**StringUtils lowerCase() Method** | The `lowerCase()` method is a static method in the `StringUtils` class that converts the string to lower case. If the string is `null` then this method returns `null`. There are two variations: one that accepts only the string and another that accepts both string and locale.

- [StringUtils.lowerCase() Method](#stringutilslowercase-method)
- [Java StringUtils lowerCase() Method](#java-stringutils-lowercase-method)
- [StringUtils lowerCase() Example](#stringutils-lowercase-example)

---

## 1. StringUtils.lowerCase() Method

The syntax for the `lowerCase` method is as follows:

- 🔤 `public static String lowerCase(final String str)` — Converts a `String` to lowercase as per the current locale.
- 🌐 `public static String lowerCase(final String str, final Locale locale)` — Converts a `String` to lowercase as per the given locale.

- 📥 **Parameters:**
  - `str` — the string which needs to be converted to lowercase
  - `locale` — the case transformation rule
- 📤 **Return type:** `String`
- ✅ **Return value:** the string in lowercase

---

## 2. Java StringUtils lowerCase() Method

Let us see an example of the default `lowerCase(String str)` method. When the string variable is referring to `null`, `StringUtils.lowerCase()` returns `null` itself. If the string variable contains an empty string, then `StringUtils.lowerCase()` returns an empty string.

**Java program:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {

    public static void main(String[] args) {
        String string = "Know Program";
        System.out.println("After conversion: " + StringUtils.lowerCase(string));

        string = "";
        System.out.println("After conversion: " + StringUtils.lowerCase(string));

        string = null;
        System.out.println("After conversion: " + StringUtils.lowerCase(string));
    }
}
```

📤 **Output:**

```
After conversion: know program
After conversion:
After conversion: null
```

---

## 3. StringUtils lowerCase() Example

Let us see an example of the `StringUtils.lowerCase()` method using locale.

**Java program with Locale:**

```java
import java.util.Locale;

import org.apache.commons.lang3.StringUtils;

public class Main {

    public static void main(String[] args) {
        String string = "ΙΧΘΥΣ";
        System.out.println(StringUtils.lowerCase(string, Locale.ENGLISH));
        System.out.println(StringUtils.lowerCase(string, Locale.GERMAN));
        System.out.println(StringUtils.lowerCase(string, Locale.FRANCE));
    }
}
```

📤 **Output:**

```
ιχθυς
ιχθυς
ιχθυς
```

> 📝 **Note:** The `lowerCase()` method is null-safe unlike Java's built-in `String.toLowerCase()`. When working with strings that could be `null`, prefer `StringUtils.lowerCase()` to avoid `NullPointerException`.
