# Java StringUtils substring() Method

**Java StringUtils substring() Method** | The `substring` method in the `StringUtils` class returns a substring from the specified start and end index. There are several variations of this method as listed below.

- 🔤 `substring(String str, int start)` — Gets a substring from the specified start index
- ✂️ `substring(String str, int start, int end)` — Gets a substring from start to end index
- ➡️ `substringAfter(String str, int/String separator)` — Gets the substring after the first occurrence of a separator
- ⏩ `substringAfterLast(String str, int/String separator)` — Gets the substring after the last occurrence of a separator
- ⬅️ `substringBefore(String str, int/String separator)` — Gets the substring before the first occurrence of a separator
- ⏪ `substringBeforeLast(String str, String separator)` — Gets the substring before the last occurrence of a separator
- 🔍 `substringBetween(String str, String tag)` — Gets the string nested between two instances of the same string
- 🔎 `substringBetween(String str, String open, String close)` — Gets the string nested between two different strings
- 📦 `substringsBetween(String str, String open, String close)` — Returns all matching substrings in an array

- [Java StringUtils substring() Method Examples](#java-stringutils-substring-method-examples)

---

## 1. Java StringUtils substring() Method Examples

**Example 1 — `substring()`:**

Let us see an example of `substring(String str, int start)` and `substring(String str, int start, int end)`.

```java
import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        String str = "The pen is mightier than the,,, sword...!";
        System.out.println("The substring is:" + StringUtils.substring(str, 7));
        System.out.println("The substring is:" + StringUtils.substring(str, 7, 20));
    }
}
```

📤 **Output:**

```
The substring is: is mightier than the,,, sword...!
The substring is: is mightier
```

**Example 2 — `substringAfter()`:**

Let us see an example of `substringAfter(String str, int separator)` and `substringAfter(String str, String separator)`.

```java
import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        String str = "The pen is mightier than the,,, sword...!";
        System.out.println("The substring is:" + StringUtils.substringAfter(str, 7));
        System.out.println("The substring is:" + StringUtils.substringAfter(str, "."));
    }
}
```

📤 **Output:**

```
The substring is:
The substring is:..!
```

**Example 3 — `substringAfterLast()`:**

Let us see an example of `substringAfterLast(String str, int separator)` and `substringAfterLast(String str, String separator)`.

```java
import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        String str = "The pen is mightier than the,,, sword...!";
        System.out.println("The substring is:" + StringUtils.substringAfterLast(str, 9));
        System.out.println("The substring is:" + StringUtils.substringAfterLast(str, ","));
    }
}
```

📤 **Output:**

```
The substring is:
The substring is: sword...!
```

**Example 4 — `substringBefore()` and `substringBeforeLast()`:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        String str = "The pen is mightier than the,,, sword...!";
        System.out.println("The substring is: " + StringUtils.substringBefore(str, 4));
        System.out.println("The substring is: " + StringUtils.substringBefore(str, ","));
        System.out.println("The substring is: " + StringUtils.substringBeforeLast(str, ","));
    }
}
```

📤 **Output:**

```
The substring is: The pen is mightier than the,,, sword...!
The substring is: The pen is mightier than the
The substring is: The pen is mightier than the,,
```

**Example 5 — `substringBetween()` and `substringsBetween()`:**

```java
import java.util.Arrays;

import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        String str = "The pen is mightier than the,,, sword...!";
        System.out.println("The substring is: "
                + StringUtils.substringBetween(str, ","));
        System.out.println("The substring is: "
                + StringUtils.substringBetween(str, "5", "10"));
        System.out.println("The substring is: "
                + StringUtils.substringBetween(str, "m", "d"));
        System.out.println("The substring is: "
                + Arrays.toString(StringUtils.substringsBetween(str, "m", "d")));
    }
}
```

📤 **Output:**

```
The substring is:
The substring is: null
The substring is: ightier than the,,, swor
The substring is: [ightier than the,,, swor]
```

> 💡 **Tip:** All `StringUtils.substring*()` methods are null-safe and avoid `StringIndexOutOfBoundsException`. Unlike Java's built-in `String.substring()`, these methods return `null` or empty strings instead of throwing exceptions.
