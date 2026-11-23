# StringUtils isNumeric() Java

**StringUtils isNumeric() Java** | The `isNumeric()` method is a static method in the `StringUtils` class that checks whether the string contains Unicode digits or not. This method returns `false` if the string has decimal values as decimal values are not considered Unicode digits and also it returns `false` if it contains `null` or the string is empty. Also see: [Unicode character set in Java](017_Unicode_Character_Set_in_Java.md)

- [Java StringUtils isNumeric() Method](#java-stringutils-isnumeric-method)
- [Java isNumeric() StringUtils Example](#java-isnumeric-stringutils-example)

---

## 1. Java StringUtils isNumeric() Method

**Method signature:**

```java
public static boolean isNumeric(final CharSequence cs)
```

- 📥 **Parameters:** `cs` — the string which needs to be checked whether it contains Unicode digits or not
- 📤 **Return type:** `boolean`
- ✅ **Returns:** `true` if the string contains only Unicode digits, or else `false`

🔍 `StringUtils.isNumeric()` checks if the `CharSequence` contains only Unicode digits. A decimal point is not a Unicode digit and returns `false`. A `null` will return `false`. An empty `CharSequence` (`length()=0`) will return `false`.

> ⚠️ **Caution:** The method does not allow for a leading sign, either positive or negative. Also, if a `String` passes the numeric test, it may still generate a `NumberFormatException` when parsed by `Integer.parseInt` or `Long.parseLong`, e.g. if the value is outside the range for `int` or `long` respectively.

| Input 🔍 | Result 📤 | Reason 📝 |
|-----------|-----------|-----------|
| `"4789652"` | ✅ `true` | All Unicode digits |
| `"Hi "` | ❌️ `false` | Contains letters and space |
| `"\u0967\u0968"` (१२) | ✅ `true` | Valid Unicode digits |
| `"   "` | ❌️ `false` | Whitespace only |
| `"-1334"` | ❌️ `false` | Leading sign not allowed |
| `null` | ❌️ `false` | Null input |
| `""` | ❌️ `false` | Empty string |

---

## 2. Java isNumeric() StringUtils Example

**Example 1 — Numeric string:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {

    public static void main(String[] args) {
        String string = "4789652";
        System.out.println(StringUtils.isNumeric(string));
    }
}
```

📤 **Output:**

```
true
```

**Example 2 — String with letters:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {

    public static void main(String[] args) {
        String string = "Hi ";
        System.out.println(StringUtils.isNumeric(string));
    }
}
```

📤 **Output:**

```
false
```

**Example 3 — Unicode digits:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {

    public static void main(String[] args) {
        String string = "\u0967\u0968";
        System.out.println(StringUtils.isNumeric(string));
        System.out.println("String: " + string);
    }
}
```

📤 **Output:**

```
true
String: १२
```

**Example 4 — Whitespace-only string:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {

    public static void main(String[] args) {
        String string = "   ";
        System.out.println(StringUtils.isNumeric(string));
    }
}
```

📤 **Output:**

```
false
```

**Example 5 — Negative number:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {

    public static void main(String[] args) {
        String string = "-1334";
        System.out.println(StringUtils.isNumeric(string));
    }
}
```

📤 **Output:**

```
false
```

Since `StringUtils.isNumeric()` method doesn't allow a leading sign therefore `StringUtils.isNumeric()` method returns `false` for the number `-1334`.

> 💡 **Tip:** If you need to check for numeric strings that include decimal points or signs, consider using `StringUtils.isNumericSpace()` or `NumberUtils.isCreatable()` from Apache Commons Lang instead.
