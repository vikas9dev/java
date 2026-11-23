# Java StringUtils split() Method

**Java StringUtils split() Method** | The `split()` method in the `StringUtils` class takes two arguments: a string which needs to be split and the substring or character which needs to be removed from the string. The `split` method returns an array of strings after the split is performed.

The overloaded forms of the `StringUtils.split()` are as follows:

- 🔤 `public static String[] split(final String str)` — Splits using whitespace as the separator
- 🔡 `public static String[] split(final String str, final char separatorChar)` — Splits by a specified character
- 🔍 `public static String[] split(final String str, final String separatorChars)` — Splits by specified characters
- ✂️ `public static String[] split(final String str, final String separatorChars, final int max)` — Splits with a maximum array length

- [Java StringUtils split() Method](#java-stringutils-split-method-1)
- [Java Code To Split String With Specific Length Using StringUtils](#java-code-to-split-string-with-specific-length-using-stringutils)
- [Java StringUtils split() And trim()](#java-stringutils-split-and-trim)
- [Similar Methods like StringUtils.split()](#similar-methods-like-stringutilssplit)

---

## 1. Java StringUtils split() Method

**Example 1 — Split by character:**

```java
import java.util.Arrays;

import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        String string = "bababacca";
        String[] array = StringUtils.split(string, 'a');
        System.out.println(Arrays.toString(array));
    }
}
```

📤 **Output:**

```
[b, b, b, cc]
```

**Example 2 — Multiple split variations:**

```java
import java.util.Arrays;

import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        String string = "Know Program";
        System.out.println(Arrays.toString(StringUtils.split(string)));
        System.out.println(Arrays.toString(StringUtils.split(string, 'o')));
        System.out.println(Arrays.toString(StringUtils.split(string, "ro")));

    }
}
```

📤 **Output:**

```
[Know, Program]
[Kn, w Pr, gram]
[Kn, w P, g, am]
```

> 📝 **Note:** The `StringUtils.split(string, "ro")` method splits a string by characters `'r'`, and `'o'`, and substring `"ro"`. But not only based on the substring `"ro"`.

---

## 2. Java Code To Split String With Specific Length Using StringUtils

**Java program:**

```java
import java.util.Arrays;

import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        String string = "Know Program";
        System.out.println(Arrays.toString(StringUtils.split(string, "ro")));
        System.out.println(Arrays.toString(StringUtils.split(string, "ro", 1)));
        System.out.println(Arrays.toString(StringUtils.split(string, "ro", 2)));
        System.out.println(Arrays.toString(StringUtils.split(string, "ro", 3)));
        System.out.println(Arrays.toString(StringUtils.split(string, "ro", 4)));
        System.out.println(Arrays.toString(StringUtils.split(string, "ro", 5)));
    }
}
```

📤 **Output:**

```
[Kn, w P, g, am]
[Know Program]
[Kn, w Program]
[Kn, w P, gram]
[Kn, w P, g, am]
[Kn, w P, g, am]
```

---

## 3. Java StringUtils split() And trim()

The `split()` and `trim()` are two different methods used to manipulate the string. Even though both seem the same there are slight differences between them:

- ✂️ The `split()` method removes the object we specify and returns an **array of strings**
- 🧹 The `trim()` method removes only the **whitespaces** and returns the original string without leading and trailing whitespaces

**Java program:**

```java
import java.util.Arrays;

import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        String string = "       Know Program       ";
        System.out.println(Arrays.toString(StringUtils.split(string)));
        System.out.println(Arrays.toString(StringUtils.split(string, 'o')));
        System.out.println(StringUtils.trim(string));
    }
}
```

📤 **Output:**

```
[Know, Program]
[ Kn, w Pr, gram ]
Know Program
```

---

## 4. Similar Methods like StringUtils.split()

There are many similar methods like the `split()` method. They are as follows:

- `splitByCharacterType(final String str)`
- `splitByCharacterTypeCamelCase(final String str)`
- `splitByWholeSeparator(final String str, final String separator)`
- `splitByWholeSeparator(final String str, final String separator, final int max)`
- `splitByWholeSeparatorPreserveAllTokens(final String str, final String separator)`
- `splitByWholeSeparatorPreserveAllTokens(final String str, final String separator, final int max)`
- `splitPreserveAllTokens(final String str)`
- `splitPreserveAllTokens(final String str, final char separatorChar)`
- `splitPreserveAllTokens(final String str, final String separatorChars)`
- `splitPreserveAllTokens(final String str, final String separatorChars, final int max)`

**Java program demonstrating similar methods:**

```java
import java.util.Arrays;
import org.apache.commons.lang3.StringUtils;

public class Main {

    public static void main(String[] args) {
        String string = "Know Program";

        System.out.println(Arrays.toString(StringUtils.splitByWholeSeparator(string, "o")));
        System.out.println(Arrays.toString(
            StringUtils.splitByWholeSeparator(string, "o", 3)));
        System.out.println(Arrays.toString(
            StringUtils.splitByWholeSeparatorPreserveAllTokens(string, "o")));
        System.out.println(Arrays.toString(
            StringUtils.splitByWholeSeparatorPreserveAllTokens(string, "o", 3)));

        System.out.println(Arrays.toString(StringUtils.splitPreserveAllTokens(string)));
        System.out.println(Arrays.toString(
            StringUtils.splitPreserveAllTokens(string, 'o')));
        System.out.println(Arrays.toString(
            StringUtils.splitPreserveAllTokens(string, "o")));
        System.out.println(Arrays.toString(
            StringUtils.splitPreserveAllTokens(string, "o", 1)));
    }
}
```

📤 **Output:**

```
[Kn, w Pr, gram]
[Kn, w Pr, gram]
[Kn, w Pr, gram]
[Kn, w Pr, gram]
[Know, Program]
[Kn, w Pr, gram]
[Kn, w Pr, gram]
[Know Program]
```

> 💡 **Tip:** Use `splitByWholeSeparator()` when you need to split by the entire separator string rather than individual characters. Use `splitPreserveAllTokens()` when empty tokens should be preserved in the result array.
