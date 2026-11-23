# String lastIndexOf() in Java

**String lastIndexOf() Method in Java** | The String `lastIndexOf()` method is a built-in method in the [Java String class](097_String_Class_Methods_In_Java.md) that returns the last index or occurrence of the given character or substring.

- [Java String lastIndexOf() Example](#java-string-lastindexof-example)
- [String lastIndexOf() Java Example](#string-lastindexof-java-example)
- [Java lastIndexOf() Quiz](#java-lastindexof-quiz)

For the `lastIndexOf()` method the index counter starts from 0, and if the character or substring is not found it returns -1. Similar to `lastIndexOf()`, the Java String class also contains the [indexOf() method](110_Java_String_indexOf()_Method.md).

🧠 **In Simple Words:**

- 🔍 `"Good Morning".lastIndexOf('g')` => 11 (last 'g' is at index 11)
- ❌️ `"Happy day".lastIndexOf('z')` => -1 (not found)
- 🔍 `"It was a great day".lastIndexOf("great")` => 9

There are four variations in the `lastIndexOf()` method:

| Method 📋 | Description 🔍 |
|-----------|---------------|
| **`lastIndexOf(int char1)`** | Returns last index of the character |
| **`lastIndexOf(int char1, int fromIndex)`** | Returns last index of character at or before `fromIndex` |
| **`lastIndexOf(String substring)`** | Returns last index of the substring |
| **`lastIndexOf(String substring, int fromIndex)`** | Returns last index of substring at or before `fromIndex` |

- 🔤 **Parameters:** `char1` - the character to search; `substring` - the substring to search; `fromIndex` - start the search from this index (searching backwards).
- 📤 **Returns:** The index of the character/string. -1 if character/substring is not found.
- 🔢 **Return Type:** `int`

---

## 1. Java String lastIndexOf() Example

Let us see an example for the `public int lastIndexOf(int char1)` method. We will take a character that exists multiple times and one character which doesn't exist.

**lastIndexOf(int char1) example:**

```java
public class Main {
   public static void main(String args[]) {

      String string = "Have a great day!";
      char ch1 = 'a';
      char ch2 = 'X';

      int lastIndex1 = string.lastIndexOf(ch1);
      int lastIndex2 = string.lastIndexOf(ch2);

      System.out.println("Last Index of \'" + ch1
            + "\' at = " + lastIndex1);
      System.out.println("Last Index of \'" + ch2
            + "\' at = " + lastIndex2);
   }
}
```

📤 **Output:**

```
Last Index of 'a' at = 14
Last Index of 'X' at = -1
```

**lastIndexOf(int char1, int fromIndex) example:**

It will return the index of the last character at or before the given index position.

```java
public class Main {
   public static void main(String args[]) {
      String str = "Hello people";
      System.out.println(str.lastIndexOf('e', str.length()));
      System.out.println(str.lastIndexOf('e', 9));
      System.out.println(str.lastIndexOf('e', 5));
   }
}
```

📤 **Output:**

```
11
7
1
```

> 💡 **Tip:** Calling `str.lastIndexOf('e', str.length())` and `str.lastIndexOf('e')` will always produce the same result.

**Negative fromIndex always returns -1:**

```java
public class Main {
   public static void main(String args[]) {
      String str = "Hello people";
      System.out.println(str.lastIndexOf('e', -1));
      System.out.println(str.lastIndexOf('e', -9));
      System.out.println(
          str.lastIndexOf('e', Integer.MIN_VALUE));
   }
}
```

📤 **Output:**

```
-1
-1
-1
```

> 📝 **Note:** If we pass the second parameter < 0 then we will always get -1, because there is no character/string before the 0th index, and it will not search in circular order.

---

## 2. String lastIndexOf() Java Example

We have already seen the `lastIndexOf()` example for the character. Now let us see examples for the sub-string. The method signature is `public int lastIndexOf(String substring)`.

Since Java is a case-sensitive programming language, it will compare case-wise. It will return the last index of the given sub-string from the given string. If the sub-string is not available then it returns -1.

**lastIndexOf(String substring) example:**

```java
public class Main {
   public static void main(String args[]) {
      String str = "Welocome to Knowprogram. "
         + "Java is one of the popular programming language";

      System.out.println(str.lastIndexOf("program"));
      System.out.println(str.lastIndexOf("one"));
      System.out.println(str.lastIndexOf("Hello"));
   }
}
```

📤 **Output:**

```
52
33
-1
```

**lastIndexOf(String substring, int fromIndex) example:**

Here also, if the passed second argument is < 0 then we will always get -1 because it won't compare in circular order.

```java
public class Main {
   public static void main(String args[]) {
      String str = "Fear leads to anger;"
            + " anger leads to hatred;"
            + " hatred leads to conflict;"
            + " conflict leads to suffering.";

      System.out.println(str.lastIndexOf("leads", str.length()));
      System.out.println(str.lastIndexOf("leads", 70));
      System.out.println(str.lastIndexOf("leads", 41));
      System.out.println(str.lastIndexOf("leads", 17));
      System.out.println(str.lastIndexOf("leads", 4));
   }
}
```

📤 **Output:**

```
79
51
27
5
-1
```

---

## 3. Java lastIndexOf() Quiz

**Q1)** Which of these will give the same result for `String name = "KnowProgram"`?

- a) `name.lastIndexOf('o')`
- b) `name.lastIndexOf('o', name.length())`
- c) `name.lastIndexOf('o', Integer.MAX_VALUE)`
- d) `name.lastIndexOf('o', Integer.MIN_VALUE)`

> 🔑 **Answer:** (a), (b), and (c). All three search from the end of the string (or beyond), so they find the same last 'o'. Option (d) returns -1 because `Integer.MIN_VALUE` is negative.

---

**Q2)** Find the output of the below program.

```java
public class Main {
   public static void main(String args[]) {
      String name = "KnowProgram";
      System.out.println(name.lastIndexOf("KnowProgram"));
   }
}
```

- a) 1
- b) 0
- c) -1
- d) None of these

> 🔑 **Answer:** (b) 0
>
> Explanation: The index starts from 0. The sub-string "KnowProgram" starts from the 0th index in the given string "KnowProgram". Therefore the program will return 0 as output.

---

**Q3)** Find the output of the below program.

```java
public class Main {
   public static void main(String args[]) {
      String name = "KnowProgram";
      System.out.println(name.lastIndexOf("o", -0));
   }
}
```

- a) 1
- b) 0
- c) -1
- d) None of these

> 🔑 **Answer:** (c) -1

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
- lastIndexOf() Method
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
