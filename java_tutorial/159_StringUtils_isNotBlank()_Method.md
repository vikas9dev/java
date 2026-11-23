# StringUtils isNotBlank() Method

**StringUtils isNotBlank() Method** | The `isNotBlank()` method in the `StringUtils` class is used to check whether the string is not blank or not. It is just the opposite of the `StringUtils.isBlank()` method where `isBlank()` checks if the string is empty or not but `isNotBlank()` checks if the string is not empty or not. If the string is empty then `isNotBlank()` returns `false`, or else if the string is not empty then it returns `true`.

- [Java StringUtils isNotBlank() Method](#java-stringutils-isnotblank-method)
- [StringUtils.isNotBlank() Example-1](#stringutilsisnotblank-example-1)
- [StringUtils.isNotBlank() Java Example-2](#stringutilsisnotblank-java-example-2)
- [isNotBlank() StringUtils Example-3](#isnotblank-stringutils-example-3)

---

## 1. Java StringUtils isNotBlank() Method

The syntax for the `isNotBlank()` method is as follows:

**Method signature:**

```java
public static boolean isNotBlank(final CharSequence cs)
```

It checks if a `CharSequence` is not empty (`""`), not `null`, and not whitespace only.

- 📥 **Parameters:** `CharSequence` to check
- 📤 **Return type:** `boolean`
- ✅ **Returns:** `true` if the string contains some characters, or else `false`

🛠️ **Internal implementation:**

```java
public static boolean isNotBlank(final CharSequence cs) {
    return !isBlank(cs);
}
```

| Method Call 🔍 | Result 📤 |
|----------------|-----------|
| `StringUtils.isNotBlank("Hello")` | ✅ `true` |
| `StringUtils.isNotBlank(null)` | ❌️ `false` |
| `StringUtils.isNotBlank("")` | ❌️ `false` |
| `StringUtils.isNotBlank(" ")` | ❌️ `false` |

---

## 2. StringUtils.isNotBlank() Example-1

**Java program:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {

   public static void main(String[] args) {
      String string = "Know Program";
      System.out.println(StringUtils.isNotBlank(string));

      string = null;
      System.out.println(StringUtils.isNotBlank(string));
   }
}
```

📤 **Output:**

```
true
false
```

The string literal `"Know Program"` has a length greater than 0 excluding the whitespaces therefore `StringUtils.isNotBlank()` method returns `true`. But where the string is referencing to `null` in that case it is not holding any actual characters, therefore, `StringUtils.isNotBlank()` method returns `false`.

---

## 3. StringUtils.isNotBlank() Java Example-2

**Java program:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {

   public static void main(String[] args) {
      String string = "null";
      System.out.println(StringUtils.isNotBlank(string));

      string = "   \n\t";
      System.out.println(StringUtils.isNotBlank(string));
   }
}
```

📤 **Output:**

```
true
false
```

Here also the string literal `"null"` has length greater than 0 therefore `StringUtils.isNotBlank()` method returns `true`. Note that it is not a `null` reference rather it is a valid string literal with characters `'n'`, `'u'`, `'l'`, `'l'`.

Whereas the string literal `" \n\t"` contains only whitespaces therefore the `StringUtils.isNotBlank()` method returns `false` because it is not containing any valid character and has length 0 (excluding whitespaces).

---

## 4. isNotBlank() StringUtils Example-3

**Java program:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {

    public static void main(String[] args) {
        String string = "";
        System.out.println(StringUtils.isNotBlank(string));
    }
}
```

📤 **Output:**

```
false
```

In this example, the variable contains an empty string literal and its length is 0. Hence `StringUtils.isNotBlank()` method returns `false`.

> 💡 **Tip:** Use `isNotBlank()` instead of manually checking for `null`, empty, and whitespace-only strings. It combines all three checks into a single null-safe call.
