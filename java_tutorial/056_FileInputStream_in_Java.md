# FileInputStream in Java

**FileInputStream in Java** | Reading binary data from a file using the `FileInputStream` class from `java.io`.

- [Overview](#overview)
- [Java FileInputStream Class Methods](#java-fileinputstream-class-methods)
- [Java FileInputStream Example](#java-fileinputstream-example)
- [Limitation of FileInputStream](#limitation-of-fileinputstream)

---

## 1. Overview

`FileInputStream` in Java is used to read binary data from the file. It is a sub class of [**InputStream**](054_InputStream_in_Java.md) class and available from Java 1.0 version onwards.

### Constructors

- `public FileInputStream(String name) throws FileNotFoundException`
- `public FileInputStream(File file) throws FileNotFoundException`
- `public FileInputStream(FileDescriptor fdObj)`

📝 **Note:** No param constructor is not given in the `FileInputStream` because it is a stream-based connection object where one end is a Java application. Therefore second end information must be passed as input.

To create a `FileInputStream` class object the file must exist with the passed argument name, else JVM throws `java.io.FileNotFoundException`. The `FileInputStream` class constructor throws `java.io.FileNotFoundException` in the given below situations:

- 🚨 If the file does not exist with the passed name
- 📂 The passed file name is a directory rather than a regular file
- 🔒 If the file doesn't have reading permissions

---

## 2. Java FileInputStream Class Methods

`FileInputStream` inherits all methods of [InputStream](054_InputStream_in_Java.md) class. All these methods throw `IOException`.

| Return Type 🔄 | Method 🛠️ | Description 📋 |
|----------------|-----------|----------------|
| `int` | `available()` | Returns number of available bytes |
| `int` | `read()` | Reads a byte of data from this input stream |
| `int` | `read(byte b[])` | Reads up to `b.length` bytes of data from this input stream into an array of bytes |
| `int` | `read(byte b[], int off, int len)` | Reads up to `len` bytes of data from this input stream into an array of bytes |
| `long` | `skip(long n)` | Skips over and discards `n` bytes of data from the input stream |
| `void` | `close()` | Closes this file input stream and releases any system resources associated with the stream |

---

## 3. Java FileInputStream Example

**Steps to read binary data from a file using FileInputStream:**

1️⃣ Import `java.io` package or related classes
2️⃣ Create a `FileInputStream` class object, let us say its name is `fis`
3️⃣ Invoke `fis.read()` method to read the data
4️⃣ Invoke `fis.close()` method to close the stream and release the system resources
5️⃣ Handle `IOException` and [FileNotFoundException](060_FileNotFoundException_in_Java.md)

🔑 **Properties of `read()` method of Java FileInputStream:**

- 📥 It reads only one byte at a time in the given file
- 🔢 It returns data in the terms of byte i.e. `int` value. To display a value in other types we must use typecasting.
- ❌️ If there is no byte available then it returns `-1`

To read multiple bytes we must use a loop until `read()` method doesn't return `-1`.

**Read loop pattern:**

```java
int data;
while((data = fis.read()) != -1) {
  ...
}
```

We have a `data.txt` file, and we will read from this file.

**Contents of `data.txt`:**

```
94584.4847
Hello, World!
```

**Reading data from file:**

```java
import java.io.FileInputStream;
import java.io.IOException;
import java.io.FileNotFoundException;
public class FileInputStreamDemo {

   public static void main(String[] args)
     throws FileNotFoundException, IOException {

      // create object
      FileInputStream fis = new FileInputStream("data.txt");

      // read data
      int data;
      while((data = fis.read()) != -1){
         System.out.print((char)data);
      }

      // close stream
      fis.close();
   }
}
```

📤 **Output:**

```
94584.4847
Hello, World!
```

💡 **Tip:** Instead of checking `data == -1`, we can also use the `available()` method.

---

## 4. Limitation of FileInputStream

It reads data only in a one-byte format. It is not possible to read data in the primitive or object format. To solve this problem we must use the [DataInputStream](058_DataInputStream_in_Java.md) class by wrapping the `FileInputStream` class.

```mermaid
graph LR
    A[File] --> B[FileInputStream]
    B --> C[DataInputStream]
    C --> D[Java Application]

    classDef purple fill:#A162F7,stroke:#A162F7,color:#fff
    classDef cyan fill:#00b4d8,stroke:#00b4d8,color:#fff
    classDef green fill:#28C76F,stroke:#28C76F,color:#fff
    classDef orange fill:#FF9F43,stroke:#FF9F43,color:#fff

    class A green
    class B orange
    class C cyan
    class D purple
```

> 📝 **Note:** `FileInputStream` reads one byte at a time. To read primitive types (int, long, float, double), wrap it with `DataInputStream`.
