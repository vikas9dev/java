# StringUtils.isNotEmpty() Method

**StringUtils.isNotEmpty() Method** | Learn how to use the Apache `StringUtils` `isNotEmpty()` method to check if a string is not empty and not `null`.

- [Apache StringUtils isNotEmpty() Method](#apache-stringutils-isnotempty-method)
- [StringUtils.isNotEmpty() in Java Example-1](#stringutilsisnotempty-in-java-example-1)
- [StringUtils.isNotEmpty() Java Example-2](#stringutilsisnotempty-java-example-2)
- [StringUtils.isNotEmpty() In Java Example-3](#stringutilsisnotempty-in-java-example-3)

---

## 1. Apache StringUtils isNotEmpty() Method

This method is opposite to the StringUtils.isEmpty() method. In the `isEmpty()` method we find whether the given string is empty or not but in the `isNotEmpty()` method we find whether the string is not empty. This method is present in the Apache `StringUtils` class hence to use this method we need to import `StringUtils` class.

| Property 📋 | Details 📖 |
|-------------|-----------|
| **Syntax** | `public static boolean isNotEmpty(final CharSequence cs)` |
| **Purpose** | Checks if a `CharSequence` is not empty (`""`) and not `null` |
| **Parameters** | `CharSequence` — the string to be checked |
| **Return type** | `boolean` |
| **Returns** | `true` if not empty, `false` if empty or `null` |

The `StringUtils.isNotEmpty()` is simply implemented as follows:

**Internal implementation:**

```java
public static boolean isNotEmpty(final CharSequence cs) {
    return !isEmpty(cs);
}
```

| Method Call 🔧 | Result ✨ |
|----------------|----------|
| `StringUtils.isNotEmpty("Hello")` | `true` |
| `StringUtils.isNotEmpty(null)` | `false` |
| `StringUtils.isNotEmpty("")` | `false` |
| `StringUtils.isNotEmpty(" ")` | `true` |

> 📝 **Note:** `isNotEmpty()` considers a whitespace-only string as "not empty". Use `isNotBlank()` if you want to exclude whitespace-only strings as well.

---

## 2. StringUtils.isNotEmpty() in Java Example-1

**Basic usage with string and null:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {

    public static void main(String[] args) {
        String string = "Hello, World!";
        System.out.println(StringUtils.isNotEmpty(string));

        string = null;
        System.out.println(StringUtils.isNotEmpty(string));
    }
}
```

📤 **Output:**

```
true
false
```

- 🔤 The string literal `"Hello, World!"` contains more than `0` characters and hence the `StringUtils.isNotEmpty()` method returns `true`.
- 🔗 The `string` variable contains a reference to `null` therefore `StringUtils.isNotEmpty()` method returns `false`.

---

## 3. StringUtils.isNotEmpty() Java Example-2

**Whitespace and "null" string literal:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {

    public static void main(String[] args) {
        String string = "null";
        System.out.println(StringUtils.isNotEmpty(string));

        string = "   \n\t";
        System.out.println(StringUtils.isNotEmpty(string));
    }
}
```

📤 **Output:**

```
true
true
```

- 🔤 In the string literal `"null"` there are 4 valid characters `'n'`, `'u'`, `'l'`, `'l'`, and it has string length greater than `0` therefore `StringUtils.isNotEmpty()` method returns `true`.
- 📏 The string variable contains only whitespaces. If it were `StringUtils.isNotBlank()` it would return `false` because it excludes whitespaces, but `StringUtils.isNotEmpty()` includes whitespace therefore it returns `true`.

> 💡 **Tip:** If you need to treat whitespace-only strings as empty, use `StringUtils.isNotBlank()` instead of `StringUtils.isNotEmpty()`.

---

## 4. StringUtils.isNotEmpty() In Java Example-3

**Empty string check:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {

    public static void main(String[] args) {
        String string = "";
        System.out.println(StringUtils.isNotEmpty(string));
    }
}
```

📤 **Output:**

```
false
```

📏 The string variable contains an empty string. The length of an empty string is `0` therefore the `StringUtils.isNotEmpty()` method returns `false`.

| Input 🔧 | isEmpty() ✨ | isNotEmpty() ✨ | isBlank() ✨ | isNotBlank() ✨ |
|----------|-------------|----------------|-------------|----------------|
| `"Hello"` | `false` | `true` | `false` | `true` |
| `null` | `true` | `false` | `true` | `false` |
| `""` | `true` | `false` | `true` | `false` |
| `"   "` | `false` | `true` | `true` | `false` |
