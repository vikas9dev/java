# Java String hashCode() Method

**Java String hashCode() Method** | Java provides a method called `hashCode()` to retrieve the hash code for strings. It is computed as: `s[0] * 31^(n-1) + s[1] * 31^(n-2) + ... + s[n-1]` where `s[i]` is the ith character, the `^` symbol indicates exponentiation, and `n` is the length of the string.

- [String hashCode() Java](#string-hashcode-java)
- [Java String hashcode() Implementation](#java-string-hashcode-implementation)
- [String hashCode() Java Example](#string-hashcode-java-example)
- [Java String hashCode Example](#java-string-hashcode-example)

The hash value is the encrypted value of the hash function. This [hashCode() method](071_Hashcode_in_Java_–_hashCode()_Method.md) is mainly defined in the [Object class](069_Object_Class_in_Java.md) which is the parent class for all Java classes. Java String class overrides the `hashCode()` method and provides its own implementation different from the Object class.

🧠 **In Simple Words:**

- 🔤 String = `"honey"` => Hashcode value = `99461947`
- 🔤 String = `"kenmore"` => Hashcode value = `-824864855`

---

## 1. String hashCode() Java

| Detail 📋 | Description 🔢 |
|-----------|---------------|
| **Method Signature** | `public int hashCode()` |
| **Parameters** | None |
| **Returns** | Hash value of the string |
| **Return Type** | `int` |

---

## 2. Java String hashcode() Implementation

The `hashCode()` method in the Java String class is implemented as follows:

**Internal implementation:**

```java
public int hashCode() {
   int h = hash;
   if (h == 0 && !hashIsZero) {
      h = isLatin1() ? StringLatin1.hashCode(value)
                     : StringUTF16.hashCode(value);
      if (h == 0) {
         hashIsZero = true;
      } else {
         hash = h;
      }
   }
   return h;
}
```

---

## 3. String hashCode() Java Example

Let us see some examples of the Java String `hashCode()` method to understand how it works and the algorithm it uses to return the results.

**Example 1 - Single character hashCodes:**

```java
class Main {
   public static void main(String[] args) {
      String str = "a";
      String str1 = "A";
      String str2 = "z";
      String str3 = "Z";
      String str4 = "0";
      String str5 = "9";

      System.out.println(str.hashCode());
      System.out.println(str1.hashCode());
      System.out.println(str2.hashCode());
      System.out.println(str3.hashCode());
      System.out.println(str4.hashCode());
      System.out.println(str5.hashCode());
   }
}
```

📤 **Output:**

```
97
65
122
90
48
57
```

> 💡 **Tip:** From the above program, we can observe that the return value for single characters is nothing but the ASCII value. From the algorithm: `s[0] * 31^(n-1)` for string = "A", Hashcode = 65 * 31^(1-1) = 65 * 1 = 65. The ASCII value of 'A' is 65. See more: Java program to find ASCII value.

**Example 2 - Multi-character string hashCodes:**

```java
public class Main {
   public static void main(String[] args) {
      String str = "Hi";
      String str1 = "Java";
      String str2 = "KnowProgram";
      String str3 = "#KnowProgram@2030";

      System.out.println(str.hashCode());
      System.out.println(str1.hashCode());
      System.out.println(str2.hashCode());
      System.out.println(str3.hashCode());
   }
}
```

📤 **Output:**

```
2337
2301506
2058267993
-617909819
```

The hashcode value of string = "Hi" is calculated as follows: 72 * 31^(2-1) + 105 * 31^(2-2) = 72*31 + 105*1 = 2232 + 105 = **2337**.

Similarly the hashcode value of string = "Java" can be calculated as follows: 74 * 31^3 + 97 * 31^2 + 118 * 31 + 97 = 2204534 + 93217 + 3658 + 97 = **2301506**.

> 📝 **Note:** For the string "#KnowProgram@2030" the hashcode value is negative (-617909819). This is because the `hashCode()` return type is `int`. Once the total value exceeds `Integer.MAX_VALUE` (2^31 - 1) range, due to integer overflow it wraps into negative values.

Since the hashcode value is calculated based on the algorithm, there can be cases where **two strings can have the same hashcode**. For example, "FB" and "Ea" have the same hashcode.

**Hash collision example:**

```java
public class Main {
   public static void main(String[] args) {
      String str = "FB";
      String str1 = "Ea";

      System.out.println(str.hashCode());
      System.out.println(str1.hashCode());
   }
}
```

📤 **Output:**

```
2236
2236
```

> ⚠️ **Caution:** Similarly the strings "abyz" & "abz[" have the same hashcode. And "tensada" & "friabili" have the same hashcode. Since the int range is between -2^31 to 2^31-1 there can be infinite possibilities for strings having the same hashcode.

**More collision examples:**

```java
public class Main {
   public static void main(String[] args) {
      String str = "abyz";
      String str1 = "abz[";
      System.out.println(str.hashCode());
      System.out.println(str1.hashCode());

      String str2 = "tensada";
      String str3 = "friabili";
      System.out.println(str2.hashCode());
      System.out.println(str3.hashCode());
   }
}
```

📤 **Output:**

```
2987778
2987778
-1427101464
-1427101464
```

---

## 4. Java String hashCode Example

In this code, we compare two strings and find out whether they have the same hash value or not.

**Comparing hash values:**

```java
public class Main {
   public static void main(String[] args) {
      String str = "K";
      String str1 = "K";
      int hash1 = str.hashCode();
      int hash2 = str1.hashCode();
      if (hash1 == hash2) {
         System.out.println("Values Same");
      } else {
         System.out.println("Not Same");
      }

      String str2 = "a";
      String str3 = "A";
      int hash3 = str2.hashCode();
      int hash4 = str3.hashCode();
      if (hash3 == hash4) {
         System.out.println("Values Same");
      } else {
         System.out.println("Not Same");
      }

      String str4 = "HAPPY";
      String str5 = "Happy";
      int hash5 = str4.hashCode();
      int hash6 = str5.hashCode();
      if (hash5 == hash6) {
         System.out.println("Values Same");
      } else {
         System.out.println("Not Same");
      }

   }
}
```

📤 **Output:**

```
Values Same
Not Same
Not Same
```

> 🔑 **Key Point:** Equal strings always produce the same hash code, but strings with the same hash code are not necessarily equal (hash collision). Also, uppercase and lowercase versions of the same text will produce different hash codes.

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
