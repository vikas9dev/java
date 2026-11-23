# Java FileOutputStream

**Java FileOutputStream** | Writing binary data to a file one byte at a time using the `FileOutputStream` class from `java.io`.

- [Overview](#overview)
- [Methods of FileOutputStream](#methods-of-fileoutputstream)
- [Java FileOutputStream Example](#java-fileoutputstream-example)
- [Limitation of Java FileOutputStream](#limitation-of-java-fileoutputstream)

---

## 1. Overview

`FileOutputStream` class in Java is used to write binary data to the file. It is a subclass of [**OutputStream**](053_OutputStream_in_Java.md) class and it is available from Java 1.0 version onwards. It is used for writing data into a file in a binary format one byte at a time. These data can be number, character, boolean, image etc.

```java
public class FileOutputStream
extends OutputStream
```

Since `FileOutputStream` is connection-based, where one end is a Java application and another end is a File, we must always pass the file information to the constructor. Therefore, it doesn't contain a 0 parameter constructor.

### Constructors

- `public FileOutputStream(String name) throws FileNotFoundException`
- `public FileOutputStream(File file) throws FileNotFoundException`
- `public FileOutputStream(FileDescriptor file) throws FileNotFoundException`
- `public FileOutputStream(String name, boolean append) throws FileNotFoundException`
- `public FileOutputStream(File file, boolean append) throws FileNotFoundException`

The constructor having only one parameter will write data in the file from the beginning. If we want to append the file, instead of overriding then we must use constructors having two parameters. If we pass append as `true` then existing data of the file won't be overridden and new data will be written from the end of the file. But if we pass append as `false` then it is similar to the one-parameter constructor without append values which will override the existing data.

📝 **Note:** If the file is not available then the `FileOutputStream` class constructors itself creates the new file. But these constructors throw [**FileNotFoundException**](060_FileNotFoundException_in_Java.md) not because the file is not available but because of the below reasons:

- 🚨 File doesn't exist and doesn't have file creation permission.
- 📂 The passed file name is a directory or folder rather than a regular file.
- 🔒 File is available but writing permission is not there i.e. it is a read-only file.

> ⚠️ **Caution:** Generally in C drive of Windows OS we can create folder/directory only, not the file. Similarly in Linux we can't create file in another user's directory.

---

## 2. Methods of FileOutputStream

`FileOutputStream` is a subclass of `OutputStream`, so all its superclass methods are inherited. The important methods are given below. All these methods throw `IOException` if an input/output error occurs.

| Method 🛠️ | Description 📋 |
|-----------|----------------|
| `void write(int b)` | Writes the specified byte to this file output stream |
| `void write(byte b[])` | Writes `b.length` bytes from the specified byte array to this file output stream |
| `void write(byte b[], int off, int len)` | Writes `len` bytes from the specified byte array starting at offset `off` to the file output stream |
| `void close()` | Closes this file output stream and releases any system resources associated with this stream |

🔧 **Other Methods:**

- `public FileChannel getChannel()`
- `public final FileDescriptor getFD() throws IOException`

---

## 3. Java FileOutputStream Example

**Steps to writing binary data into a file using FileOutputStream:**

1️⃣ Import `java.io` package or required classes
2️⃣ Create `FileOutputStream` class object, let us say its variable name is `fos`
3️⃣ Invoke `fos.write(data)` method to store the data
4️⃣ Call `fos.close()` method to close the stream and release the system resources
5️⃣ Handle `IOException` and `FileNotFoundException`

**Writing data to a file:**

```java
import java.io.FileOutputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
public class FileOutputStreamDemo {

   public static void main(String[] args)
     throws FileNotFoundException, IOException {

      // create FileOutputStream class object
      FileOutputStream fos = new FileOutputStream("output.txt");

      // write data to the file
      int n1 = 97;
      fos.write(n1);
      fos.write(98);

      // to store string, convert it into byteArray
      String s = "Hello, World!";
      fos.write(s.getBytes());

      // display some message (optional)
      System.out.print("Data is saved");

      // close stream
      fos.close();
   }
}
```

📤 **Data in `output.txt` after execution:**

```
abHello, World!
```

In this program, if the `abc.txt` file is not already available then the constructor won't give an Exception rather it creates the `abc.txt` file itself. But if it is already available then it will override. If we run the same program once again then existing data will be overridden.

By default, `FileOutputStream` opens the connection in override mode. If we want to append the file then we must use 2 parameter constructor, and pass `true` as the second parameter value.

**Append mode:**

```java
FileOutputStream fos = new FileOutputStream("abc.txt", true);
// file connected in append mode
```

💡 **Tip:** We are saying that `FileOutputStream` is used to write data in binary form, but when we open the `output.txt` file then it displays characters or text data, how? While the execution of the program, the `write()` method converts given data to byte format and writes that data. Actually, data is stored in binary form, but when we use any text editor to open the file then the text editor converts them to corresponding ASCII character. For example, the ASCII value of `#` is 35, and `$` is 36.

**Example with ASCII values:**

```java
fos.write(35);
fos.write(36);
// Output:-
// #$
```

---

## 4. Limitation of Java FileOutputStream

❌️ **Limitation 1:** It writes data only in one byte format. It is not possible to write data in the format of primitive or objects.

We can write 97 as byte, short, int, long, char, float, double data type, which requires different bytes. But when we pass 97 in any data type format to the `write()` method then it will be written in only one byte. If the passed value exceeds the range of byte data type, then it will be typecast to byte and then written. For example byte 256 is the maximum range of byte, but if we try to write 353, (i.e. 256 + 97), then it will be typecast and 97 will be stored.

**Typecasting example:**

```java
// 256 + 48 = 304
fos.write(304);
// 256 + 65 = 321
fos.write(321);
// 256 + 97 = 353
fos.write(353);
```

📤 **Output:**

```
0Aa
```

❌️ **Limitation 2:** Using `FileOutputStream` we can't write `long`, `float`, `double`, `boolean`, `String` values directly.

```java
fos.write(50L);    // error
fos.write(9.9);    // error
fos.write(true);   // error
fos.write("Hello"); // error
```

> 📝 **Note:** To save data in primitive values we must save data using [DataOutputStream](057_DataOutputStream_in_Java.md), similarly to store data as Object we must use `ObjectOutputStream` class.
