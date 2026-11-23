# Java String valueOf() Method

**Java String valueOf() Method** | The [Java String class](097_String_Class_Methods_In_Java.md) contains the `valueOf()` method which returns the string representation of the given object or primitive type.

- [valueOf() Method Variations](#valueof-method-variations)
- [String.valueOf() Java Example](#stringvalueof-java-example)
- [Java String valueOf() Boolean Example](#java-string-valueof-boolean-example)
- [Java String.valueOf() Character Example](#java-stringvalueof-character-example)
- [String valueOf() Float and Double Example](#string-valueof-float-and-double-example)

---

## 1. valueOf() Method Variations

There are nine variations of the `valueOf()` method:

| Method Signature 🏷️ | Description 📋 |
|----------------------|----------------|
| **`valueOf(boolean bool)`** | Returns the string representation of the boolean argument |
| **`valueOf(char c)`** | Returns the string representation of the character argument |
| **`valueOf(char[] ch)`** | Returns the string representation of the character array argument |
| **`valueOf(char[] ch, int offset, int count)`** | Returns the string representation of a specific element in the character array |
| **`valueOf(double d)`** | Returns the string representation of the double |
| **`valueOf(float floats)`** | Returns the string representation of the float |
| **`valueOf(int i)`** | Returns the string representation of the integer |
| **`valueOf(long l)`** | Returns the string representation of the long |
| **`valueOf(Object object)`** | Returns the string representation of the Object |

---

## 2. String.valueOf() Java Example

Let us see some examples of the Java String class `valueOf()` method. Using the `valueOf()` method we are able to convert primitive type and object values to string type.

**Converting primitives to String:**

```java
public class Main {
   public static void main(String args[]) {
      double d = 7896523.2145994;
      boolean bool = true;
      long lng = 56987412;
      char[] array = { 'P', 'r', 'o', 'g', 'r', 'a', 'm' };

      System.out.println("Return Value: " + String.valueOf(d));
      System.out.println("Return Value: " + String.valueOf(bool));
      System.out.println("Return Value: " + String.valueOf(lng));
      System.out.println("Return Value: " + String.valueOf(array));
   }
}
```

📤 **Output:**

```
Return Value: 7896523.2145994
Return Value: true
Return Value: 56987412
Return Value: Program
```

The `String.valueOf()` method is also useful to convert an array of characters to a string object. We can either convert the complete array to a string object or some portion of the array to a string object.

---

## 3. Java String valueOf() Boolean Example

The below Java program demonstrates how to convert a boolean to a `String` in Java using the `String.valueOf()` method.

**Boolean to String conversion:**

```java
public class Main {
   public static void main(String[] args) {
      boolean bool = true;
      boolean bool2 = false;
      String str1 = String.valueOf(bool);
      String str2 = String.valueOf(bool2);
      System.out.println(str1);
      System.out.println(str2);
   }
}
```

📤 **Output:**

```
true
false
```

---

## 4. Java String.valueOf() Character Example

Using the `String.valueOf()` method we can convert a character into a `String`. For example, if we want to concatenate some character into a string then we can take the help of the `valueOf()` method to convert character to string. Later we can concatenate the string with a string using the concatenation operator.

**Character to String conversion:**

```java
public class Main {
   public static void main(String[] args) {
      char ch1 = 'A';
      char ch2 = 'Z';
      String str1 = String.valueOf(ch1);
      String str2 = String.valueOf(ch2);
      System.out.println(str1);
      System.out.println(str2);

      char ch3 = 's';
      String str3 = "Example";
      String str4 = str3 + String.valueOf(ch3);
      System.out.println(str4);
   }
}
```

📤 **Output:**

```
A
Z
Examples
```

---

## 5. String valueOf() Float and Double Example

**Float and Double to String conversion:**

```java
public class Main {
   public static void main(String[] args) {
      float f = 45.3f;
      double d = 102.25;
      String str1 = String.valueOf(f);
      String str2 = String.valueOf(d);
      System.out.println(str1);
      System.out.println(str2);
   }
}
```

📤 **Output:**

```
45.3
102.25
```

> 💡 **Tip:** `String.valueOf()` is a null-safe alternative to calling `toString()` on an object. If the argument is `null`, it returns the string `"null"` instead of throwing a `NullPointerException`.

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
