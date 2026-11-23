# StringBuilder Class Methods In Java

**StringBuilder Class Methods In Java** | A comprehensive reference of all `StringBuilder` class methods introduced in JDK 1.5, including methods inherited from `AbstractStringBuilder`.

- [StringBuilder Overview](#stringbuilder-overview)
- [StringBuilder Class Core Methods](#stringbuilder-class-core-methods)
- [append() Method Overloads](#append-method-overloads)
- [insert() Method Overloads](#insert-method-overloads)
- [StringBuilder Class Methods Defined in AbstractStringBuilder Class](#stringbuilder-class-methods-defined-in-abstractstringbuilder-class)

---

## 1. StringBuilder Overview

In Java, the `StringBuilder` class was defined in JDK 1.5 version. For storing characters, the `String` class and `StringBuffer` class were already available since the Java 1.0 version, but there were some limitations with both of these classes. The `String` class is immutable and the `StringBuffer` class is synchronized. To overcome these limitations, the `StringBuilder` class was defined in Java 1.5 version.

- ⚡ The `StringBuilder` class is **mutable** — we can modify the `StringBuilder` object without creating a new object
- 🔓 All the methods of the `StringBuilder` class are **non-synchronized** and therefore provide good performance in single thread applications

---

## 2. StringBuilder Class Core Methods

Following are the `StringBuilder` class methods with their purpose or description:

| Method 🏷️ | Description 📋 |
|-----------|----------------|
| **`compareTo(StringBuilder another)`** | Compares two `StringBuilder` instances lexicographically following `CharSequence.compare(this, another)` rules |
| **`delete(int start, int end)`** | Removes the characters in a substring of this sequence |
| **`deleteCharAt(int index)`** | Removes the char at the specified position; sequence is shortened by one char |
| **`replace(int start, int end, String str)`** | Replaces the characters in a substring with characters in the specified String |
| **`indexOf(String str)`** | Returns the index of the first occurrence of the specified substring |
| **`indexOf(String str, int fromIndex)`** | Returns the index of the first occurrence starting at the specified index |
| **`lastIndexOf(String str)`** | Returns the index of the last occurrence of the specified substring |
| **`lastIndexOf(String str, int fromIndex)`** | Returns the index of the last occurrence, searching backward from the specified index |
| **[`reverse()`](141_StringBuilder_reverse()_In_Java.md)** | Causes this character sequence to be replaced by the reverse of the sequence |
| **[`toString()`](139_StringBuilder_toString()_Java.md)** | Returns a string representing the data in this sequence |

---

## 3. append() Method Overloads

The **append()** method of the `StringBuilder` class appends the specified string to this character sequence. `StringBuilder` class has the following overloaded forms of `append()` method:

1. `public StringBuilder append(Object obj)`
2. `public StringBuilder append(String str)`
3. `public StringBuilder append(StringBuffer sb)`
4. `public StringBuilder append(CharSequence s)`
5. `public StringBuilder append(CharSequence s, int start, int end)`
6. `public StringBuilder append(char[] str)`
7. `public StringBuilder append(char[] str, int offset, int len)`
8. `public StringBuilder append(boolean b)`
9. `public StringBuilder append(char c)`
10. `public StringBuilder append(int i)`
11. `public StringBuilder append(long lng)`
12. `public StringBuilder append(float f)`
13. `public StringBuilder append(double d)`

**append() example:**

```java
public class Main {
    public static void main(String[] args) {
        StringBuilder string = new StringBuilder();
        string.append("Hello");
        string.append(',');
        string.append(2030);
        string.append(" ");
        string.append(50.99);
        string.append(true);
        System.out.println(string);
    }
}
```

📤 **Output:**

```
Hello,2030 50.99true
```

---

## 4. insert() Method Overloads

The `StringBuilder` class **insert()** method inserts the string representation of the argument into this sequence at the specified offset. `StringBuilder` class has the following overloaded forms of `insert()` method:

1. `public StringBuilder insert(int offset, float flt)`
2. `public StringBuilder insert(int offset, int i)`
3. `public StringBuilder insert(int offset, long lng)`
4. `public StringBuilder insert(int offset, Object objt)`
5. `public StringBuilder insert(int offset, String string)`
6. `public StringBuilder insert(int ind, char[] array, int offset, int len)`
7. `public StringBuilder insert(int dstOffset, CharSequence seq)`
8. `public StringBuilder insert(int dstOffset, CharSequence seq, int begin, int end)`
9. `public StringBuilder insert(int offset, double dbl)`
10. `public StringBuilder insert(int offset, boolean bool)`
11. `public StringBuilder insert(int offset, char c)`
12. `public StringBuilder insert(int offset, char[] array)`

**insert() example:**

```java
public class Main {
    public static void main(String[] args) {
        StringBuilder string = new StringBuilder("Hello, World!");
        string.insert(0, true);
        System.out.println(string);
        string.insert(1, "Hi");
        System.out.println(string);
    }
}
```

📤 **Output:**

```
trueHello, World!
tHirueHello, World!
```

---

## 5. StringBuilder Class Methods Defined in AbstractStringBuilder Class

The `StringBuilder` class extends `AbstractStringBuilder`. The `AbstractStringBuilder` class also contains many methods for [string handling](088_String_Handling_in_Java.md). Therefore they are also available for `StringBuilder` objects.

| Method 🏷️ | Description 📋 |
|-----------|----------------|
| **`length()`** | Returns the length or character count |
| **`capacity()`** | Returns the current capacity |
| **`ensureCapacity(int minimumCapacity)`** | Ensures capacity is at least equal to the specified minimum |
| **`trimToSize()`** | Attempts to reduce storage used for the character sequence |
| **`setLength(int newLength)`** | Sets the length of the character sequence |
| **`charAt(int index)`** | Returns the char value at the specified index |
| **`codePointAt(int index)`** | Returns the Unicode code point at the specified index |
| **`codePointBefore(int index)`** | Returns the Unicode code point before the specified index |
| **`codePointCount(int beginIndex, int endIndex)`** | Returns the number of Unicode code points in the specified range |
| **`offsetByCodePoints(int index, int codePointOffset)`** | Returns the index offset by the given code points |
| **`getChars(int srcBegin, int srcEnd, char[] dst, int dstBegin)`** | Copies characters into the destination character array |
| **`setCharAt(int index, char ch)`** | Sets the character at the specified index to `ch` |
| **`appendCodePoint(int codePoint)`** | Appends the string representation of the code point |
| **`substring(int start)`** | Returns a new `String` containing a subsequence from the start index |
| **`substring(int start, int end)`** | Returns a new `String` containing a subsequence between start and end |
| **`subSequence(int start, int end)`** | Returns a new `CharSequence` that is a subsequence of this sequence |

**Other Methods:**

- 🔤 `IntStream chars()` — Returns a stream of `int` zero-extending the `char` values
- 🔢 `IntStream codePoints()` — Returns a stream of code point values

> 📝 **Note:** The `StringBuilder` class inherits methods from both the `AbstractStringBuilder` class and the `Object` class, making it a powerful tool for mutable string manipulation in single-threaded environments.

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
