# StringUtils replaceEach() Example

**StringUtils replaceEach() Example** | The `replaceEach()` method of the `StringUtils` class is used to replace each of the characters/patterns present in the string using search and replacement arrays.

The question might arise: what is the difference between `replace()` and `replaceEach()` method? The `replace()` method replaces all occurrences of a single given pattern whereas `replaceEach()` accepts arrays of search strings and replacement strings, allowing multiple replacements in a single call. Also `replaceEach()` can replace the occurrence of the given pattern provided it does not need to be in any specific order.

- [StringUtils replaceEach() Method Syntax](#stringutils-replaceeach-method-syntax)
- [Java StringUtils replaceEach() Example](#java-stringutils-replaceeach-example)

---

## 1. StringUtils replaceEach() Method Syntax

**Method signature:**

```java
public static String replaceEach(final String text, final String[] searchList, final String[] replacementList)
```

- 📥 **Parameters:**
  - `text` — the original string
  - `searchList` — array of strings containing the patterns to be replaced
  - `replacementList` — array of strings that have the replacement values at corresponding positions

| Parameter 📋 | Description 📝 |
|--------------|----------------|
| **`text`** | The original string to perform replacements on |
| **`searchList`** | Array of search patterns |
| **`replacementList`** | Array of replacement values (must match `searchList` length) |

---

## 2. Java StringUtils replaceEach() Example

**Example 1 — Basic replacement:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        String str = "7896";
        System.out.println("The string after the replacement is: "
                + StringUtils.replaceEach(str, new String[] { "789" }, new String[] { "156" }));
        str = " ";
        System.out.println("The string after the replacement is: "
                + StringUtils.replaceEach(str, new String[] { "789" }, new String[] { "123" }));
    }
}
```

📤 **Output:**

```
The string after the replacement is: 1566
The string after the replacement is:
```

**Example 2 — No matching pattern:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        String str = "abc";
        System.out.println("The string after the replacement is: "
                + StringUtils.replaceEach(str, new String[] { " " }, new String[] { " " }));
        str = "abc";
        System.out.println("The string after the replacement is: "
                + StringUtils.replaceEach(str, new String[] { "789" }, new String[] {}));
    }
}
```

📤 **Output:**

```
The string after the replacement is: abc
The string after the replacement is: abc
```

**Example 3 — Multiple replacements:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        String str = "abc";
        System.out.println("The string after the replacement is: "
                + StringUtils.replaceEach(str, new String[] { "a" }, new String[] { " " }));
        str = "abc";
        System.out.println("The string after the replacement is: "
                + StringUtils.replaceEach(str, new String[] { "789" }, new String[] { "123" }));
        str = "abcde";
        System.out.println("The string after the replacement is: "
                + StringUtils.replaceEach(str, new String[] { "a", "d" }, new String[] { "A", "D" }));
    }
}
```

📤 **Output:**

```
The string after the replacement is:  bc
The string after the replacement is: abc
The string after the replacement is: AbcDe
```

> 💡 **Tip:** The `searchList` and `replacementList` arrays must be of the same length. Each element in `searchList` is replaced by the corresponding element in `replacementList`. This method is very useful for performing multiple string substitutions in a single pass.
