# Java String getBytes() Method

**Java String getBytes() Method** | The `getBytes()` method of the Java String class encodes the string into a sequence of bytes and stores the result in a byte array. The `getBytes()` method has three variations.

- [Java String getBytes Default Encoding](#java-string-getbytes-default-encoding)
- [Java String getBytes Encoding](#java-string-getbytes-encoding)
- [Java String getBytes() Charset](#java-string-getbytes-charset)

| Variation 📋 | Method Signature 🔤 | Since 📅 |
|-------------|-------------------|---------|
| **1** | `public byte[] getBytes(String charsetName) throws UnsupportedEncodingException` | Java 1.1 |
| **2** | `public byte[] getBytes(Charset charset)` | Java 1.6 |
| **3** | `public byte[] getBytes()` | Java 1.1 |

---

## 1. Java String getBytes Default Encoding

**Default encoding example:**

```java
import java.util.Arrays;

public class Main {
   public static void main(String args[]) {
      String str = "Hello World!";
      byte[] byteArray = str.getBytes();
      System.out.println(Arrays.toString(byteArray));
   }
}
```

📤 **Output:**

```
[72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33]
```

> 💡 **Tip:** By default, it returns the array of equivalent ASCII values for the characters. The ASCII value of 'a' to 'z' is 97 to 122, 'A' to 'Z' is 65 to 90, and '0' to '9' is 48 to 57. See more here: Java Program to Find ASCII Value.

---

## 2. Java String getBytes Encoding

We can also pass different encoding type names as strings to get a byte array according to the given encoding type. For this, `public byte[] getBytes(String charsetName) throws UnsupportedEncodingException` method will be called. If the named charset is not supported then this `getBytes()` method throws `UnsupportedEncodingException`.

**Encoding with charset name:**

```java
import java.io.UnsupportedEncodingException;
import java.util.Arrays;

public class Main {
   public static void main(String argvs[]) {
      String string = "Welcome to KnowProgram.";
      System.out.println("Input String: " + string);
      try {
         byte[] arrayUTF16 = string.getBytes("UTF-16");
         System.out.println("In UTF-16: "
              + Arrays.toString(arrayUTF16));

         byte[] arrayUTF16BE = string.getBytes("UTF-16BE");
         System.out.println("In UTF-16BE: "
              + Arrays.toString(arrayUTF16BE));

         byte[] arrayISO8859 = string.getBytes("ISO-8859-1");
         System.out.println("In ISO-8859-1: "
              + Arrays.toString(arrayISO8859));

         byte[] arrayUTF16LE = string.getBytes("UTF-16LE");
         System.out.println("In UTF-16LE : "
              + Arrays.toString(arrayUTF16LE));
      } catch (UnsupportedEncodingException uee) {
         System.out.println("Unsupported character set" + uee);
      }
   }
}
```

📤 **Output:**

```
Input String: Welcome to KnowProgram.
In UTF-16: [-2, -1, 0, 87, 0, 101, 0, 108, 0, 99, 0, 111, 0, 109, 0, 101, 0, 32, 0, 116, 0, 111, 0, 32, 0, 75, 0, 110, 0, 111, 0, 119, 0, 80, 0, 114, 0, 111, 0, 103, 0, 114, 0, 97, 0, 109, 0, 46]
In UTF-16BE: [0, 87, 0, 101, 0, 108, 0, 99, 0, 111, 0, 109, 0, 101, 0, 32, 0, 116, 0, 111, 0, 32, 0, 75, 0, 110, 0, 111, 0, 119, 0, 80, 0, 114, 0, 111, 0, 103, 0, 114, 0, 97, 0, 109, 0, 46]
In ISO-8859-1: [87, 101, 108, 99, 111, 109, 101, 32, 116, 111, 32, 75, 110, 111, 119, 80, 114, 111, 103, 114, 97, 109, 46]
In UTF-16LE : [87, 0, 101, 0, 108, 0, 99, 0, 111, 0, 109, 0, 101, 0, 32, 0, 116, 0, 111, 0, 32, 0, 75, 0, 110, 0, 111, 0, 119, 0, 80, 0, 114, 0, 111, 0, 103, 0, 114, 0, 97, 0, 109, 0, 46, 0]
```

---

## 3. Java String getBytes() Charset

We can also pass a `Charset` object directly to the `getBytes()` method. For this, `public byte[] getBytes(Charset charset)` method will be called. The `StandardCharsets` class contains the following charsets:

- 🔤 `US_ASCII`
- 🔤 `ISO_8859_1`
- 🔤 `UTF_8`
- 🔤 `UTF_16BE`
- 🔤 `UTF_16LE`
- 🔤 `UTF_16`

> 📝 **Note:** Unlike passing `charsetName`, when we directly pass a `Charset` object then the `getBytes()` method won't throw any exception.

**Charset object example:**

```java
import java.nio.charset.StandardCharsets;
import java.util.Arrays;

public class Main {
   public static void main(String argvs[]) {
      String string = "Hello, World!";
      System.out.println("Input String: " + string);

      byte[] arrayUTF8 = string.getBytes(StandardCharsets.UTF_8);
      System.out.println("Byte array in UTF-8: "
               + Arrays.toString(arrayUTF8));

      byte[] arrayUTF16 = string.getBytes(StandardCharsets.UTF_16);
      System.out.println("Byte array in UTF-16: "
               + Arrays.toString(arrayUTF16));

      byte[] arrayUTF16BE = string.getBytes(StandardCharsets.UTF_16BE);
      System.out.println("Byte array in UTF-16BE: "
               + Arrays.toString(arrayUTF16BE));

      byte[] arrayUTF16LE = string.getBytes(StandardCharsets.UTF_16LE);
      System.out.println("Byte array in UTF-16LE: "
               + Arrays.toString(arrayUTF16LE));
   }
}
```

📤 **Output:**

```
Input String: Hello, World!
Byte array in UTF-8: [72, 101, 108, 108, 111, 44, 32, 87, 111, 114, 108, 100, 33]
Byte array in UTF-16: [-2, -1, 0, 72, 0, 101, 0, 108, 0, 108, 0, 111, 0, 44, 0, 32, 0, 87, 0, 111, 0, 114, 0, 108, 0, 100, 0, 33]
Byte array in UTF-16BE: [0, 72, 0, 101, 0, 108, 0, 108, 0, 111, 0, 44, 0, 32, 0, 87, 0, 111, 0, 114, 0, 108, 0, 100, 0, 33]
Byte array in UTF-16LE: [72, 0, 101, 0, 108, 0, 108, 0, 111, 0, 44, 0, 32, 0, 87, 0, 111, 0, 114, 0, 108, 0, 100, 0, 33, 0]
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
