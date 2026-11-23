# How to Find Length of String in Java

**How to Find Length of String in Java** | Java provides a built-in function to find the length of a string: `length()`, and its return type is `int`. Also see: Length of String in Java Without Using length() Method

- [Find the Length of a String in Java Without Using length() Method](#find-the-length-of-a-string-in-java-without-using-length-method)
- [Java String Length Limit](#java-string-length-limit)
- [String Array Length In Java](#string-array-length-in-java)
- [How To Limit String Input Length In Java](#how-to-limit-string-input-length-in-java)

Method Syntax: `public int length()`. It returns an integer value, which is the length of the given string.

**Basic length() example:**

```java
public class Main {
    public static void main(String args[]) {
        String str = "Know Program";
        System.out.println(str.length());
    }
}
```

📤 **Output:**

```
12
```

---

## 1. Find the Length of a String in Java Without Using length() Method

We can also find the length of a string in Java without using the `length()` method and to do this we can take the help of any loop. We will iterate through the string from the start to the end of the character and will count the number of iterations. The number of iterations gives the length of the string.

**Find the length using a while loop and charAt():**

```java
public class Test {
    public static void main(String args[]) {
        String str = "Know Program";
        int length = 0;
        try {
            while (true) {
                str.charAt(length);
                length++;
            }
        } catch (StringIndexOutOfBoundsException e) {
        }
        System.out.println(str.length());
    }
}
```

📤 **Output:**

```
12
```

The charAt() method of the String class fetches the character at the given index, and if we try to access a character at an index less than 0 or greater (where there is no character) then this method throws StringIndexOutOfBoundsException.

> 💡 **Tip:** In the above program, the `length` variable is initialized with 0 therefore it will fetch the first character of the string. Since `while` contains `true` it should run infinitely. But when it tries to fetch a character at an index greater than the length of the string, `charAt()` throws `StringIndexOutOfBoundsException`, and control of the program moves to the catch block. Finally, the `length` variable contains the length of the string.

---

## 2. Java String Length Limit

In this section, we discuss the length limit of the String. A string is a sequence of characters and it is immutable i.e. once created it cannot be changed. The length of the string is usually equal to the [Unicode](017_Unicode_Character_Set_in_Java.md) units in the string.

The `length()` method returns the integer value hence the max length of the string would be -2^31 to 2^31 - 1 that is -2147483648 to 2147483647. As we cannot use a negative value for indexing, the indexing is done from 0 to 2147483647. Hence we can have a string length of up to **2,147,483,647**.

> 📝 **Note:** The snippet below demonstrates the maximum string length and the space available in the heap. For this, we have used `Integer.MAX_VALUE` which stores the maximum possible value of the integer.

**Maximum string length demo:**

```java
import java.util.Arrays;

public class Main {
   public static void main(String args[]) {
      for (int i = 0; i < 1000; i++) {
         try {
            char[] arr = new char[Integer.MAX_VALUE - i];
            Arrays.fill(arr, 'a');
            String string = new String(arr);
            System.out.println(string.length());
         } catch (Throwable e) {
            System.out.println(e.getMessage());
            System.out.println("Last: " + (Integer.MAX_VALUE - i));
            System.out.println("Last: " + i);
         }
      }
   }
}
```

📤 **Output:**

```
Requested array size exceeds VM limit
Last: 2147483647
Last: 0
Requested array size exceeds VM limit
Last: 2147483646
Last: 1
Java heap space
Last: 2147483645
Last: 2
Java heap space
Last: 2147483644
Last: 3
...
```

---

## 3. String Array Length In Java

Now we will find the length of an array. Previously we used `length()` to find the length of the string but to find the length of an array we use the `length` property of the array.

**Array length example:**

```java
public class Main {
   public static void main(String[] args) {
      String[] arr = { "Java", "Python", "C", "C++", "HTML" };
      System.out.println("String array length: " + arr.length);
   }
}
```

📤 **Output:**

```
String array length: 5
```

> 🔑 **Key Point:** For strings, use `length()` (a method with parentheses). For arrays, use `length` (a property without parentheses).

---

## 4. How To Limit String Input Length In Java

Now, we will see how to limit the string input in Java. If the given string is greater than a defined length then it will print "The given string exceeds the maximum length" or else the code returns the string.

**Limiting string input:**

```java
import java.util.Scanner;

public class Main {
   public static void main(String args[]) {
      int max = 5;
      Scanner scan = new Scanner(System.in);
      System.out.print("Enter String: ");
      String str = scan.next();
      if (str.length() <= max) {
         System.out.println(str);
      } else {
         System.out.println("The given string " +
                   "exceeds the maximum length");
      }
      scan.close();
   }
}
```

📤 **Output:**

```
Enter String: Java
Java

Enter String: JavaScript
The given string exceeds the maximum length
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
- length() Method
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
