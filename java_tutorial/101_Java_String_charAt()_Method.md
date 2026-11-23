# Java String charAt() Method

**Java String charAt() Method** | The `charAt()` method in the Java String class is used to return the character at the specified index. It takes an integer value as a parameter (the index). The index starts from 0 and if the index is greater than the length of the string then `charAt()` throws `IndexOutOfBoundsException`.

- [String charAt() in Java](#string-charat-in-java)
- [Java String charAt() Exception](#java-string-charat-exception)
- [Iterate Through Each Character of The String using charAt() in Java](#iterate-through-each-character-of-the-string-using-charat-in-java)

| Detail 📋 | Description 🔤 |
|-----------|---------------|
| **Method Signature** | `public char charAt(int index)` |
| **Parameter** | `int index` - the index of the character to return |
| **Return Type** | `char` |
| **Exception** | `IndexOutOfBoundsException` when index is negative or >= string length |

---

## 1. String charAt() in Java

Now let us see the code to understand how exactly `charAt()` works. In the below program we retrieve different characters from the same string using different character variables.

**Example 1 - Retrieving characters at various indices:**

```java
public class Main {
   public static void main(String args[]) {
      String str = "KnowProgram";

      char res1 = str.charAt(8);
      char res2 = str.charAt(0);
      char res3 = str.charAt(5);

      System.out.println(res1);
      System.out.println(res2);
      System.out.println(res3);

      System.out.println(str.charAt(3));
      System.out.println(str.charAt(6));
   }
}
```

📤 **Output:**

```
r
K
r
w
o
```

**Example 2 - Storing charAt() result in a variable:**

```java
public class Main {
   public static void main(String args[]) {
      String str = "Welcome to KnowProgram";

      char res = str.charAt(3);
      System.out.println(res);

      res = str.charAt(0);
      System.out.println(res);
   }
}
```

📤 **Output:**

```
c
W
```

---

## 2. Java String charAt() Exception

This program shows the exception thrown by the `charAt()` method. If we pass any negative number or the number greater than or equal to the length of the string then `charAt()` throws **StringIndexOutOfBoundsException**. It is an unchecked exception therefore it is not necessary to handle it using try-catch.

**Exception example:**

```java
public class Main {
   public static void main(String args[]) {
      String str = "KnowProgram";
      System.out.println("String length: " + str.length());
      System.out.println(str.charAt(-5));
      // System.out.println(str.charAt(11));
      // System.out.println(str.charAt(30));
   }
}
```

📤 **Output:**

```
String length: 11
Exception in thread "main" java.lang.StringIndexOutOfBoundsException: String index out of range: -5
at java.base/java.lang.StringLatin1.charAt(StringLatin1.java:48)
at java.base/java.lang.String.charAt(String.java:711)
at Main.main(Main.java:5)
```

> ⚠️ **Caution:** Always ensure the index is between `0` and `length() - 1` (inclusive) before calling `charAt()` to avoid `StringIndexOutOfBoundsException`.

Using [String class length()](099_How_to_Find_Length_of_String_in_Java.md) we can find the length of the string. With the help of the `charAt()` method, we can solve multiple problems related to the string. Some examples are: count the number of vowels in a string, find consonants in the given string, find & count repeated characters in a string in Java, and traverse/iterate through each character of the string.

---

## 3. Iterate Through Each Character of The String using charAt() in Java

To iterate through the character of the string we can use a loop from 0 to the length of the string, and then get the character from the string using the `charAt()` method.

**Iterate using for loop:**

```java
public class Main {
   public static void main(String args[]) {
      String string = "KnowProgram";
      for(int i=0; i<string.length(); i++) {
         System.out.print(string.charAt(i) + " ");
      }
   }
}
```

📤 **Output:**

```
K n o w P r o g r a m
```

**Java Program to Print Vowels in a Given String:**

```java
public class Main {
   public static void main(String args[]) {
      String string = "Hello World!";
      System.out.println("Vowels in the given string are: ");
      for (int i = 0; i < string.length(); i++) {
         char ch = string.charAt(i);
         if (ch == 'a' || ch == 'e' || ch == 'i' ||
            ch == 'o' || ch == 'u' || ch == 'A' ||
            ch == 'E' || ch == 'I' || ch == 'O' || ch == 'U')
            System.out.print(string.charAt(i) + " ");
      }
   }
}
```

📤 **Output:**

```
Vowels in the given string are:
e o o
```

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
