# Java StringUtils repeat() Method

**Java StringUtils repeat() Method** | The `repeat()` method in the [StringUtils class](155_Import_StringUtils_in_Java.md) is used to repeat a string or character a specified number of times.

- [Java StringUtils repeat() Method Syntax](#java-stringutils-repeat-method-syntax)
- [Example of StringUtils.repeat() Java Method](#example-of-stringutilsrepeat-java-method)
- [StringUtils.repeat() Java Examples](#stringutilsrepeat-java-examples)
- [How To Use StringUtils In Java To repeat A Character](#how-to-use-stringutils-in-java-to-repeat-a-character)
- [String repeat Java Without StringUtils](#string-repeat-java-without-stringutils)
- [Limitations with String class repeat() Method](#limitations-with-string-class-repeat-method)

---

## 1. Java StringUtils repeat() Method Syntax

Java `StringUtils.repeat()` method has the following three variations:

1. 🔤 `public static String repeat(final char ch, final int repeat)` — Returns padding using the specified delimiter repeated to a given length.
2. 🔡 `public static String repeat(final String str, final int repeat)` — Repeat a `String` given repeat times to form a new `String`.
3. 🔗 `public static String repeat(final String str, final String separator, final int repeat)` — Repeat a `String` given repeat times to form a new `String`, with a `String` separator injected each time.

- 📥 **Parameters:**
  - `ch` — the character needed to be repeated
  - `str` — the string needed to be repeated
  - `repeat` — the number of times it should be repeated
  - `separator` — specifies the character to separate each string; if not mentioned then the repeated strings are concatenated together
- 📤 **Return type:** `String`
- ✅ **Returns:** the string after repeating

---

## 2. Example of StringUtils.repeat() Java Method

🛠️ **Example 1:**

- String: `"Mango"`, Repetitions: 2 → `"MangoMango"`

🛠️ **Example 2:**

- String: `"Mango"`, Separator: `","`, Repetitions: 2 → `"Mango,Mango"`

🛠️ **Example 3:**

- Character: `'c'`, Repetitions: 2 → `"cc"`

---

## 3. StringUtils.repeat() Java Examples

Let us see an example of `repeat(String str, int repeat)` which repeats the `String` a given number of times.

**Repeat a string:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        String str = "Hello";
        System.out.println("String after repetition: " + StringUtils.repeat(str, 4));
        str = " ";
        System.out.println("String after repetition: " + StringUtils.repeat(str, 3));
        str = "Abc";
        System.out.println("String after repetition: " + StringUtils.repeat(str, 3));
        str = null;
        System.out.println("String after repetition: " + StringUtils.repeat(str, 3));
        str = "null";
        System.out.println("String after repetition: " + StringUtils.repeat(str, 3));
    }
}
```

📤 **Output:**

```
String after repetition: HelloHelloHelloHello
String after repetition:
String after repetition: AbcAbcAbc
String after repetition: null
String after repetition: nullnullnull
```

Let us see an example of `repeat(String str, String separator, int repeat)` which repeats the `String` with a separator injected each time.

**Repeat with separator:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        String string = "Hello";
        System.out.println("String after repetition: " + StringUtils.repeat(string, " ", 4));
        string = "Abc";
        System.out.println("String after repetition: " + StringUtils.repeat(string, ", ", 3));
        string = null;
        System.out.println("String after repetition: " + StringUtils.repeat(string, " /", 3));

    }
}
```

📤 **Output:**

```
String after repetition: Hello Hello Hello Hello
String after repetition: Abc, Abc, Abc
String after repetition: null
```

---

## 4. How To Use StringUtils In Java To repeat A Character

Let us see an example of `repeat(char ch, int repeat)` which returns padding using the specified delimiter repeated to a given length.

**Repeat a character:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        char ch = 'B';
        System.out.println("Character after repetition: " + StringUtils.repeat(ch, 4));
        ch = 'a';
        System.out.println("Character after repetition: " + StringUtils.repeat(ch, 3));
        ch = ' ';
        System.out.println("Character after repetition: " + StringUtils.repeat(ch, 3));
    }
}
```

📤 **Output:**

```
Character after repetition: BBBB
Character after repetition: aaa
Character after repetition:
```

---

## 5. String repeat Java Without StringUtils

We can also repeat a character or `String` without using the `StringUtils` class. The `String` class itself contains the repeat() method which can repeat the string N number of times.

**Java program to repeat a string without StringUtils:**

```java
public class Main {
    public static void main(String[] args) {
        String string = "KnowProgram";
        System.out.println("String: " + string.repeat(2));
        string = "Abc";
        System.out.println("String: " + string.repeat(5));
    }
}
```

📤 **Output:**

```
String: KnowProgramKnowProgram
String: AbcAbcAbcAbcAbc
```

**Java program to repeat a character without StringUtils:**

```java
public class Main {
    public static void main(String[] args) {
        char ch = 'H';
        // convert char to String
        String string = String.valueOf(ch);
        System.out.println("String: " + string.repeat(2));

        ch = '9';
        System.out.println("String: " + String.valueOf(ch).repeat(5));
    }
}
```

📤 **Output:**

```
String: HH
String: 99999
```

---

## 6. Limitations with String class repeat() Method

> ⚠️ **Caution:** Why do we need `StringUtils.repeat()` over `String.repeat()`?

1. 🔗 Using the `String` class `repeat()` method we can't inject a separator between the repeated string or character.
2. 🔄 To repeat a character, the character needs to be converted to a string first.
3. 🚨 `String` class methods don't handle `null` and when we apply the `repeat()` method on a `null` reference it gives `NullPointerException`.

**Null handling comparison:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        String string = null;
        System.out.println("Using StringUtils.repeat(): " + StringUtils.repeat(string, 2));

        System.out.println("Using String class repeat(): ");
        System.out.println(string.repeat(2));
    }
}
```

📤 **Output:**

```
Using StringUtils.repeat(): null
Using String class repeat():
Exception in thread "main" java.lang.NullPointerException
at Main.main(Main.java:9)
```

4. 🚨 When we pass a negative value as the number of repeats to `StringUtils.repeat()`, it returns an empty string. But the `String` class `repeat()` method throws `IllegalArgumentException`.

**Negative repeat comparison:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        String string = "Hello";
        String newString = StringUtils.repeat(string, -2);
        System.out.println("Using StringUtils.repeat(): " + newString);
        System.out.println("Length: " + newString.length());

        System.out.println("Using String class repeat(): ");
        System.out.println(string.repeat(-2));
    }
}
```

📤 **Output:**

```
Using StringUtils.repeat():
Length: 0
Using String class repeat():
Exception in thread "main" java.lang.IllegalArgumentException: count is negative: -2
at java.base/java.lang.String.repeat(String.java:3149)
at Main.main(Main.java:11)
```

| Feature ⚖️ | StringUtils.repeat() 🛠️ | String.repeat() 🔤 |
|-------------|--------------------------|---------------------|
| **Null safety** | ✅ Returns `null` | ❌️ Throws `NullPointerException` |
| **Separator support** | ✅ Built-in separator option | ❌️ Not supported |
| **Char repeat** | ✅ Direct `char` support | ❌️ Needs conversion |
| **Negative count** | ✅ Returns empty string | ❌️ Throws `IllegalArgumentException` |
