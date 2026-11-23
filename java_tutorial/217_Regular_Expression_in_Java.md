# Regular Expression in Java

**Regular Expression in Java** | If we want to represent a group of strings according to a particular pattern then we can use regular expression. Java has provided `Pattern` and `Matcher` classes to work with regular expression. Pattern and Matcher classes are present in the `java.util.regex` package and they were introduced in the Java 1.4 version.

- [Pattern Object in Java](#pattern-object-in-java)
- [Matcher Object in Java](#matcher-object-in-java)
- [Regex Example](#regex-example)
- [Pattern Class split() Method](#pattern-class-split-method)
- [String Class Split() Method](#string-class-split-method)
- [String class split() vs Pattern class split()](#string-class-split-vs-pattern-class-split)
- [String Tokenizer Class In Java](#string-tokenizer-class-in-java)
- [Regular Expression to Represent Valid 10-digit Mobile Number](#regular-expression-to-represent-valid-10-digit-mobile-number)

---

🛠️ **Example:** Write a regular expression representing all valid mobile numbers or mail IDs.

The main important application areas of regular expression are:

- 🔍 To develop validation fieldwork
- 🔎 To develop pattern-matching applications (Example: ctrl + F in Windows, Grep in Unix).
- 🔧 To develop translators like assemblers, compilers, interpreters, etc.
- 🔌 To develop digital circuits, or to develop communication protocols like TCP/IP, UDP, etc.

**Basic pattern matching example:**

Target String: `abbabba`
Search for: `ab`
Find the start index, and end index of each match and display the match.

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class Test {
    public static void main(String[] args) {
        String target = "abbabba";
        String search = "ab";

        // create Pattern and Matcher objects
        Pattern pattern = Pattern.compile(search);
        Matcher matcher = pattern.matcher(target);

        int count = 0;
        while (matcher.find()) {
            count++;
            System.out.println(matcher.start() + " "
                  + matcher.end() + " " + matcher.group());
        }
        System.out.println("Count: " + count);
    }
}
```

📤 **Output:**

```
0 2 ab
3 5 ab
Count: 2
```

To create a Pattern object with a given pattern use the `compile()` static method which is available in the Pattern class. Similarly, the `matcher()` method is available in the Pattern class which returns the Matcher object.

- `start()` => print start index of every match.
- `end()` => print end index of match (end+1)
- `group()` => Which thing is matched

---

## 1. Pattern Object in Java

A pattern object is a compiled version of a regular expression i.e. it is a Java equivalent object of the pattern. We can create a pattern by using the `compile()` method of the pattern class: **`public static Pattern compile(String regex)`**

**Creating a Pattern:**

```java
Pattern pattern = Pattern.compile("ab");
```

---

## 2. Matcher Object in Java

We can use the Matcher object to check the given pattern in the target string. We can create a matcher object by using the `matcher()` method of the Pattern class: **`public Matcher matcher(String target)`**

**Creating a Matcher:**

```java
Matcher matcher = pattern.matcher ("abbabbba");
```

| Method 🔧 | Description 📋 |
|-----------|---------------|
| **`boolean find()`** | It attempts to find, match, and return true if available |
| **`int start()`** | It returns the start index of the match |
| **`int end()`** | It returns the end+1 index of the match |
| **`String group()`** | It returns the matched pattern |

---

## 3. Regex Example

| Regex 🔍 | Search for 📋 |
|----------|--------------|
| **`[abc]`** | Either 'a' or 'b' or 'c' |
| **`[^abc]`** | Except 'a' or 'b' or 'c' |
| **`[a-z]`** | Any lowercase alphabet symbol from a to z |
| **`[A-Z]`** | Any uppercase alphabet symbol from A to Z |
| **`[a-zA-Z]`** | Any alphabet symbol |
| **`[0-9]`** | Any digit |
| **`[a-zA-Z0-9]`** | Any alphanumeric symbol |
| **`[^a-zA-Z0-9]`** | Except for alphanumeric symbols (i.e. search for the special symbol) |

**Character class example:**

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class Test {
    public static void main(String[] args) {
        Pattern pattern = Pattern.compile("[abc]");
        Matcher matcher = pattern.matcher("a3#kb@9z");

        int count = 0;
        while (matcher.find()) {
            count++;
            System.out.println(matcher.start() + " "
                    + matcher.end() + " " + matcher.group());
        }
        System.out.println("Count: " + count);
    }
}
```

📤 **Output:**

```
0 1 a
4 5 b
Count: 2
```

| Regex 🔍 | Search for 📋 |
|----------|--------------|
| **`\s`** | Space character |
| **`\S`** | Except for the space character |
| **`\d`** | Any digit (0-9) |
| **`\D`** | Except for digit |
| **`\w`** | Word (any alphanumeric character) |
| **`\W`** | Except alphanumeric (i.e. special characters) |
| **`.`** (dot) | Any Character |

> 📝 **Note:** The capital letter works exactly opposite to the small letter.

In Java to represent the backslash `\` symbol we should use `\\`.

```java
// not recommended
Pattern pattern = Pattern.compile("\s");

// recommended to use, to avoid any confusion
Pattern pattern = Pattern.compile("\\S");
```

**Quantifiers**

Quantifiers are used to specify the number of occurrences to match.

| Quantifier 🔢 | Meaning 📋 |
|---------------|-----------|
| **`a`** | Exactly one 'a' |
| **`a+`** | At least one 'a' |
| **`a*`** | Any number of 'a' including zero number |
| **`a?`** | At most one 'a' |

**Quantifier example with `a`:**

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class Test {
    public static void main(String[] args) {
        Pattern pattern = Pattern.compile("a");
        Matcher matcher = pattern.matcher("abaabaaab");

        int count = 0;
        while (matcher.find()) {
            count++;
            System.out.println(matcher.start() + " "
                       + matcher.end() + " " + matcher.group());
        }
        System.out.println("Count: " + count);
    }
}
```

📤 **Output:**

```
0 1 a
2 3 a
3 4 a
5 6 a
6 7 a
7 8 a
Count: 6
```

**With `a+` (at least one):**

```java
Pattern pattern = Pattern.compile("a+");
```

📤 **Output:**

```
0 1 a
2 4 aa
5 8 aaa
Count: 3
```

**With `a*` (zero or more):**

```java
Pattern pattern = Pattern.compile("a*");
```

📤 **Output:**

```
0 1 a
1 1
2 4 aa
4 4
5 8 aaa
8 8
9 9
Count: 7
```

**With `a?` (at most one):**

```java
Pattern pattern = Pattern.compile("a?");
```

📤 **Output:**

```
0 1 a
1 1
2 3 a
3 4 a
4 4
5 6 a
6 7 a
7 8 a
8 8
9 9
Count: 10
```

---

## 4. Pattern Class split() Method

To split target string based on space:

```java
import java.util.Arrays;
import java.util.regex.Pattern;

public class Test {
    public static void main(String[] args) {
        Pattern pattern = Pattern.compile("\\s");
        String[] strings = pattern.split("Welcome to Know Program");
        System.out.println(Arrays.toString(strings));
    }
}
```

📤 **Output:**

```
[Welcome, to, Know, Program]
```

We can use the Pattern class `split()` method to split the target string according to a particular pattern.

**Split by character 'o':**

```java
Pattern pattern = Pattern.compile("o");
```

📤 **Output:**

```
[Welc, me t, Kn, w Pr, gram]
```

**How to split based on `.`?**

Target string: `www.knowprogram.com`
Expected output: `[www, knowprogram, com]`

```java
import java.util.Arrays;
import java.util.regex.Pattern;

public class Test {
    public static void main(String[] args) {
        Pattern pattern = Pattern.compile("[.]");
        String[] strings = pattern.split("www.knowprogram.com");
        System.out.println(Arrays.toString(strings));
    }
}
```

---

## 5. String Class Split() Method

String class also contains a `split()` method to split the target String according to the particular pattern.

```java
import java.util.Arrays;

public class Test {
    public static void main(String[] args) {
        String target = "www.knowprogram.com";
        String[] strings = target.split("[.]");
        System.out.println(Arrays.toString(strings));
    }
}
```

---

## 6. String class split() vs Pattern class split()

The pattern class `split()` method can take the **target string** as an argument whereas the string class `split()` method can take the pattern as an argument.

**Pattern.split():**

```java
// In Pattern.split():-
Pattern pattern = Pattern.compile("[.]");
String target = "www.knowprogram.com";
String[] words = pattern.split(target);
```

**String.split():**

```java
// In String.split():-
String target = "www.knowprogram.com";
String[] words = target.split("[.]");
```

---

## 7. String Tokenizer Class In Java

It is a specially designed class for tokenization activity. It is present in `java.util` package.

**Default tokenizer (space delimiter):**

```java
import java.util.StringTokenizer;

public class Test {
    public static void main(String[] args) {
        StringTokenizer tokenizer = new StringTokenizer("Welcome to Know Program");
        while (tokenizer.hasMoreTokens()) {
            System.out.println(tokenizer.nextToken());
        }
    }
}
```

📤 **Output:**

```
Welcome
to
Know
Program
```

The default pattern for StringTokenizer is space.

**Custom delimiter (hyphen):**

Target string: `"01-09-2022"`
Split for `-` hyphen symbol.

```java
import java.util.StringTokenizer;

public class Test {
    public static void main(String[] args) {
        StringTokenizer tokenizer = new StringTokenizer("01-09-2022", "-");
        while (tokenizer.hasMoreTokens()) {
            System.out.println(tokenizer.nextToken());
        }
    }
}
```

📤 **Output:**

```
01
09
2022
```

---

## 8. Regular Expression to Represent Valid 10-digit Mobile Number

Write a regular expression to represent all valid 10-digit mobile numbers.
Rules: Every number should contain exactly 10 digits, the 1st digit should be 7, 8, 9.

- `[789]` => Either 7 or 8 or 9
- `[0-9]` => 0 to 9

Hence regex is:
`[789][0-9][0-9][0-9][0-9][0-9][0-9][0-9][0-9][0-9]`
Or, **`[789][0-9]{9}`**

Mobile numbers can be 10 digits, 11 digits, or 12 digits.

1. If it is 11 digits then the first digit is 0.
2. If it is 12 digits then the first two digits are 91.

Hence regex is: `(0|91)?[789][0-9]{9}`

> 💡 **Tip:** In pattern, `x.z` means `.` can be anything.
