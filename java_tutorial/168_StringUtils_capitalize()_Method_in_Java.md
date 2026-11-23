# StringUtils capitalize() Method in Java

**StringUtils capitalize() Method in Java** | The `capitalize()` method in the `StringUtils` class capitalizes only the first character in the string. It changes the first character to title case while no other characters are changed.

- [StringUtils.capitalize() Method](#stringutilscapitalize-method)
- [StringUtils.capitalize() Example in Java](#stringutilscapitalize-example-in-java)

---

## 1. StringUtils.capitalize() Method

**Method signature:**

```java
public static String capitalize(final String str)
```

It capitalizes a `String` changing the first character to title case, no other characters are changed.

- 📥 **Parameter:** `str` — the string whose first letter needs to be capitalized
- 📤 **Return type:** `String`
- ✅ **Returns:** the capitalized string

🛠️ **Examples:**

- `"hello"` → `"Hello"`
- `"apple"` → `"Apple"`
- `"mAngo"` → `"MAngo"`

> 📝 **Note:** The `capitalize()` method only changes the **first character** to title case. All other characters remain exactly as they are.

---

## 2. StringUtils.capitalize() Example in Java

**Java program:**

```java
import org.apache.commons.lang3.StringUtils;

public class Main {
    public static void main(String[] args) {
        String string = "banana";
        System.out.println("String: " + string);
        System.out.println("StringUtils.capitalize(string): "
            + StringUtils.capitalize(string));

        string = "aPRICOT";
        System.out.println("String: " + string);
        System.out.println("StringUtils.capitalize(string): "
            + StringUtils.capitalize(string));

        string = "PIne apple";
        System.out.println("String: " + string);
        System.out.println("StringUtils.capitalize(string): "
            + StringUtils.capitalize(string));

        string = "tOmato";
        System.out.println("String: " + string);
        System.out.println("StringUtils.capitalize(string): "
            + StringUtils.capitalize(string));
    }
}
```

📤 **Output:**

```
String: banana
StringUtils.capitalize(string): Banana
String: aPRICOT
StringUtils.capitalize(string): APRICOT
String: PIne apple
StringUtils.capitalize(string): PIne apple
String: tOmato
StringUtils.capitalize(string): TOmato
```

The `capitalize` method is used to capitalize only the first character of the string. In the above code, we have used the signature `StringUtils.capitalize(String str)` and passed four different types of strings to see the output for different scenarios.

This method works the same in all cases — the main use of this method is to make the string in heading format so that only the first letter gets capitalized. The remaining other characters remain as they are.

| Input 🔤 | Output 📤 | Explanation 📝 |
|-----------|-----------|----------------|
| `"banana"` | `"Banana"` | First `'b'` → `'B'` |
| `"aPRICOT"` | `"APRICOT"` | First `'a'` → `'A'`, rest unchanged |
| `"PIne apple"` | `"PIne apple"` | `'P'` is already uppercase, no change |
| `"tOmato"` | `"TOmato"` | First `'t'` → `'T'`, rest unchanged |

> 💡 **Tip:** If you need to capitalize the first letter and lowercase the rest, combine `capitalize()` with `lowerCase()`: `StringUtils.capitalize(StringUtils.lowerCase(str))`.
