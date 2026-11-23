# StringUtils containsAny() Method

**StringUtils containsAny() Method** | The `containsAny()` method in the [StringUtils class](155_Import_StringUtils_in_Java.md) is used to check whether the given string contains any of the specified characters or substrings. The contains() method of StringUtils class also does a similar task but the difference is that `contains()` searches for an exact pattern while `containsAny()` checks if any of the search characters/strings exist in the main string.

The `containsAny()` method returns a `boolean` value. If any of the values match then it returns `true`, or if none match it returns `false`. Note that `containsAny()` method is case-sensitive.

- [StringUtils.containsAny() Method](#stringutilscontainsany-method)
- [StringUtils containsAny() Method Example](#stringutils-containsany-method-example)

---

## 1. StringUtils.containsAny() Method

There are three overloaded forms of the `StringUtils.containsAny()` method:

1. 🔤 `containsAny(CharSequence cs, char... searchChars)` — Checks for any matching characters
2. 🔡 `containsAny(CharSequence cs, CharSequence... searchCharSequences)` — Checks for any matching string from an array
3. 🔍 `containsAny(CharSequence cs, CharSequence searchChars)` — Checks for any character from the search string

The `containsAny(CharSequence cs, char... searchChars)` and `containsAny(CharSequence cs, CharSequence searchChars)` methods check if the `CharSequence` contains any character in the given set of characters. The `containsAny(CharSequence cs, CharSequence... searchCharSequences)` method checks if the `CharSequence` contains any of the `CharSequences` in the given array.

For all these overloaded forms, a `null` `CharSequence` will return `false`. A `null` or zero-length search array will also return `false`.

🛠️ **Example:**

- String: `"Apple"`, Search: `"pp"` — Result: `true`
- String: `"Apple"`, Search: `"oooo"` — Result: `false`

---

## 2. StringUtils containsAny() Method Example

**Example 1 — `containsAny(CharSequence cs, CharSequence searchChars)`:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        System.out.println(StringUtils.containsAny("Hello", "Hello"));
        System.out.println(StringUtils.containsAny("Hello", "H"));
        System.out.println(StringUtils.containsAny("Hello", "Who"));
        System.out.println(StringUtils.containsAny("Hello", "Sir"));
        System.out.println(StringUtils.containsAny("Hello", "Shift"));
    }
}
```

📤 **Output:**

```
true
true
true
false
false
```

In the String `"Hello"` there are four unique characters: `'H'`, `'e'`, `'l'`, `'o'`. In the first line, we are checking whether the given string contains any character of the string `"Hello"` and since both are the same string therefore it returns `true`.

In the second line, we are checking whether the string contains the `'H'` character or not and it returns `true`. In the third line, we are checking whether the string contains any characters from the string literal `"Who"` and since `'o'` is common among them therefore it returns `true`. Note that `containsAny()` method is case sensitive so `'H'` from `"Hello"` and `'h'` from `"Who"` is not the same.

In the fourth line, we are checking whether the string contains any character of the string literal `"Sir"`, but the `"Hello"` string doesn't contain `'S'`, `'i'`, or `'r'` characters therefore it returns `false`. Similarly in the fifth line, it returns `false`.

**Example 2 — `containsAny(CharSequence cs, char... searchChars)`:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        System.out.println(StringUtils.containsAny("Hello", 'H', 'e', 'l', 'l', 'o'));
        System.out.println(StringUtils.containsAny("Hello", 'H'));
        System.out.println(StringUtils.containsAny("Hello", 'W', 'h', 'o'));
        System.out.println(StringUtils.containsAny("Hello", 'S', 'i', 'r'));
        System.out.println(StringUtils.containsAny("Hello", 'S', 'h', 'i', 'f', 't'));
    }
}
```

📤 **Output:**

```
true
true
true
false
false
```

**Example 3 — `containsAny(CharSequence cs, CharSequence... searchCharSequences)`:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        System.out.println(StringUtils.containsAny("Hello", "H", "e", "l", "l", "o"));
        System.out.println(StringUtils.containsAny("Hello", "H"));
        System.out.println(StringUtils.containsAny("Hello", "W", "h", "o"));
        System.out.println(StringUtils.containsAny("Hello", "S", "i", "r"));
        System.out.println(StringUtils.containsAny("Hello", "S", "h", "i", "f", "t"));
    }
}
```

📤 **Output:**

```
true
true
true
false
false
```

> ⚠️ **Caution:** The `containsAny()` method is case-sensitive. `'H'` and `'h'` are treated as different characters. Use `containsAnyIgnoreCase()` if you need case-insensitive matching.
