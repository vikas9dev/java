# Java StringUtils contains() Method

**Java StringUtils contains() Method** | The `contains()` method in [StringUtils](155_Import_StringUtils_in_Java.md) checks whether the substring is contained in the main string or not. There are many variations of the `StringUtils` `contains()` method as listed below:

1. 🔍 `contains(CharSequence seq, CharSequence searchSeq)`
2. 🔤 `contains(CharSequence seq, int searchChar)`
3. 🔎 `containsAny(CharSequence cs, char... searchChars)`
4. 🔎 `containsAny(CharSequence cs, CharSequence... searchCharSequences)`
5. 🔎 `containsAny(CharSequence cs, CharSequence searchChars)`
6. 🔡 `containsAnyIgnoreCase(CharSequence cs, CharSequence... searchCharSequences)`
7. 🔡 `containsIgnoreCase(CharSequence str, CharSequence searchStr)`
8. ❌️ `containsNone(CharSequence cs, char... searchChars)`
9. ❌️ `containsNone(CharSequence cs, String invalidChars)`
10. ✅ `containsOnly(CharSequence cs, char... valid)`
11. ✅ `containsOnly(CharSequence cs, String validChars)`

- [StringUtils Java contains() Method](#stringutils-java-contains-method)
- [Java StringUtils contains() Method Example](#java-stringutils-contains-method-example)
- [Java StringUtils containsIgnoreCase() Method](#java-stringutils-containsignorecase-method)
- [StringUtils Java containsAny() Method](#stringutils-java-containsany-method)
- [Java StringUtils containsNone() Method](#java-stringutils-containsnone-method)
- [Java StringUtils containsOnly() Method](#java-stringutils-containsonly-method)

---

## 1. StringUtils Java contains() Method

🛠️ **Example:**

- String: `"Apple"`, Search: `"Ap"` — Result: `true`
- String: `"Apple"`, Search: `"abc"` — Result: `false`

---

## 2. Java StringUtils contains() Method Example

The `contains(CharSequence seq, CharSequence searchSeq)` method checks if `CharSequence` contains a search `CharSequence`, handling `null`. This method uses [String#indexOf(String)](110_Java_String_indexOf()_Method.md) if possible. A `null` `CharSequence` will return `false`.

The `contains(CharSequence seq, int searchChar)` method checks if `CharSequence` contains a search character, handling `null`. This method uses [String#indexOf(int)](110_Java_String_indexOf()_Method.md) if possible. A `null` or empty (`""`) `CharSequence` will return `false`.

**Example 1 — Basic contains:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        String string = "Banana";
        System.out.println(StringUtils.contains(string, "ana"));
        System.out.println(StringUtils.contains(string, "Hello"));
        System.out.println(StringUtils.contains(string, "H"));
        System.out.println(StringUtils.contains(string, "B"));
    }
}
```

📤 **Output:**

```
true
false
false
true
```

**Example 2 — Null and empty inputs:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        System.out.println(StringUtils.contains(null, "ana"));
        System.out.println(StringUtils.contains("", "Hello"));
        System.out.println(StringUtils.contains("", "H"));
        System.out.println(StringUtils.contains(null, "B"));
    }
}
```

📤 **Output:**

```
false
false
false
false
```

---

## 3. Java StringUtils containsIgnoreCase() Method

The `containsIgnoreCase(CharSequence str, CharSequence searchStr)` method works very similar to the `contains()` method but it ignores the case of the characters.

**Java program:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        String string = "Banana";
        System.out.println(StringUtils.containsIgnoreCase(string, "ana"));
        System.out.println(StringUtils.containsIgnoreCase(string, "BANA"));
        System.out.println(StringUtils.containsIgnoreCase(string, "A"));
        System.out.println(StringUtils.containsIgnoreCase(string, "B"));
    }
}
```

📤 **Output:**

```
true
true
true
true
```

---

## 4. StringUtils Java containsAny() Method

There are three overloaded forms of the containsAny() method:

- `public static boolean containsAny(final CharSequence cs, final char... searchChars)`
- `public static boolean containsAny(final CharSequence cs, final CharSequence searchChars)`
- `public static boolean containsAny(final CharSequence cs, final CharSequence... searchCharSequences)`

The first and second methods check if the `CharSequence` contains any character in the given set of characters. The third method checks if the `CharSequence` contains any of the `CharSequences` in the given array.

For all these `containsAny()` methods, a `null` `CharSequence` will return `false`. A `null` or zero-length search array will return `false`.

**Java program:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {

    public static void main(String[] args) {
        String string = "Hello, World";
        System.out.println(StringUtils.containsAny(string, 'X', 'Y', 'Z'));
        System.out.println(StringUtils.containsAny(string, 'l', 'B', 'C'));

        System.out.println(StringUtils.containsAny(string, "Hi"));
        System.out.println(StringUtils.containsAny(string, "ABC"));

        System.out.println(StringUtils.containsAny(string, "Hi", "Hey"));
        System.out.println(StringUtils.containsAny(string, "Hel", "Hey"));
    }
}
```

📤 **Output:**

```
false
true
true
false
false
true
```

---

## 5. Java StringUtils containsNone() Method

The `containsNone(CharSequence cs, char... searchChars)` and `containsNone(CharSequence cs, String invalidChars)` methods check that the `CharSequence` does not contain certain characters. A `null` `CharSequence` will return `true`. A `null` invalid character array will return `true`. An empty `CharSequence` (`length()=0`) always returns `true`.

The `containsNone()` method is the opposite of the `containsAny()` method.

**Java program:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {

    public static void main(String[] args) {
        String string = "Hello, World";
        System.out.println(StringUtils.containsNone(string, 'X', 'Y', 'Z'));
        System.out.println(StringUtils.containsNone(string, 'l', 'B', 'C'));

        System.out.println(StringUtils.containsNone(string, "Hi"));
        System.out.println(StringUtils.containsNone(string, "ABC"));
    }
}
```

📤 **Output:**

```
true
false
false
true
```

---

## 6. Java StringUtils containsOnly() Method

The `containsOnly(CharSequence cs, char... valid)` and `containsOnly(CharSequence cs, String validChars)` methods check if the `CharSequence` contains only certain characters.

A `null` `CharSequence` will return `false`. A `null` valid character array will return `false`. An empty `CharSequence` (`length()=0`) always returns `true`.

**Java program:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {

    public static void main(String[] args) {
        System.out.println(StringUtils.containsOnly("Hi", 'H', 'i', 'o'));
        System.out.println(StringUtils.containsOnly("Hi", 'H', 'i'));

        System.out.println(StringUtils.containsOnly("Hi", "Hi"));
        System.out.println(StringUtils.containsOnly("Hi", "Hello"));
        System.out.println(StringUtils.containsOnly("Hi", "ABC"));
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

> 💡 **Tip:** Use `contains()` for exact substring matching, `containsAny()` when checking for any of multiple characters/strings, `containsNone()` to ensure exclusion, and `containsOnly()` to validate allowed characters.
