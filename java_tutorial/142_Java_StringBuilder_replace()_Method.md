# Java StringBuilder replace() Method

**Java StringBuilder replace() Method** | The `replace()` method substitutes characters in a `StringBuilder` from a start index to an end index with a specified replacement string.

- [Syntax and Parameters](#syntax-and-parameters)
- [Replace StringBuilder Java Example](#replace-stringbuilder-java-example)
- [Java StringBuilder replace() Method Example](#java-stringbuilder-replace-method-example)
- [StringBuilder Replace Java Exception](#stringbuilder-replace-java-exception)

---

## 1. Syntax and Parameters

The `replace()` method of the `StringBuilder` class is used to replace the characters or the substring in the given `StringBuilder` object. The substring or the character begins at the particular index and ends at the particular index according to the user input or the parameters we supply to the `replace()` method.

```java
public StringBuilder replace(int begin, int end, String string)
```

| Parameter 🏷️ | Description 📋 |
|--------------|----------------|
| **`begin`** | The start index from where the replacement should begin |
| **`end`** | The end index where the replacement should end |
| **`string`** | The string which replaces the substring |
| **Return type** | `StringBuilder` |
| **Returns** | The string after replacement |
| **Exception** | Throws `IndexOutOfBoundsException` if the passed parameters are out of bound |

🛠️ **Examples:**

- 🔄 String: `"Hey People"` → Replace `"Hey"` with `"Hi"` → Result: `"Hi People"`
- 🔄 String: `"Good Afternoon"` → Replace `"Afternoon"` with `"Morning"` → Result: `"Good Morning"`

---

## 2. Replace StringBuilder Java Example

In this program, we are passing the string to the constructor of `StringBuilder` and then calling `replace()` method, and then printing the same.

**Basic replace example:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuilder sb = new StringBuilder("Life is too short...!");
      System.out.println("StringBuilder = " + sb);
      StringBuilder sb1 = sb.replace(1, 4, "IFE");
      System.out.println("After replacement = " + sb1);
   }
}
```

📤 **Output:**

```
StringBuilder = Life is too short...!
After replacement = LIFE is too short...!
```

---

## 3. Java StringBuilder replace() Method Example

**Replacing a word in the middle:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuilder sb = new StringBuilder("Tiger is our National Animal");
      System.out.println("StringBuilder = " + sb);
      StringBuilder sb1 = sb.replace(13, 21, " NATIONAL ");
      System.out.println("After replacement = " + sb1);
   }
}
```

📤 **Output:**

```
StringBuilder = Tiger is our National Animal
After replacement = Tiger is our NATIONAL Animal
```

> 📝 **Note:** The `replace()` method modifies the original `StringBuilder` object. The replacement string does not need to be the same length as the portion being replaced.

---

## 4. StringBuilder Replace Java Exception

This code will show you the exception thrown by the `replace()` method. The `replace()` method throws the **StringIndexOutOfBoundsException** when the parameters passed are out of bound.

**Exception example:**

```java
public class Main {
   public static void main(String[] args) {
      StringBuilder sb = new StringBuilder("Hello, World!");
      try {
         StringBuilder sb1 = sb.replace(-15, 16, "Program");
         System.out.println(sb1);
      } catch (Exception e) {
         e.printStackTrace();
      }
   }
}
```

📤 **Output:**

```
java.lang.StringIndexOutOfBoundsException: start -15, end 13, length 13
at java.base/java.lang.AbstractStringBuilder.checkRangeSIOOBE(AbstractStringBuilder.java:1810)
at java.base/java.lang.AbstractStringBuilder.replace(AbstractStringBuilder.java:1000)
at java.base/java.lang.StringBuilder.replace(StringBuilder.java:303)
at Main.main(Main.java:5)
```

> ⚠️ **Caution:** Always ensure the `begin` index is non-negative and less than or equal to the `end` index, and both are within the bounds of the `StringBuilder` length. Otherwise, `StringIndexOutOfBoundsException` will be thrown.

---

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
