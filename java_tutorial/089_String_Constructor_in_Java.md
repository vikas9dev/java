# String Constructor in Java

**String Constructor in Java** | The String class has a total of 15 constructors among them below 8 are regularly used constructors. All these constructors are overloaded constructors with siblings.

- [Important String Constructor in Java](#important-string-constructor-in-java)
- [Rules for String Constructor in Java with offset and count](#rules-for-string-constructor-in-java-with-offset-and-count)
- [Working with null in String Constructor in Java](#working-with-null-in-string-constructor-in-java)

---

## 1. Important String Constructor in Java

🔤 **Regularly used constructors:**

| # | Constructor 🏷️ | Description 📋 |
|---|----------------|----------------|
| **1** | `public String()` | Creates empty string `""` |
| **2** | `public String(String s)` | Copies given String |
| **3** | `public String(StringBuffer sb)` | Copies from StringBuffer |
| **4** | `public String(StringBuilder sb)` | Copies from StringBuilder |
| **5** | `public String(char[] ch)` | Converts char array to String |
| **6** | `public String(char[] ch, int offset, int count)` | Partial char array to String |
| **7** | `public String(byte[] b)` | Converts byte array to String |
| **8** | `public String(byte[] b, int offset, int length)` | Partial byte array to String |

📝 **Other constructors of String class:**

9. `public String(int[] codePoints, int offset, int count)`
10. `public String(byte bytes[], Charset charset)`
11. `public String(byte bytes[], String charsetName) throws UnsupportedEncodingException`
12. `public String(byte bytes[], int offset, int length, Charset charset)`
13. `public String(byte bytes[], int offset, int length, String charsetName) throws UnsupportedEncodingException`

> ⚠️ **Caution:** Two more string constructors in Java are available, but they are deprecated since the 1.1 version:  
> 14. `public String(byte ascii[], int hibyte)`  
> 15. `public String(byte ascii[], int hibyte, int offset, int count)`

Now let us see important string constructor in Java with examples, and then we will see rules to be followed while using string constructor.

### String()

It creates an empty string object with the content `""` i.e. the string having 0 length or empty character sequence. This constructor is unnecessary since Strings are [immutable](091_Immutable_Class_in_Java.md).

**`public String()` example:**

```java
public class Test1 {
   public static void main(String[] args) {
   String s1 = new String();
   System.out.println("String value: "+ s1);
   }
}
```

📤 **Output:**

```
String value:
```

> 📝 **Note:** It is not equal to the null string referenced variable.

```java
String s = ""; // empty string
String s = null; // null reference
// Both are different
```

In the first line (`String s = "";`) one string object is created with 0 lengths but in the next line String object is not there.

### String(String s)

It creates a String object with given String object characters. It performs a String copy operation.

**`public String(String s)` example:**

```java
public class Test2 {
   public static void main(String[] args) {
      String s = "KnowProgram";

      // string copy
      String s1 = new String(s);

      // creating string directly using string literal
      String s2 = new String("Learn Java");

      // reference assignment
      String s3 = s2;

      System.out.println("Address of String s: " +
                          System.identityHashCode(s));
      System.out.println("String s value: " + s);

      System.out.println("Address of String s1: " +
                          System.identityHashCode(s1));
      System.out.println("String s1 value: " + s1);

      System.out.println("Address of String s2: " +
                          System.identityHashCode(s2));
      System.out.println("String s2 value: " + s2);

      System.out.println("Address of String s3: " +
                          System.identityHashCode(s3));
      System.out.println("String s3 value: " + s3);

      System.out.println(s == s1);
      System.out.println(s2 == s3);
   }
}
```

📤 **Output:**

```
Address of String s: 1259475182
String s value: KnowProgram
Address of String s1: 1072591677
String s1 value: KnowProgram
Address of String s2: 1523554304
String s2 value: Learn Java
Address of String s3: 1523554304
String s3 value: Learn Java
false
true
```

**String copy vs reference assignment:**

```java
// string copy
String s1 = new String(s);
String s2 = new String("Learn Java");
```

In string copy two different String objects are created with same data, it is like a file copy operation in the operating system.

```java
// string reference assignment
String s3 = s2;
```

In string reference assignment current object reference is copied to the destination variable, a new object is not created.

### String(StringBuffer sb)

It creates a new String object with the given StringBuffer object's data. It performs string copy from StringBuffer object to String object.

**`public String(StringBuffer buffer)` example:**

```java
public class Test3 {
   public static void main(String[] args) {
      StringBuffer sb = new StringBuffer();
      sb.append("Java String");

      String str = new String(sb);
      System.out.println(str);
   }
}
```

📤 **Output:**

```
Java String
```

### String(StringBuilder sb)

It creates a new String object with the given StringBuilder object content. It performs string copy operation from StringBuilder object to String object.

**`public String(StringBuilder builder)` example:**

```java
public class Test4 {
   public static void main(String[] args) {
      StringBuilder sb = new StringBuilder();
      sb.append("Learn Java");

      String str = new String(sb);
      System.out.println(str);
   }
}
```

📤 **Output:**

```
Learn Java
```

### String(char[] ch)

It creates a String object with the given char array values. It performs string copy operation from `char[]` object to a String object.

**`public String(char value[])` example:**

```java
public class Test5 {
   public static void main(String[] args) {
      char[] ch = {'K','n','o','w','p','r','o','g','r','a','m'};
      String s = new String(ch);
      System.out.println("String value: "+ s);
   }
}
```

📤 **Output:**

```
String value: Knowprogram
```

### String(char[] ch, int offset, int count)

It creates a new object with the given count number of characters from the given offset in the `char[]` object. Here offset is the starting index from which characters must be copied.

**`public String(char value[], int offset, int count)` parameters:**

- `offset` - the index from which characters should be copied.
- `count` - the number of characters should be copied from the offset.

> 📝 **Note:** The index of an array starts from 0.

```java
class Test6 {
   public static void main(String[] args) {
      char[] ch = {'K','n','o','w','P','r','o','g','r','a','m'};
      String s = new String(ch, 4, 7);
      System.out.println("String value: "+ s);
   }
}
```

📤 **Output:**

```
String value: Program
```

The value of offset is 4 so, the new string will be copied from the 4th index of `ch[]`. The element at the 4th index in the `ch[]` is 'p'. The value of count is 7, so from 'p' 7 elements will be copied. Finally, the new string is "Program".

### String(byte[] b)

It creates a new String object by copying the given `byte[]` numbers by converting them into their ASCII characters.

**`public String(byte[] bytes)` example:**

```java
class Test7 {
   public static void main(String[] args) {
      byte[] b = {65,66,97,98};
      String s = new String(b);
      System.out.println("String value: "+ s);
   }
}
```

📤 **Output:**

```
String value: ABab
```

### String(byte[] b, int offset, int count)

It creates a new String object with the given count number of bytes from the given offset in the `byte[]`. All bytes are stored in their ASCII character form.

**`public String(byte bytes[], int offset, int length)` example:**

```java
class Test8 {
   public static void main(String[] args) {
      byte[] b = {65,66,97,98};
      String s = new String(b, 2, 2);
      System.out.println("String value: "+ s);
   }
}
```

📤 **Output:**

```
String value: ab
```

These were the important constructors given in the String class. Now, let us see some rules regarding String object creation through constructors.

---

## 2. Rules for String Constructor in Java with offset and count

Example of String Constructor in Java with offset and count as parameter values:

- `public String(char[] ch, int offset, int count)`
- `public String(byte[] b, int offset, int length)`

1) The given **offset** argument value must be within the range of [0 to LengthOfString], else it leads to run time exception: **StringIndexOutOfBoundsException**.

The new string object will be copied from the offset. The offset gives the index number, so the index should be >=0 and less than the length of the string.

**Offset validation example:**

```java
public class Rule1 {
   public static void main(String[] args) {
      byte[] b = { 65, 66, 97, 98 };
      String s1 = new String(b, -1, 2); // Exception
      String s2 = new String(b, 0, 2); // Valid
      String s3 = new String(b, 5, 1); // Exception

      char[] ch = { 'a', 'b', 'c', 'd' };
      String s4 = new String(ch, -2, 2); // Exception
      String s5 = new String(ch, 0, 2); // Valid
      String s6 = new String(ch, 4, 2); // Exception
   }
}
```

> ⚠️ **Caution:** Here, we get `java.lang.StringIndexOutOfBoundsException`. Note that the exception is `StringIndexOutOfBoundsException` not the `ArrayIndexOutOfBoundsException`.

2) The given count value depends on offset. The new string object copied from the offset to the given number of count characters. Therefore it also should be valid.

**Count validation example:**

```java
public class Rule2 {
   public static void main(String[] args) {
      char[] ch = { 'a', 'b', 'c', 'd' };
      String s = new String(ch, 0, -4); // Exception
      String s1 = new String(ch, 0, 0); // Valid
      String s2 = new String(ch, 0, 4); // Valid
      String s3 = new String(ch, 0, 5); // Exception
      String s4 = new String(ch, 0, 6); // Exception
   }
}
```

**Valid offset and count example:**

```java
public class Example {
   public static void main(String[] args) {
      char[] ch = { 'a', 'b', 'c', 'd' };
      String s1 = new String(ch, 0, 4);
      System.out.println(s1);
      String s2 = new String(ch, 1, 3);
      System.out.println(s2);
      String s3 = new String(ch, 2, 2);
      System.out.println(s3);
      String s4 = new String(ch, 3, 1);
      System.out.println(s4);
   }
}
```

📤 **Output:**

```
abcd
bcd
cd
d
```

---

## 3. Working with null in String Constructor in Java

**1) We can't pass `null` as argument directly to the constructors of the string class, it leads to compile-time error: ambiguous error because it is matched with all parameters of String constructor in Java.**

**Passing null directly:**

```java
public class Rule1 {
   public static void main(String[] args) {
      String s = new String(null);
      System.out.println("String value: " + s);
   }
}
```

🚨 **Compile-time error:** *reference to String is ambiguous*

```
error: reference to String is ambiguous
	String s = new String(null);
	           ^
  both constructor String(StringBuffer) in String and
  constructor String(StringBuilder) in String match
1 error
```

The `null` is a default value of all referenced variables. So, most of the constructors of the string class can take `null` as an argument. The compiler can't decide that this `null` is passed to which constructor, so it gives an ambiguous error. Read the error message given by the compiler: both constructor `String(StringBuffer)` in String and constructor `String(StringBuilder)` in String match.

**2) We can't create String object with `null` it leads to runtime error: `java.lang.NullPointerException`**

In rule1, we have seen that the compiler gives an ambiguous error because the compiler didn't decide which constructor should be used. But by using casting we can convert the `null` into string-type `null`. In this case, the compiler didn't give any error because this time compiler knows that `(String)null` is used to call constructor having string parameter.

But in this case, the JVM will throw `NullPointerException`. To create a new string object JVM need to perform the copy operation. To copy the string data it should point to the referenced variable. Here, due to `null`, the JVM can't perform the copy operation.

**Casting null to specific types:**

```java
public class Rule2 {
   public static void main(String[] args) {
      String str = null;
      String s1 = new String(str); // Exception
      String s2 = new String((String) null); // Exception
      String s3 = new String((StringBuffer) null); // Exception
      String s4 = new String((StringBuilder) null); // Exception
   }
}
```

🚨 **Exception in thread "main" java.lang.NullPointerException**

> 🔑 **Key Point:** We can create a `null` String referenced variable (in the above program, `str`) but we can't create a String object with `null`. It leads to run time error.
