# FileWriter in Java

**FileWriter in Java** | Writing character/text data to files using the `java.io` package

- [Constructors](#constructors)
- [Java FileWriter Class Methods](#java-filewriter-class-methods)
- [FileWriter Java Example](#filewriter-java-example)
- [Newline in Java FileWriter](#newline-in-java-filewriter)
- [FileWriter Append](#filewriter-append)
- [Limitations of FileWriter Class](#limitations-of-filewriter-class)

---

## 1. Constructors

The `FileWriter` class in Java is **used to write character/text data** to the file/console/network. It is defined in the `java.io` package and it is a subclass of `OutputStreamWriter`. The `OutputStreamWriter` class is a subclass of the [Writer class](061_Writer_Class_in_Java.md). Both `OutputStreamWriter` and `Writer` classes are abstract classes.

**Class declaration:**

```java
public class FileWriter
extends OutputStreamWriter
```

Since `FileWriter` is a connection based, where one end is Java application and another end is a File. We must always pass the file information to the constructor. Therefore, it doesn't contain 0 parameter constructor.

**Constructors available in `FileWriter` class:**

- 📄 `public FileWriter(String fileName) throws IOException`
- 📁 `public FileWriter(File file) throws IOException`
- 🔧 `public FileWriter(FileDescriptor fd)`
- ➕ `public FileWriter(String fileName, boolean append) throws IOException`
- ➕ `public FileWriter(File file, boolean append) throws IOException`

The constructors which have only one parameter are used to write data to the file in override mode. The new data will be from the beginning of the file.

The remaining constructors have two parameters that accept append value as `true` or `false`. If we pass `true` then the file will be connected in appended mode and data will be written from the end of the file rather than the beginning. But if we pass `false` then it is similar to the one-parameter constructors i.e. data will be written from the beginning of the file.

💡 **Tip:** If the destination file isn't already available then all the constructors will create the file itself. To create a new file it uses Java `File` class. See: [Java program to create files and directories.](049_Java_Program_to_Create_File.md)

**New constructors added in Java 11 version:**

- 🔤 `public FileWriter(String fileName, Charset charset) throws IOException`
- 🔤 `public FileWriter(String fileName, Charset charset, boolean append) throws IOException`
- 🔤 `public FileWriter(File file, Charset charset) throws IOException`
- 🔤 `public FileWriter(File file, Charset charset, boolean append) throws IOException`

---

## 2. Java FileWriter Class Methods

`FileWriter` class itself doesn't contain any method, all methods are inherited either from super class or from the interfaces. See: [Writer class methods](061_Writer_Class_in_Java.md)

**Write methods:**

| Method 🛠️ | Description 📋 |
|-----------|----------------|
| `write(int c)` | It writes a single character at a time |
| `write(char cbuf[])` | It writes an array of characters |
| `write(char[] ch, int off, int len)` | It writes a portion of an array of characters |
| `write(String str)` | It writes a string |
| `write(String str, int off, int len)` | It writes a portion of a string |

**Other important methods:**

| Return Type 🏷️ | Method 🛠️ | Description 📋 |
|----------------|-----------|----------------|
| `void` | `flush()` | It flushes the stream |
| `void` | `close()` | It closes the stream, flushing it first |

---

## 3. FileWriter Java Example

Now, let us develop a simple Java program to demonstrate the different `write()` methods of `FileWriter` class.

**FileWriter demo:**

```java
import java.io.FileWriter;
import java.io.IOException;
public class FileWriterDemo {
   public static void main(String[] args)
                       throws IOException {

      // create FileWriter object
      FileWriter fw = new FileWriter("output.txt");

      // write data
      fw.write('a');
      fw.write(98);
      fw.write("Welcome to Java programming");
      char ch[] = {'x','y','z'};
      fw.write(ch);

      // display some message
      System.out.println("Data saved to output.txt");

      // close connection
      fw.close();
   }
}
```

📤 **Output:**

```
Data saved to output.txt
```

📄 **Data in output.txt:**

```
abWelcome to Java programmingxyz
```

📝 **Note:** Whenever `close()` method is invoked on the `FileWriter` class object then first it calls the `flush()` method to flush the stream and then closes the connection, releases the resources.

---

## 4. Newline in Java FileWriter

`FileWriter` writes data to the file in a single line. To place a new line we have to use some special character. Which is varied from system to system.

> ⚠️ **Caution:** If the below program doesn't work on your computer then don't worry, read the limitation of `FileWriter` given at the end.

**FileWriter with newline:**

```java
import java.io.FileWriter;
import java.io.IOException;
public class FileWriterDemo {
   public static void main(String[] args)
                       throws IOException {
      FileWriter fw = new FileWriter("output.txt");
      fw.write('a');
      fw.write(98);

      fw.write('\n'); // for new line
      fw.write("Welcome to Java programming");

      fw.write('\n');
      char ch[] = {'x','y','z'};
      fw.write(ch);

      System.out.println("Data saved to output.txt");
      fw.close();
   }
}
```

📄 **Now, data in output.txt is:**

```
ab
Welcome to Java programming
xyz
```

---

## 5. FileWriter Append

Some constructors like `FileWriter(String fileName)` and `FileWriter(File file)` are meant for overriding of the existing data on the file. If we run the previous program multiple times then data in `output.txt` will be overridden i.e. new data will be written from the beginning of the file.

Instead of overriding the data, if we want to append i.e write data from the end of the file then we must use a constructor that accepts boolean values `true`. For append operation, in these constructors pass boolean value `true` as the second parameter. If we pass `false` then the file will be overridden and it is equal to calling one parameter constructor.

**Append mode example:**

```java
FileWriter fw = new FileWriter("output.txt", true);
```

Now file will be opened in append mode, and on every execution data will be written from end of file rather than beginning of file.

---

## 6. Limitations of FileWriter Class

1. ❌️ The main problem with the `FileWriter` is, we have to insert a line separator or new line manually, which is varied from system to system and it is a burden to the programmer. We can solve this problem using [BufferedWriter](066_Java_BufferedWriter.md) and [PrintWriter](068_PrintWriter_in_Java.md) classes.

2. ❌️ Using `FileWriter` class we can write data only to the file not to the console, because it doesn't contain any constructor which can connect with any Streams.

3. ❌️ We can't write primitive data directly, we must convert them to String. For example: if we want to write data 100 to the file then we must pass `"100"` as String. If we pass `100` directly then it will be stored as character `'d'`.

**Primitive data behavior:**

```java
fw.write(100);   // 'd'
fw.write("100"); // 100
fw.write(10.5);  // error
fw.write("10.5"); // 10.5
fw.write(true);  // error
fw.write("true"); // true
```

💡 **Tip:** To solve these problems we can use the `PrintWriter` class. `PrintWriter` class is the most enhanced way to write character or text data to the file. It has a method to write primitive values directly with or without a new line.
