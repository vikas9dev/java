# Escape Sequence In Java

**Escape Sequence In Java** | Understanding escape characters, their Unicode values, and usage in Java programs including text blocks.

- [Escape Character in Java](#escape-character-in-java)
- [Java Escape Sequence Example](#java-escape-sequence-example)
- [New Escape Characters](#new-escape-characters)

---

In Java, the escape sequence is a character preceded by a backslash (`\`) and it has special meaning to the compiler, JVM, Console, and Editor software. Every escape character must start with `\` following by a single character.

The escape sequence changes the original meaning of a character. When we place `\` before a character then it is not considered as a regular character some special functionality will be added. For example, if we use just `'n'`, then it is treated as a character `'n'`.

**Without escape character:**

```java
System.out.println("Know n Program");
```

📤 **Output:**

```
Know n Program
```

But if we place `\` before `'n'` then its meaning is changed and now it represents a new line:

**With escape character:**

```java
System.out.println("Know \n Program");
```

📤 **Output:**

```
Know
 Program
```

When an escape sequence is encountered in a print statement, the compiler interprets it accordingly. For example, if you want to put quotes within quotes you must use the escape sequence, `\"`, on the interior quotes.

---

## 1. Escape Character in Java

Java supports following escape characters:

| Escape Character 🔤 | Description 📋 | [Unicode Value](017_Unicode_Character_Set_in_Java.md) 🔢 |
|---------------------|---------------|-------------|
| `\b` | Backspace | `\u0008` |
| `\t` | Horizontal tab | `\u0009` |
| `\n` | New line | `\u000a` |
| `\f` | Form feed | `\u000c` |
| `\r` | Carriage return | `\u000d` |
| `\"` | Double quote | `\u0022` |
| `\'` | Single quote | `\u0027` |
| `\\` | Backslash | `\u005c` |

---

## 2. Java Escape Sequence Example

The `\t` **escape character** is used to insert one tab space (generally 5 space) between the text.

```java
System.out.println("Java\tKnow\tProgram");
```

📤 **Output:**

```
Java	Know	Program
```

The `\n` **escape character** is used to insert one line between the text.

```java
System.out.println("Java\nKnow\nProgram");
```

📤 **Output:**

```
Java
Know
Program
```

The `\b` **escape character** moves the cursor one character back with or without deleting the character. The output depends on the compiler.

```java
System.out.println("Java\bKnow\bProgram");
```

📤 **Output:**

```
JavKnoProgram
```

The `\f` **escape sequence** is a form feed character. It is an old technique and used to indicate a page break. The output depends on the compiler.

```java
System.out.println("Java\fKnow\fProgram");
```

📤 **Output:**

```
Java
     Know
         Program
```

The **carriage return** `\r` moves the output point back to the beginning of the line without moving down a line. The output depends on the compiler.

```java
System.out.println("Java\rKnow\rProgram");
System.out.println("\rJava");
System.out.println("Java\rKnow");
```

📤 **Output:**

```
Program
Java
Know
```

The **backslash escape character** `\\` is used to represent `\`. It contains two backslashes, this means after reading the first `\` the compiler read the next `\` as a new character.

```java
System.out.println("The file is located"
             +" at C:\\KnowProgram\\Java");
```

📤 **Output:**

```
The file is located at C:\KnowProgram\Java
```

### Simple Programs

**Program1: Display 'K' within single quote and double quote.**

```java
System.out.println("'K'"); // 'K'
System.out.println("\'K\'"); // 'K'

// System.out.println(""K""); // error
System.out.println("\"K\""); // "K"
```

**Program2: Print the following text: She said "Hello!" to me.**

```java
System.out.println("She said \"Hello!\" to me.");
```

**Program3: Display the following folder: D:\Java\Program**

```java
System.out.println("D:\Java\Program"); // error
System.out.println("D:\\Java\\Program"); // valid
// Output:- D:\Java\Program
```

---

## 3. New Escape Characters

To support text block features two escape characters are introduced in Java 15 version. These are:

| Escape Character 🔤 | Description 📋 |
|---------------------|---------------|
| `\` (at end of line) | Line-terminator |
| `\s` | Insert space |

A text block is a new kind of literal in the Java language. It may be used to denote a string anywhere that a string literal could appear, but offers greater expressiveness and less accidental complexity. A text block consists of zero or more content characters, enclosed by opening and closing delimiters.

**Text block example:**

```java
"""
line 1
line 2
line 3
"""
```

is equivalent to the string literal:

```java
"line 1\nline 2\nline 3\n"
```

or a concatenation of string literals:

```java
"line 1\n" +
"line 2\n" +
"line 3\n"
```

**Use of line-terminator** (`\`)

Generally, we split a long string into smaller substring and then using `+` operator convert them into multiple lines.

```java
String text = "Lorem ipsum dolor sit amet, consectetur adipiscing " +
              "elit, sed do eiusmod tempor incididunt ut labore " +
              "et dolore magna aliqua.";
```

In text block using line-terminator it can be simply written as:

```java
String text = """
                Lorem ipsum dolor sit amet, consectetur adipiscing \
                elit, sed do eiusmod tempor incididunt ut labore \
                et dolore magna aliqua.\
                """;
```

**Use of `\s`**

Escape sequences aren't translated until after incidental space stripping, so `\s` can act as a fence to prevent the stripping of trailing white space. Using `\s` at the end of each line in this example guarantees that each line is exactly six characters long:

```java
String colors = """
    red  \s
    green\s
    blue \s
    """;
```

> 📝 **Note:** The `\s` escape sequence can be used in text blocks, traditional string literals, and character literals. Learn More: [Text blocks](https://openjdk.org/jeps/378)
