# StringUtils startsWith() Example

**StringUtils startsWith() Example** | The `startsWith()` method of the [StringUtils class](155_Import_StringUtils_in_Java.md) from the Apache Commons Lang package returns a `boolean` value indicating whether the string starts with the given character or character sequence. If the string starts with the given value then it returns `true`, otherwise it returns `false`.

Basically, the `startsWith` method is a string-handling method that helps to check whether the given string starts with a particular character/string or not. This method is case-sensitive — if there is a lowercase letter at the beginning of the string and you search for an uppercase letter, it returns `false`.

- [The syntax of StringUtils startsWith() Method](#the-syntax-of-stringutils-startswith-method)
- [Example of the StringUtils.startsWith() Method](#example-of-the-stringutilsstartswith-method)
- [Java Program For StringUtils startsWith() Method](#java-program-for-stringutils-startswith-method)

---

## 1. The syntax of StringUtils startsWith() Method

**Method signature:**

```java
public static boolean startsWith(final CharSequence str, final CharSequence prefix)
```

Check if a `CharSequence` starts with a specified prefix.

- 📥 **Parameters:**
  - `str` — the given string which needs to be checked
  - `prefix` — the first letter or first substring to match against
- 📤 **Return type:** `boolean`
- ✅ **Returns:** `true` if the string starts with the given prefix, or `false` otherwise

🔒 `Null`s are handled without exceptions. Two `null` references are considered to be equal. The comparison is case-sensitive.

---

## 2. Example of the StringUtils.startsWith() Method

🛠️ **Example 1:**

- String: `"Apples"`, Starts With: `"A"` → `true`

🛠️ **Example 2:**

- String: `"Apples"`, Starts with: `"a"` → `false`

---

## 3. Java Program For StringUtils startsWith() Method

**Example 1 — Basic usage:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        String str = "Hello";
        System.out.println(StringUtils.startsWith(str, "H"));
        System.out.println(StringUtils.startsWith(str, "h"));
        System.out.println(StringUtils.startsWith(str, "Hel"));
        System.out.println(StringUtils.startsWith(str, "World"));
        System.out.println(StringUtils.startsWith(str, "Hello"));
    }
}
```

📤 **Output:**

```
true
false
true
false
true
```

Since the `startsWith()` method compares case-wise therefore `StringUtils.startsWith(str, "h")` returns `false` but `StringUtils.startsWith(str, "H")` returns `true`.

> ⚠️ **Caution:** The comparison is case-sensitive. `"H"` and `"h"` are treated as different prefixes.

**Example 2 — Null handling:**

`Null`s are handled without exceptions. Two `null` references are considered to be equal.

```java
import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        String str = null;
        System.out.println(StringUtils.startsWith(str, null));
        System.out.println(StringUtils.startsWith(str, "n"));
        System.out.println(StringUtils.startsWith(str, "null"));
        System.out.println(StringUtils.startsWith(str, "NULL"));
    }
}
```

📤 **Output:**

```
true
false
false
false
```

> 💡 **Tip:** Prefer `StringUtils.startsWith()` over Java's `String.startsWith()` when either the string or the prefix could be `null`. It handles `null` safely without throwing `NullPointerException`.
