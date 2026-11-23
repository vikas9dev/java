# StringUtils equals() Method

**StringUtils equals() Method** | The `StringUtils.equals()` method compares two different strings and evaluates whether they are equal or not. It returns `true` if the strings are equal or else it returns `false`. The return type of the `equals` method is `boolean`.

- [Java StringUtils equals() Method](#java-stringutils-equals-method)
- [StringUtils equals() Java Example](#stringutils-equals-java-example)
- [StringUtils equalsIgnoreCase() Method Example](#stringutils-equalsignorecase-method-example)
- [StringUtils equalsAny() Method](#stringutils-equalsany-method)
- [StringUtils equalsAnyIgnoreCase() Method](#stringutils-equalsanyignorecase-method)

---

## 1. Java StringUtils equals() Method

The syntax for the `equals` method is as follows:

**Method signature:**

```java
public static boolean equals(final CharSequence cs1, final CharSequence cs2)
```

It compares two `CharSequences`, returning `true` if they represent equal sequences of characters. The `null`s are handled without exceptions. Two `null` references are considered to be equal. The comparison is case-sensitive.

- 📥 **Parameters:**
  - `cs1` — the `CharSequence` needed to be compared
  - `cs2` — the `CharSequence` which is compared
- 📤 **Return type:** `boolean`
- ✅ **Returns:** `true` if the strings are equal and `false` if the strings are not equal

🛠️ **Example:**

- `string1`: `"Hi"`, `string2`: `"People"` — Compare: `false`
- `string1`: `"Hi"`, `string2`: `"Hi"` — Compare: `true`

There are some other similar variations of the `StringUtils.equals()` method:

- 🔤 `equalsIgnoreCase(CharSequence cs1, CharSequence cs2)` — Case-insensitive comparison
- 🔍 `equalsAny(CharSequence string, CharSequence... searchStrings)` — Matches against multiple strings
- 🔎 `equalsAnyIgnoreCase(CharSequence string, CharSequence... searchStrings)` — Case-insensitive match against multiple strings

---

## 2. StringUtils equals() Java Example

**Example 1 — Null and equal strings:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {

    public static void main(String[] args) {
        String string1 = null;
        String string2 = null;
        System.out.println(StringUtils.equals(string1, string2));

        string1 = "Know Program";
        string2 = "Know Program";
        System.out.println(StringUtils.equals(string1, string2));
    }
}
```

📤 **Output:**

```
true
true
```

Initially both string variables referenced to `null` therefore `StringUtils.equals(string1, string2)` returns `true`, and later both strings contain the same value therefore `StringUtils.equals()` method returns `true`.

**Example 2 — Null vs non-null and different strings:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {

    public static void main(String[] args) {
        String string1 = null;
        String string2 = "Hi";
        System.out.println(StringUtils.equals(string1, string2));

        string1 = "Hello";
        System.out.println(StringUtils.equals(string1, string2));
    }
}
```

📤 **Output:**

```
false
false
```

The string variable `string1` is referenced to `null` but the string variable `string2` contains the string literal `"Hi"`. Since both are not similar and don't contain the same characters therefore the `StringUtils.equals()` method returns `false`.

Later string variable `string1` contains the string literal `"Hello"` which is completely different from the string literal `"Hi"` therefore `StringUtils.equals(string1, string2)` method returns `false`.

---

## 3. StringUtils equalsIgnoreCase() Method Example

The `StringUtils.equals()` method compares `CharSequence` case-wise. If we want to ignore the case of string/character then we can use the `StringUtils.equalsIgnoreCase()` method.

**Method signature:**

```java
public static boolean equalsIgnoreCase(final CharSequence cs1, final CharSequence cs2)
```

It compares two `CharSequences`, returning `true` if they represent equal sequences of characters, ignoring the case.

**Java program:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {

    public static void main(String[] args) {
        String string1 = "Hello";
        String string2 = "HELLO";
        System.out.println(StringUtils.equals(string1, string2));
        System.out.println(StringUtils.equalsIgnoreCase(string1, string2));
    }
}
```

📤 **Output:**

```
false
true
```

---

## 4. StringUtils equalsAny() Method

If we have many strings and we want to check whether in these strings there is a specific string, in that case, we can use the `StringUtils.equalsAny()` method.

**Method signature:**

```java
public static boolean equalsAny(final CharSequence string, final CharSequence... searchStrings)
```

It compares the given string to a `CharSequences` vararg of `searchStrings`, returning `true` if the string is equal to any of the `searchStrings`.

**Example 1:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {

    public static void main(String[] args) {
        String string = "Hi";
        System.out.println(StringUtils.equalsAny(string, "Hello", "Hey", "Welcome"));
        System.out.println(StringUtils.equalsAny(string, "Hello", "Hi", "Welcome"));
    }
}
```

📤 **Output:**

```
false
true
```

In the first call of `StringUtils.equalsAny()` the string vararg doesn't contain the `"Hi"` string therefore the `StringUtils.equalsAny()` method returns `false` but in the second call, the string vararg contains the `"Hi"` string therefore the `StringUtils.equalsAny()` method returns `true`.

**Example 2:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {

    public static void main(String[] args) {
        String string = "xyz";
        System.out.println(
           StringUtils.equalsAny(string, "XYZ", "xy", "yz", "x", "y", "z"));
        System.out.println(
           StringUtils.equalsAny(string, "XYZ", "xyz", "yz", "x", "y", "z"));
    }
}
```

📤 **Output:**

```
false
true
```

---

## 5. StringUtils equalsAnyIgnoreCase() Method

The `equalsAnyIgnoreCase` method works like `equalsAny` but ignores the case during comparison.

**Method signature:**

```java
public static boolean equalsAnyIgnoreCase(CharSequence string, CharSequence... searchStrings)
```

**Java program:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {

    public static void main(String[] args) {
        String string = "xyz";
        System.out.println(
           StringUtils.equalsAnyIgnoreCase(string, "wxyz", "xy", "yz", "x", "y", "z"));
        System.out.println(
           StringUtils.equalsAnyIgnoreCase(string, "XYZ", "xy", "yz", "x", "y", "z"));
        System.out.println(
           StringUtils.equalsAnyIgnoreCase(string, "XYZ", "xyz", "yz", "x", "y", "z"));
    }
}
```

📤 **Output:**

```
false
true
true
```

> 💡 **Tip:** Prefer `StringUtils.equals()` over Java's `String.equals()` when either string could be `null`. It handles `null` safely without throwing `NullPointerException`.
