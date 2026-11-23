# Java String repeat() Method

**Java String repeat() Method** | The `repeat()` method repeats a string N number of times and returns the concatenated result as a new string.

---

## 1. Syntax and Parameters

The syntax for the Java repeat string method:

```java
public String repeat(int count)
```

| Parameter 🏷️ | Description 📋 |
|--------------|----------------|
| **`count`** | Number of times the string needs to be repeated |
| **Return type** | `String` |
| **Returns** | The string with repetition |

If this string is empty or the count is zero then the empty string is returned.

🛠️ **Examples:**

- 🔤 String = `"Hi"`, Count = `2` → Output: `"HiHi"`
- 🔤 String = `"LOL"`, Count = `4` → Output: `"LOLLOLLOLLOL"`

---

## 2. Java String repeat() Method Example

**Repeating a string 4 times:**

```java
public class Main {
   public static void main(String[] args) {
      String str = "Java";
      int count = 4;
      System.out.println("String: " + str.repeat(count));
   }
}
```

📤 **Output:**

```
String: JavaJavaJavaJava
```

We have initialized a string variable with a string literal "Java". Later we called the `repeat()` method of the Java string class by passing count value 4. Therefore it returns `"JavaJavaJavaJava"`.

**Repeat with count = 0:**

```java
public class Main {
   public static void main(String[] args) {
      String str = "Abc";
      int count = 0;
      String str1 = str.repeat(count);
      System.out.println("String: " + str1);
      System.out.println("Length: " + str1.length());
   }
}
```

📤 **Output:**

```
String:
Length: 0
```

Since the count value is 0 therefore Java string `repeat()` method returns an empty string. Similarly, if the input string is empty that case also the `repeat()` method always returns an empty string.

**Repeat on an empty string:**

```java
public class Main {
   public static void main(String[] args) {
      String str = "";

      String str1 = str.repeat(5);
      System.out.println("String1: " + str1);
      System.out.println("Length: " + str1.length());

      String str2 = str.repeat(0);
      System.out.println("String2: " + str2);
      System.out.println("Length: " + str2.length());
   }
}
```

📤 **Output:**

```
String1:
Length: 0
String2:
Length: 0
```

---

## 3. Exceptions Thrown by Java String.repeat() Method

The Java string `repeat()` method throws `IllegalArgumentException` and `OutOfMemoryError`:

- 🚨 **`IllegalArgumentException`** — if the count value is negative
- 💥 **`OutOfMemoryError`** — when `Integer.MAX_VALUE / count < string.length`

**Negative count example:**

```java
public class Main {
   public static void main(String[] args) {
      String str = "Hello";

      String str1 = str.repeat(-5);
      System.out.println("String1: " + str1);
      System.out.println("Length: " + str1.length());
   }
}
```

📤 **Output:**

```
Exception in thread "main" java.lang.IllegalArgumentException: count is negative: -5
```

**MAX_VALUE count example:**

```java
public class Main {
   public static void main(String[] args) {
      String str = "Hello";

      String str1 = str.repeat(Integer.MAX_VALUE);
      System.out.println("String1: " + str1);
      System.out.println("Length: " + str1.length());
   }
}
```

📤 **Output:**

```
Exception in thread "main" java.lang.OutOfMemoryError: Required length exceeds implementation limit
```

If we want to overcome some of these limitations then we can use the StringUtils class repeat() method. There we have explained the limitations of the `String` class `repeat()` method and why we need to use the `StringUtils` class `repeat()` method.

> ⚠️ **Caution:** Like other string class methods, `String` class `repeat()` method also does not handle `null`. When we call the `repeat()` method on a `null` reference then it gives `NullPointerException`. The `StringUtils` class `repeat()` method also gives the option to inject some separator in between the repeated string or characters. See more: StringUtils class repeat() method

---

## 4. How to Repeat a String N Times in Java

To repeat any string in Java N number of times we can use the Java string class `repeat()` method. The value of N must be positive. If the N value is negative then we will get `IllegalArgumentException` and if the N value is zero then we will get an empty string.

**Safe repeat with validation:**

```java
public class Main {
   public static void main(String[] args) {
      String string = "Apple";
      int number = 2;
      String repeatedString = null;
      if(string != null && number >= 0 && number <= Integer.MAX_VALUE) {
          repeatedString = string.repeat(number);
      }
      System.out.println(repeatedString);
   }
}
```

📤 **Output:**

```
AppleApple
```

> 💡 **Tip:** Always validate the count parameter before calling `repeat()` to avoid runtime exceptions. Use a guard condition to ensure the string is not `null` and the count is non-negative.

---

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

**Java Tutorial**

**[String Class Methods](097_String_Class_Methods_In_Java.md)**
- charAt() Method
- codePoints() Method
- [compareTo() Method](106_String_compareTo()_Java.md)
- [compareToIgnoreCase()](107_String_compareToIgnoreCase()_Java.md)
- [concat() Method](113_Concat_Strings_in_Java.md)
- [contains() Method](116_String_contains()_Method_in_Java.md)
- equals() Method
- [equalsIgnoreCase()](105_String_equalsIgnoreCase()_Java.md)
- format() Method
- getBytes() Method
- hashCode() Method
- indent() Method
- [indexOf() Method](110_Java_String_indexOf()_Method.md)
- intern() Method
- [isBlank() Method](124_String_isBlank()_Java_with_Examples.md)
- [isEmpty() Method](100_String_isEmpty()_Java_with_Examples.md)
- isBlank() vs isEmpty()
- [join() Method](098_String_join()_In_Java.md)
- [lastIndexOf() Method](111_String_lastIndexOf()_in_Java.md)
- [length() Method](099_How_to_Find_Length_of_String_in_Java.md)
- matches() Method
- repeat() Method
- [replace() Method](114_Replace()_In_String_Java.md)
- [replaceAll() Method](118_String_replaceAll()_Java.md)
- replaceFirst() Method
- replace() vs replaceAll()
- [split() Method](119_Split()_Method_In_Java.md)
- startsWith() & endsWith()
- strip() & stripLeading()
- [substring() Method](112_Substring_Method_In_Java.md)
- toCharArray() Method
- [toLowerCase() Method](120_Java_String_to_Lowercase.md)
- [toString() Method](126_String_toString()_Java.md)
- toUpperCase() Method
- [trim() Method](122_Trim()_in_Java_String.md)
- [trim() vs strip()](093_Java_String_trim()_Vs_strip().md)
- valueOf() Method
