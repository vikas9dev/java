# StringUtils isEmpty() Method

**StringUtils isEmpty() Method** | Learn how to use the `isEmpty()` method from the `StringUtils` class to check whether a string is empty or `null`.

- [Java StringUtils isEmpty() Method](#java-stringutils-isempty-method)
- [StringUtils.isEmpty() Method](#stringutilsisempty-method)
- [String class isEmpty() vs StringUtils.isEmpty() Method](#string-class-isempty-vs-stringutilsisempty-method)
- [Related Links](#related-links)

---

## 1. Java StringUtils isEmpty() Method

The `isEmpty()` method is a static method present in the `StringUtils` class. We can use this method to check whether the string is empty or not. We consider the string is empty only when it satisfies the below criteria:

- 📏 If the size or length of the string is zero.
- 🔗 If the string points to a `null` reference.

The syntax of `isEmpty()` is as follows:

**`public static boolean isEmpty(final CharSequence cs)`**

It checks if the `CharSequence` is `null` or empty.

| Property 📋 | Details 📖 |
|-------------|-----------|
| **Parameters** | `CharSequence cs` — the string needed to be checked |
| **Return type** | `boolean` |
| **Returns** | `true` if empty or `null`, `false` otherwise |

| Method Call 🔧 | Result ✨ |
|----------------|----------|
| `StringUtils.isEmpty("Hello")` | `false` |
| `StringUtils.isEmpty(null)` | `true` |
| `StringUtils.isEmpty("")` | `true` |
| `StringUtils.isEmpty(" ")` | `false` |

> ⚠️ **Caution:** `isEmpty()` does **not** trim the string. A string containing only whitespace (like `" "`) will return `false`. Use `isBlank()` to detect whitespace-only strings.

---

## 2. StringUtils.isEmpty() Method

To use any methods of `StringUtils` we need to import it from Apache as `import org.apache.commons.lang3.StringUtils`. In the below program, we have used the `isEmpty()` method for five different strings so that we can understand the `isEmpty()` method more clearly.

**Java code:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        String string = "Good morning";
        System.out.println("StringUtils.isEmpty() = " + StringUtils.isEmpty(string));

        string = null;
        System.out.println("StringUtils.isEmpty() = " + StringUtils.isEmpty(string));

        string = "null";
        System.out.println("StringUtils.isEmpty() = " + StringUtils.isEmpty(string));

        string = "    \n\t";
        System.out.println("StringUtils.isEmpty() = " + StringUtils.isEmpty(string));

        string = "";
        System.out.println("StringUtils.isEmpty() = " + StringUtils.isEmpty(string));
    }
}
```

📤 **Output:**

```
StringUtils.isEmpty() = false
StringUtils.isEmpty() = true
StringUtils.isEmpty() = false
StringUtils.isEmpty() = false
StringUtils.isEmpty() = true
```

- 🔤 The string `"Good morning"` has a length greater than `0` including the whitespaces therefore `StringUtils.isEmpty()` method returns `false`.
- 📝 The `StringUtils.isEmpty()` doesn't trim the given string, therefore if the string contains only whitespaces then also it will return `false`.

Also see: StringUtils isBlank() Method

---

## 3. String class isEmpty() vs StringUtils.isEmpty() Method

Java `String` class also contains `isEmpty()` method to check whether the given string is empty or not, but it has the following main difference from `StringUtils.isEmpty()` method:

| Feature ⚖️ | String.isEmpty() 🅰️ | StringUtils.isEmpty() 🅱️ |
|------------|---------------------|--------------------------|
| **Method type** | Instance method | ✅ Static method |
| **Null handling** | ❌️ Throws `NullPointerException` | ✅ Returns `true` |
| **Requires object** | ✅ Yes | ❌️ No |
| **Import needed** | ❌️ No (built-in) | ✅ Apache Commons Lang |

Since `String` class `isEmpty()` method is an instance (non-static) method, the string object must exist to call it. If the string is referring to `null`, we will get `NullPointerException`.

Whereas `StringUtils.isEmpty()` method is a static method and therefore if we pass a string referring to `null` then it will return `true` instead of `NullPointerException`. The below example demonstrates it:

**Comparison example:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        String string = null;
        System.out.println("StringUtils.isEmpty() = " + StringUtils.isEmpty(string));
        System.out.println("String isEmpty() = ");
        System.out.println(string.isEmpty());
    }
}
```

📤 **Output:**

```
StringUtils.isEmpty() = true
String isEmpty() =
Exception in thread "main" java.lang.NullPointerException
at Main.main(Main.java:8)
```

> 💡 **Tip:** Always prefer `StringUtils.isEmpty()` over `String.isEmpty()` when the string could potentially be `null` to avoid `NullPointerException`.

---

## 4. Related Links

Also see: [String class isEmpty() method](100_String_isEmpty()_Java_with_Examples.md)
