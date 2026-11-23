# PrintWriter in Java

**PrintWriter in Java** | The most enhanced Writer for character/text data with primitive data support in the `java.io` package

- [Constructors in PrintWriter Class](#constructors-in-printwriter-class)
- [Methods in PrintWriter Class](#methods-in-printwriter-class)
- [PrintWriter Java Example](#printwriter-java-example)
- [Difference Between write, print, and println Methods](#difference-between-write-print-and-println-methods)
- [Writing Data to the Console Using PrintWriter](#writing-data-to-the-console-using-printwriter)
- [Advantage of Java PrintWriter Class](#advantage-of-java-printwriter-class)

---

## 1. Constructors in PrintWriter Class

In Java, the `PrintWriter` class is the most enhanced Writer to write character or text data to the file. The biggest advantage of `PrintWriter` over [FileWriter](064_FileWriter_in_Java.md) and [BufferedWriter](066_Java_BufferedWriter.md) is: we can write any primitive data directly with or without a newline character, and methods of `PrintWriter` class never throw `IOException`.

It is defined in the [java.io](https://docs.oracle.com/en/java/javase/15/docs/api/java.base/java/io/package-summary.html) package and it is the subclass of [Writer](061_Writer_Class_in_Java.md). `PrintWriter` class can be used to write character data not only to the file but also on the console.

Since `PrintWriter` is a connection based, where one end is a Java application and another end is a file or console. We must always pass the file or console information to the constructor. Therefore, it doesn't contain 0 parameter constructor. `PrintWriter` can directly communicate to the file and also communicate via some `Writer` object.

**Constructors for direct file communication:**

- 📄 `public PrintWriter(String fileName) throws FileNotFoundException`
- 📁 `public PrintWriter(File file) throws FileNotFoundException`
- 🔤 `public PrintWriter(String fileName, String csn) throws FileNotFoundException, UnsupportedEncodingException`
- 🔤 `public PrintWriter(File file, String csn) throws FileNotFoundException, UnsupportedEncodingException`

**Constructors for stream communication (typically console):**

- 🔗 `public PrintWriter(Writer out)`
- 🔗 `public PrintWriter(Writer out, boolean autoFlush)`
- 🔄 `public PrintWriter(OutputStream out)`
- 🔄 `public PrintWriter(OutputStream out, boolean autoFlush)`

**Constructors added in Java 10:**

- ⚙️ `public PrintWriter(OutputStream out, boolean autoFlush, Charset charset)`
- ⚙️ `public PrintWriter(String fileName, Charset charset) throws IOException`
- ⚙️ `public PrintWriter(File file, Charset charset) throws IOException`

---

## 2. Methods in PrintWriter Class

`PrintWriter` class contains multiple overloaded methods to write primitive data with or without line separator. This class implements all of the print methods found in `PrintStream`. In `PrintWriter` class, if automatic flushing is enabled then it will be done only when one of the `println`, `printf`, or `format` methods is invoked. In the `PrintWriter` class, none of the methods throw `IOException`.

**Overloaded `print()` methods:**

- 🔹 `print(boolean b)`
- 🔹 `print(char ch)`
- 🔹 `print(int i)`
- 🔹 `print(long l)`
- 🔹 `print(float f)`
- 🔹 `print(double d)`
- 🔹 `print(char s[])`
- 🔹 `print(String s)`
- 🔹 `print(Object obj)`

📝 **Note:** In all these methods the produced bytes are written in exactly the manner of the `write(int)` method. **Internally every `print()` is using `write(int)` method.**

**Overloaded `println()` methods:**

- 🔸 `println()`
- 🔸 `println(boolean x)`
- 🔸 `println(char x)`
- 🔸 `println(int x)`
- 🔸 `println(long x)`
- 🔸 `println(float x)`
- 🔸 `println(double x)`
- 🔸 `println(char x[])`
- 🔸 `println(String x)`
- 🔸 `println(Object x)`

The overloaded forms of `println()` are used to write data with a line separator. The `println()` methods directly write a new line. Remaining all methods internally call `print(type)` and `println()` method. For example:

**Internal implementation of println(int):**

```java
public void println(int x) {
    synchronized (lock) {
        print(x);
        println();
    }
}
```

**Overloaded `write()` methods:**

- ✍️ `write(int c)`
- ✍️ `write(char buf[])`
- ✍️ `write(char buf[], int off, int len)`
- ✍️ `write(String s)`
- ✍️ `write(String s, int off, int len)`

📝 **Note:** Since all overloaded forms of `write()`, `print()` and `println()` methods are given to write the data that's why return type of **these methods are `void`.**

**Other important methods:**

| Method 🛠️ | Description 📋 |
|-----------|----------------|
| `flush()` | It flushes the stream |
| `close()` | Closes the stream and releases any system resources associated with it |
| `checkError()` | It flushes the stream if it's not closed and checks its error state |

**Additional formatting and append methods:**

- 📝 `PrintWriter printf(String format, Object ... args)`
- 📝 `PrintWriter printf(Locale l, String format, Object ... args)`
- 📝 `PrintWriter format(String format, Object ... args)`
- 📝 `PrintWriter format(Locale l, String format, Object ... args)`
- ➕ `PrintWriter append(char c)`
- ➕ `PrintWriter append(CharSequence csq)`
- ➕ `PrintWriter append(CharSequence csq, int start, int end)`

---

## 3. PrintWriter Java Example

**Java program to demonstrate methods of `PrintWriter` class and saving data to the file:**

```java
import java.io.PrintWriter;
import java.io.FileNotFoundException;
public class PrintWriterDemo {

   public static void main(String[] args)
    throws FileNotFoundException {

      // create object of PrintWriter
      PrintWriter pw = new PrintWriter("output.txt");

      // write data
      pw.println(97);
      pw.println('b');
      pw.println(10.5);
      pw.println(true);
      pw.println("knowprogram");

      // close streams
      pw.close();
   }
}
```

📄 **Data in output.txt:**

```
97
b
10.5
true
knowprogram
```

📝 **Note:** Whenever `close()` method is called on `PrintWriter` object then first it flushes the data from stream to file and then closes the connection. But if automatic flushing is enabled then it will be done every time when one of the `println`, `printf`, or `format` methods is invoked.

---

## 4. Difference Between write, print, and println Methods

### print vs println

The `print` method places the cursor in the same line after printing the data so that the next coming output will be printed in the same line. But the `println` method places the cursor in the next line after printing data so that the next coming output will be printed in the next line.

**print() example:**

```java
pw.print('a');
pw.print('b');
pw.print('c');
// Output: abc
```

**println() example:**

```java
pw.println('a');
pw.println('b');
pw.println('c');
// Output:
// a
// b
// c
```

### print vs write

The `print` or `println` method first calls `java.lang.String.valueOf()` method and the produced string is translated into bytes and writes those bytes into the file. Whereas the `write` method directly converts given number into bytes and writes those bytes into the file. Then the file editor shows those bytes as its corresponding ASCII character.

**print() behavior:**

```java
pw.print(97);
pw.print(98);
// Output: 9798
```

**write() behavior:**

```java
pw.write(97);
pw.write(98);
// Output: ab
```

---

## 5. Writing Data to the Console Using PrintWriter

To create `PrintWriter` class object connecting to the console:

1. Pass `System.out` as an argument to `OutputStreamWriter` object creation
2. Pass `OutputStreamWriter` as an argument to `PrintWriter` object creation

**Connection setup:**

```java
OutputStreamWriter osw = new OutputStreamWriter(System.out);
PrintWriter pw = new PrintWriter(osw);
```

**Java program to write data to the console:**

```java
import java.io.OutputStreamWriter;
import java.io.PrintWriter;
public class PrintWriterDemo {
   public static void main(String[] args) {

      // create PrintWriter object
      PrintWriter pw = new PrintWriter(
             new OutputStreamWriter(System.out));

      // write data to the file
      pw.println(97);
      char[] ch1 = {'a', 'b', 'c', 'd'};
      pw.println(ch1);
      pw.println("knowprogram");
      pw.println("Hello, World!");

      // close stream
      pw.close();
   }
}
```

📤 **Output:**

```
97
abcd
knowprogram
Hello, World!
```

---

## 6. Advantage of Java PrintWriter Class

- ✅ We can write any primitive data directly
- ✅ Data can be written with or without a new line character
- ✅ Methods of `PrintWriter` class never throw `IOException`
- ✅ `PrintWriter` class can write data both on the file or the console
