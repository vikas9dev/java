# PrintStream Class in Java

**PrintStream Class in Java** | Writing binary data in its native format using `print()`, `println()`, and `write()` methods.

- [Overview](#overview)
- [Java PrintStream Class Constructors](#java-printstream-class-constructors)
- [Java PrintStream Class Methods](#java-printstream-class-methods)
- [Java PrintStream Class Example](#java-printstream-class-example)
- [Writing Data to the Console Using PrintStream](#writing-data-to-the-console-using-printstream)
- [Difference Between write, print, and println Methods](#difference-between-write-print-and-println-methods)
- [Conclusion](#conclusion)

---

## 1. Overview

`PrintStream` class in Java is a sub-class of `FilterOutputStream` class and it is used to write data as it is in the given format. It means, unlike `FileOutputStream` class, `PrintStream` class writes 97 as 97 rather than one byte. It is the most convenient class for writing binary data to another output stream. In addition to default `write()` methods it defines new methods called `print()` and `println()`. These two methods are overloaded to print all types of Java data type values including objects as they are in those formats.

```java
public class PrintStream extends FilterOutputStream
implements Appendable, Closeable
```

`FilterOutputStream` class is a sub class of [OutputStream class](053_OutputStream_in_Java.md).

---

## 2. Java PrintStream Class Constructors

### Constructors with File Parameters

Constructors to create a new print stream, without automatic line flushing, with the specified file:

- `public PrintStream(File file) throws FileNotFoundException`
- `public PrintStream(String fileName) throws FileNotFoundException`

Constructors to create a new print stream, without automatic line flushing, with the specified file and charset:

- `public PrintStream(File file, String csn) throws FileNotFoundException, UnsupportedEncodingException`
- `public PrintStream(String fileName, String csn) throws FileNotFoundException, UnsupportedEncodingException`

### Constructors with OutputStream Parameters

- `public PrintStream(OutputStream out)` — Creates a new print stream, without automatic line flushing, with the specified OutputStream.
- `public PrintStream(OutputStream out, boolean autoFlush)` — Creates a new print stream, with the specified OutputStream and line flushing.
- `public PrintStream(OutputStream out, boolean autoFlush, String encoding) throws UnsupportedEncodingException` — Creates a new print stream, with the specified OutputStream, line flushing, and character encoding.

### Constructors Added in Java 10

- `public PrintStream(File file, Charset charset) throws IOException`
- `public PrintStream(String fileName, Charset charset) throws IOException`
- `public PrintStream(OutputStream out, boolean autoFlush, Charset charset)`

---

## 3. Java PrintStream Class Methods

In `PrintStream` class there are many methods to write data with or without new lines, with or without formatting, etc. These methods are given below.

### print(), println(), and write() Methods

**Overloaded forms of `print()` method** to write data without terminating line:

- `public void print(boolean b)`
- `public void print(char c)`
- `public void print(int i)`
- `public void print(long l)`
- `public void print(float f)`
- `public void print(double f)`
- `public void print(char s[])`
- `public void print(String s)`
- `public void print(Object obj)`

These methods print the given data as it is in the given format because internally these methods call the `String.valueOf()` method to convert given data into String data. Then the returned string data is printed on the destination. Among these methods except `print(char s[])`, all other methods call `write(String.valueOf(x))` method.

**Internal implementation:**

```java
public void print(int i) {
   write(String.valueOf(i));
}
```

**Overloaded forms of `println()` method** to write data with terminating lines:

- `public void println()`
- `public void println(boolean x)`
- `public void println(char x)`
- `public void println(int x)`
- `public void println(long x)`
- `public void println(float x)`
- `public void println(double x)`
- `public void println(char[] x)`
- `public void println(String x)`
- `public void println(Object x)`

The `println()` method calls the `newLine()` method which terminates the current line by writing the line separator string. The line separator string is defined by the system property `line.separator`, and is not necessarily a single newline character `\n`.

**Internal implementation of `println(int)`:**

```java
public void println(int x) {
   if (getClass() == PrintStream.class) {
      writeln(String.valueOf(x));
   } else {
      synchronized (this) {
         print(x);
         newLine();
      }
   }
}
```

**Overloaded forms of `write()` methods:**

- `public void write(int b)`
- `public void write(byte buf[], int off, int len)`

🆕 **Added in Java 14:** Two overloaded forms of `write()` method to write all bytes from the specified byte array:

- `public void write(byte buf[]) throws IOException`
- `public void writeBytes(byte buf[])`

📝 **Note:** In `PrintStream` class only `write(byte buf[])` method throws `IOException`.

### Other Methods

**`format()` method** to write formatted string to the output stream:

- `public PrintStream format(String format, Object ... args)`
- `public PrintStream format(Locale l, String format, Object ... args)`

**`printf()` method** — alternate convenience method to write a formatted string. These methods internally call `format()` method only.

- `public PrintStream printf(String format, Object ... args)`
- `public PrintStream printf(Locale l, String format, Object ... args)`

**`append()` methods** to append the specified character to this output stream:

- `public PrintStream append(CharSequence csq)`
- `public PrintStream append(CharSequence csq, int start, int end)`
- `public PrintStream append(char c)`

**Other important methods:**

| Return Type 🔄 | Method 🛠️ | Description 📋 |
|----------------|-----------|----------------|
| `void` | `flush()` | Flushes the stream |
| `void` | `close()` | Closes the stream. This is done by flushing the stream and then closing the underlying output stream. |
| `boolean` | `checkError()` | Flushes the stream and checks its error state |

---

## 4. Java PrintStream Class Example

**Writing data to a file:**

```java
import java.io.PrintStream;
import java.io.FileNotFoundException;
public class PrintStreamDemo {

   public static void main(String[] args)
    throws FileNotFoundException {

      // create PrintStream object
      PrintStream ps = new PrintStream("output.txt");

      // write data
      ps.println(97);
      ps.println('b');
      ps.println(10.5);
      ps.println(true);
      ps.println("knowprogram");

      // close streams
      ps.close();
   }
}
```

📤 **Data in `output.txt`:**

```
97
b
10.5
true
knowprogram
```

📝 **Note:** If the given destination file `output.txt` doesn't exist then it creates the file itself. (See: Java program to create files and directories). But if the given file object denotes a directory rather than a file, or if some other error occurs while opening or creating the file then it throws `FileNotFoundException`.

💡 **Tip:** Whenever we are calling the `close()` method then first it flushes the stream and then closes the stream. But if automatic flushing is enabled then it will be done every time one of the `println`, `printf`, or `format` methods is invoked.

---

## 5. Writing Data to the Console Using PrintStream

We can directly use `System.out` to invoke `PrintStream` class methods. In `System` class, `out` and `err` are two final variables.

- 📥 `public static final InputStream in;`
- 📤 `public static final PrintStream out;`
- 🚨 `public static final PrintStream err;`

The `in` variable holds a `BufferedInputStream` class object that is connected to the keyboard, whereas `out` and `err` variables hold `PrintStream` class objects that are connected to the console. Since these variables are static final variables so we can access them directly by using System class names like `System.in`, `System.out`, `System.err`. JVM internally uses `System.out` to write output to the console and `System.err` to write exceptions to the console.

**Console output example:**

```java
public class PrintStreamDemo {
   public static void main(String[] args) {
      // write data to the console
      System.out.println(97);
      System.out.println('b');
      System.out.println(10.5);
      System.out.println(true);
      System.out.println("knowprogram");
   }
}
```

---

## 6. Difference Between write, print, and println Methods

### print() vs println()

The `print()` method places the cursor in the same line after printing the data so that the next coming output will be printed in the same line. But the `println()` method places the cursor in the next line after printing data so that the next coming output will be printed in the next line.

**`print()` example:**

```java
ps.print('a');
ps.print('b');
ps.print('c');
// Output:-
// abc
```

**`println()` example:**

```java
ps.println('a');
ps.println('b');
ps.println('c');
// Output:-
// a
// b
// c
```

### print() vs write()

The `print()` or `println()` method first calls `java.lang.String.valueOf()` method and the produced string is translated into bytes and those bytes are written into the file. Whereas the `write()` method directly converts a given number into bytes and writes those bytes into the file. Then the file editor shows those bytes as their corresponding ASCII character.

**`print()` example:**

```java
ps.print(97);
ps.print(98);
// Output:-
// 9798
```

**`write()` example:**

```java
ps.write(97);
ps.write(98);
// Output:-
// ab
```

---

## 7. Conclusion

🔑 **Key Point:** To write binary data to the console or file, `PrintStream` is the best choice. But to write character or text data to the console or file, it is not the best choice.

- ⚡ The message passed using `println()` is passed to the server's console where kernel time is required to execute the task. Kernel time refers to the CPU time.
- 🔒 Since `println()` is a synchronized method, so when multiple threads are passed it could lead to a low-performance issue.
- 🐢 The `println()` is a slow operation as it incurs heavy overhead on the machine compared to most IO operations.

> 💡 **Tip:** [**PrintWriter**](068_PrintWriter_in_Java.md) class gives high performance compared to `PrintStream`. `PrintWriter` class implements most of the methods found in `PrintStream` class, and constructors are also very similar. They are fast as compared to the `println()` of the `PrintStream` class.
