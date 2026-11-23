# String contains() Method in Java

**String contains() Method in Java** | This page explains the `contains()` method of the String class. The `contains()` method in the String class is **used to search the substring in the string**. If the substring is present it returns `true`, or else `false`. Therefore the return type of `contains()` is `boolean`.

- [Java String Contains Method Example](#java-string-contains-method-example)
- [NullPointerException with contains()](#nullpointerexception-with-contains)

---

## 1. Java String Contains Method Example

Observe the below examples:

- ✅ `"How are you?".contains("How")` --> Result = `true`
- ❌️ `"How are you?".contains("how")` --> Result = `false` (case sensitive)

| Detail 📋 | Description 📝 |
|-----------|---------------|
| **Method Signature** | `public boolean contains(CharSequence ch)` |
| **Return Type** | `boolean` (`true` or `false`) |
| **Parameters** | `ch` - the substring or character sequence to be searched |
| **Throws** | `NullPointerException` if the `CharSequence` is `null` |

> ⚠️ **Caution:** The `contains()` method is **case sensitive**. `"Java"` and `"java"` are treated differently.

**Internal implementation of `contains()` method:**

```java
public boolean contains(CharSequence s) {
   return indexOf(s.toString()) >= 0;
}
```

**Example-1 - Basic `contains()` usage:**

```java
public class Main {
   public static void main(String args[]) {
      String name = "Java Programming Languge";
      System.out.println(name.contains("java"));
      System.out.println(name.contains("Java"));
      System.out.println(name.contains("Language"));
   }
}
```

📤 **Output:**

```
false
true
false
```

**Example-2 - Storing result in a variable:**

```java
public class Main {
   public static void main(String[] args) {
      String str = "Hello Java Readers";
      boolean isContains = str.contains("Java");
      System.out.println(isContains);
      System.out.println(str.contains("java"));
      System.out.println(str.contains("the"));
   }
}
```

📤 **Output:**

```
true
false
false
```

**Example-3 - Using `contains()` with if-else:**

```java
public class Main {
   public static void main(String[] args) {
      String text = "Java Programming Language";
      String word = "Programming";
      if (text.contains(word)) {
         System.out.println("String contains " + word);
      } else {
         System.out.println("String doesn't contains " + word);
      }
   }
}
```

📤 **Output:**

```
String contains Programming
```

---

## 2. NullPointerException with contains()

This code demonstrates in which case `contains()` method of the Java String class throws the `NullPointerException`.

**Example-4 - Passing `null` as argument:**

```java
public class Main {
   public static void main(String argvs[]) {
      String str = "Welcome to Know Program!";
      if (str.contains(null)) {
         System.out.println("Inside the if block");
      } else {
         System.out.println("Inside the else block");
      }
   }
}
```

📤 **Output:**

```
Exception in thread "main" java.lang.NullPointerException: Cannot invoke
"java.lang.CharSequence.toString()" because "s" is null
at java.base/java.lang.String.contains(String.java:2054)
at Main.main(Main.java:4)
```

**Example-5 - Calling `contains()` on a `null` string:**

```java
public class Main {
   public static void main(String argvs[]) {
      String str = null;
      if (str.contains(" ")) {
         System.out.println("Inside the if block");
      } else {
         System.out.println("Inside the else block");
      }
   }
}
```

📤 **Output:**

```
Exception in thread "main" java.lang.NullPointerException: Cannot invoke
"String.contains(java.lang.CharSequence)" because "str" is null
at Main.main(Main.java:4)
```

> 💡 **Tip:** Always perform a `null` check before calling `contains()` to avoid `NullPointerException` at runtime.

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

**Java Tutorial**

**[String Class Methods](097_String_Class_Methods_In_Java.md)**
