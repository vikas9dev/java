# Java StringBuffer reverse() Method

**Java StringBuffer reverse() Method** | Learn how to reverse strings using the built-in `reverse()` method in the `StringBuffer` class and a custom recursive approach.

- [Method Syntax and Parameters](#method-syntax-and-parameters)
- [How To Reverse A String In Java Using StringBuffer](#how-to-reverse-a-string-in-java-using-stringbuffer)
- [Java StringBuffer reverse() Example](#java-stringbuffer-reverse-example)
- [How To Reverse A String In Java Without Using StringBuffer](#how-to-reverse-a-string-in-java-without-using-stringbuffer)
- [Related Links](#related-links)

---

## 1. Method Syntax and Parameters

The `reverse()` method is a built-in method in the `StringBuffer` that is used to reverse each and every character in the `StringBuffer` object. This helps to reverse the characters in the string.

| Property 📋 | Details 📖 |
|-------------|-----------|
| **Syntax** | `public StringBuffer reverse()` |
| **Parameters** | None |
| **Return type** | `StringBuffer` |
| **Returns** | The string which is reversed |

🔍 **Examples:**
- String: `"Hello"` — After reversing: `"olleH"`
- String: `"Calendar"` — After reversing: `"radnelaC"`
- String: `"098756"` — After reversing: `"657890"`

```mermaid
graph LR
    A["'Hello'"] --> B["reverse()"]
    B --> C["'olleH'"]

    classDef purple fill:#A162F7,stroke:#A162F7,color:#fff
    classDef cyan fill:#00b4d8,stroke:#00b4d8,color:#fff
    classDef green fill:#28C76F,stroke:#28C76F,color:#fff

    class A purple
    class B cyan
    class C green
```

---

## 2. How To Reverse A String In Java Using StringBuffer

In the below program we have created the `StringBuffer` object and passed the string `"Books"` to it, then used the `reverse()` method to reverse the `StringBuffer` object.

**Reversing a string:**

```java
public class Main {
    public static void main(String args[]) {
        StringBuffer sb = new StringBuffer("Books");
        System.out.println("StringBuffer = " + sb);
        sb.reverse();
        System.out.println("StringBuffer after reversing = " + sb);
    }
}
```

📤 **Output:**

```
StringBuffer = Books
StringBuffer after reversing = skooB
```

---

## 3. Java StringBuffer reverse() Example

Here, we use an integer as an example. We pass the integer to the `StringBuffer` and then reverse the integer string.

**Reversing a numeric string:**

```java
public class Main {
    public static void main(String args[]) {
        StringBuffer sb = new StringBuffer("5698745123");
        System.out.println("StringBuffer = " + sb);
        sb.reverse();
        System.out.println("StringBuffer after reversing = " + sb);
    }
}
```

📤 **Output:**

```
StringBuffer = 5698745123
StringBuffer after reversing = 3215478965
```

> 💡 **Tip:** The `reverse()` method works on the `StringBuffer` in-place, meaning it modifies the original object rather than creating a new one.

---

## 4. How To Reverse A String In Java Without Using StringBuffer

Now we use a user-defined method to reverse the string, that is we create our own method using recursion and call the same in the main method.

**Recursive string reversal:**

```java
public class Main {
    public static void reverseStr(String str) {
        if ((str == null) || (str.length() <= 1)) {
            System.out.println(str);
        }
        else {
            System.out.print(str.charAt(str.length() - 1));
            reverseStr(str.substring(0, str.length() - 1));
        }
    }

    public static void main(String[] args) {
        String str = "Pen and pencil";
        System.out.println("String: " + str);
        System.out.print("String after reverse: ");
        reverseStr(str);
    }
}
```

📤 **Output:**

```
String: Pen and pencil
String after reverse: licnep dna neP
```

🧠 **In Simple Words:** The recursive method picks the last character, prints it, and then calls itself with the remaining substring (excluding the last character) until the string is empty or has one character left.

Also see: Reverse a String In Java Using Recursion, [how to reverse a string in Java without using StringBuffer](090_How_to_Take_&_Return_a_String_in_Java.md)

---

## 5. Related Links

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

**Java Tutorial**

- [Import StringBuffer Class](132_Import_StringBuffer_In_Java.md)
- [StringBuffer vs StringBuilder](133_When_To_Use_StringBuffer_And_StringBuilder_In_Java.md)
- String To StringBuilder
- StringBuilder To String
- [String To StringBuffer](136_Java_String_To_StringBuffer.md)
- [StringBuffer To String](136_Java_String_To_StringBuffer.md)

**StringBuilder Methods**

- [toString() Method](139_StringBuilder_toString()_Java.md)
- substring() Method
- [reverse() Method](141_StringBuilder_reverse()_In_Java.md)
- replace() Method
- length() Method
- indexOf() Method
- insert() Method
- append() Method
- capacity() Method
- charAt() Method

**StringBuffer Methods**

- append() Method
- insert() Method
- length() Method
- reverse() Method
