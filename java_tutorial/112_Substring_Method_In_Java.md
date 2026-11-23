# Substring Method In Java

**Substring Method In Java** | A substring is a subset of a string. [Java String class](097_String_Class_Methods_In_Java.md) provides a `substring()` method to extract some part of the string. This is a built-in method in Java. There are 2 `substring()` methods in the Java String class including its overloaded form.

- [Java Substring Example](#java-substring-example)
- [Find Substring In Java](#find-substring-in-java)
- [Java Replace Substring](#java-replace-substring)
- [Find Longest Substring Without Repeating Characters Java](#find-longest-substring-without-repeating-characters-java)
- [Java Substring From Character](#java-substring-from-character)

| Method 📋 | Parameter ✂️ | Description 🔤 |
|-----------|-------------|---------------|
| **`substring(int beginIndex)`** | `beginIndex` (inclusive) | Returns substring from beginIndex to end |
| **`substring(int beginIndex, int endIndex)`** | `beginIndex` (inclusive), `endIndex` (exclusive) | Returns substring between the two indices |

- 🚨 **Throws:** `IndexOutOfBoundsException` if `beginIndex` is negative, `endIndex` is larger than the length of the string, or `beginIndex` is larger than `endIndex`.

> 📝 **Note:** The `substring()` method receives two parameters where `beginIndex` is **inclusive** and `endIndex` is **exclusive**.

```mermaid
graph LR
    S["'I Love Programming'"] --> B["beginIndex = 7"]
    B --> R["'Programming'"]

    classDef purple fill:#A162F7,stroke:#A162F7,color:#fff
    classDef cyan fill:#00b4d8,stroke:#00b4d8,color:#fff
    classDef green fill:#28C76F,stroke:#28C76F,color:#fff

    class S purple
    class B cyan
    class R green
```

---

## 1. Java Substring Example

**Example 1 - substring with beginIndex only:**

```java
String string = "I Love Programming";
System.out.println(string.substring(7));
```

📤 **Output:**

```
Programming
```

We have mentioned only one index which is `beginIndex`, therefore the `substring()` method returns all the characters from the given index to the end of the string. Hence the output is "Programming".

**Example 2 - substring with beginIndex and endIndex:**

```java
String string = "I Love Programming";
System.out.println(string.substring(7, 10));
```

📤 **Output:**

```
Pro
```

It returns "Pro" as 'P' starts from index 7 and 'o' is at index 9. This example takes two arguments: the start index and end index, and returns the characters between these two indexes.

---

## 2. Find Substring In Java

In the main method, we call the `substring()` method and specify the start and end index. It returns the specified substring.

**Extracting a substring:**

```java
public class Main {
  public static void main(String[] args) {
    String string = "Know Program";
    String substring = string.substring(5, 12);
    System.out.println(substring);
  }
}
```

📤 **Output:**

```
Program
```

---

## 3. Java Replace Substring

We can also replace a substring with any other string by using the `replace()` method.

**Replacing a substring:**

```java
public class Main {
   public static void main(String args[]) {
      String string = "I love programming";
      String substring = string.substring(7);
      String newString = string.replace(substring, "coding");

      System.out.println("Substring: " + substring);
      System.out.println("New String: " + newString);
   }
}
```

📤 **Output:**

```
Substring: programming
New String: I love coding
```

---

## 4. Find Longest Substring Without Repeating Characters Java

To find the longest substring we can apply the brute-force approach. We loop the string from start to end using a nested loop and if any unique characters are found, return the length of that longest substring.

**Brute-force longest unique substring:**

```java
public class Main {
  public static String longestSubstring(String str) {
    int maxLen = 0;
    int beginIndex = 0;
    int endIndex = 0;
    for (int i = 0; i < str.length(); i++) {
      for (int j = i; j < str.length(); j++) {
        if (repetition(str, i, j)) {
          if(maxLen < (j-i+1)) {
            maxLen = j - i + 1;
            beginIndex = i;
            endIndex = j+1;
          }
        }
      }
    }
    return str.substring(beginIndex, endIndex);
  }

  private static boolean repetition(String str, int start, int end) {
    int[] chars = new int[128];
    for (int i = start; i <= end; i++) {
      char ch = str.charAt(i);
      chars[ch]++;
      if (chars[ch] > 1) {
        return false;
      }
    }
    return true;
  }

  public static void main(String args[]) {
    String str = "Know Program";
    System.out.println(longestSubstring(str));
  }
}
```

📤 **Output:**

```
Know Pr
```

> 💡 **Tip:** It returns "Know Pr" because after 'r', the character 'o' comes which is already available in the substring. This brute-force approach has O(n^3) time complexity. For better performance, consider using the sliding window technique.

---

## 5. Java Substring From Character

The below program returns a substring from a set of characters. Here the `substring()` takes only the start index and returns all the characters from that start index.

**Substring from a given index:**

```java
public class Main {
  public static void main(String args[]) {
    String string = new String("Know Program");
    System.out.print("Substring starting from index 5: ");
    System.out.println(string.substring(5));
  }
}
```

📤 **Output:**

```
Substring starting from index 5: Program
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
- substring() Method
- toCharArray() Method
- [toLowerCase() Method](120_Java_String_to_Lowercase.md)
- [toString() Method](126_String_toString()_Java.md)
- toUpperCase() Method
- [trim() Method](122_Trim()_in_Java_String.md)
- [trim() vs strip()](093_Java_String_trim()_Vs_strip().md)
- valueOf() Method
