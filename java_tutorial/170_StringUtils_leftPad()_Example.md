# StringUtils leftPad() Example

**StringUtils leftPad() Example** | In the `StringUtils` class, the `leftPad()` method is used to add whitespaces or given characters/strings to the left of the string. There are three different variations of this method.

The syntax for the `leftPad()` method and its variations are as follows:

- 🔤 `public static String leftPad(final String str, final int size)` — Pad with spaces
- 🔠 `public static String leftPad(final String str, final int size, final char padChar)` — Pad with a character
- 🔡 `public static String leftPad(final String str, final int size, String padStr)` — Pad with a string

- 📥 **Parameters:**
  - `str` — the string needed to add spaces or characters
  - `size` — an integer value, which specifies the final length of the string after padding
  - `padChar` — the character which needs to be padded
  - `padStr` — the string which needs to be padded
- 📤 **Return type:** `String`
- ✅ **Returns:** the string after padding

- [Apache StringUtils leftPad() Example-1](#apache-stringutils-leftpad-example-1)
- [StringUtils leftPad() Example-2](#stringutils-leftpad-example-2)
- [Java StringUtils leftPad() Example-3](#java-stringutils-leftpad-example-3)

---

## 1. Apache StringUtils leftPad() Example-1

This example demonstrates the working of `leftPad(String str, int size)`.

**Padding with spaces:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        String str = "Books";
        int number = 19;
        System.out.println("Length of the string before padding: " + str.length());
        String str1 = StringUtils.leftPad(str, number);
        System.out.printf("StringUtils.leftPad(%s, %s) = %s", str, number, str1);
        System.out.println("\nLength of the string after padding: " + str1.length());

    }
}
```

📤 **Output:**

```
Length of the string before padding: 5
StringUtils.leftPad(Books, 19) =               Books
Length of the string after padding: 19
```

---

## 2. StringUtils leftPad() Example-2

This demonstrates the working of `leftPad(String str, int size, String padStr)`.

**Padding with a string:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        String str = "Books";
        int number = 19;
        System.out.println("Length of the string before padding: " + str.length());
        String str1 = StringUtils.leftPad(str, number, "Something");
        System.out.printf("StringUtils.leftPad(%s, %s) = %s", str, number, str1);
        System.out.println("\nLength of the string after padding: " + str1.length());
    }
}
```

📤 **Output:**

```
Length of the string before padding: 5
StringUtils.leftPad(Books, 19) = SomethingSometBooks
Length of the string after padding: 19
```

---

## 3. Java StringUtils leftPad() Example-3

This code demonstrates the working of `leftPad(String str, int size, char padChar)`.

**Padding with a character:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        String str = "Books";
        int number = 19;
        System.out.println("Length of the string before padding: " + str.length());
        String str1 = StringUtils.leftPad(str, number, 'A');
        System.out.printf("StringUtils.leftPad(%s, %s) = %s", str, number, str1);
        System.out.println("\nLength of the string after padding: " + str1.length());
    }
}
```

📤 **Output:**

```
Length of the string before padding: 5
StringUtils.leftPad(Books, 19) = AAAAAAAAAAAAAABooks
Length of the string after padding: 19
```

> 💡 **Tip:** `leftPad()` is commonly used for formatting output such as aligning numbers or creating fixed-width columns. For example, `StringUtils.leftPad("42", 5, '0')` produces `"00042"`.
