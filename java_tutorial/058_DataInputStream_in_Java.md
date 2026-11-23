# DataInputStream in Java

**DataInputStream in Java** | Reading data in primitive type size bytes from files using the `DataInputStream` class.

- [Overview](#overview)
- [Methods of DataInputStream Class](#methods-of-datainputstream-class)
- [Java Program Example Using DataInputStream](#java-program-example-using-datainputstream)
- [Limitations of Java DataInputStream Class](#limitations-of-java-datainputstream-class)

---

## 1. Overview

The `DataInputStream` class in Java is used to read data in primitive type size bytes from the underlying InputStreams. It has special methods to read primitive type size bytes.

It is a subclass of `FilterInputStream` and implements the `DataInput` interface. `FilterInputStream` is the subclass of [**InputStream**](054_InputStream_in_Java.md). These all classes are available from Java 1.0 version onwards. `InputStream` class is used to read data in binary form. `DataInput` interface has several methods to read bytes from the binary input stream and convert them into the corresponding Java primitive type. Other implemented interfaces are: `Closeable`, `AutoCloseable`.

```java
public class DataInputStream
extends FilterInputStream
implements DataInput
```

### Constructors

The [**FileInputStream**](056_FileInputStream_in_Java.md) is the basic source for all input stream classes which can directly make a connection between Java application and file. Similar to the other input stream classes, the `DataInputStream` class also depends on the `FileInputStream` class to make a connection between the Java application and file. `DataInputStream` class has only one constructor which needs `InputStream` as a parameter.

**Constructor:**

```java
public DataInputStream(InputStream in) {
   super(in);
}
```

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

---

## 2. Methods of DataInputStream Class

The `readXxx()` methods are given to read the different primitive type values. Actually, the `readXxx()` method reads the number of bytes from a file based on the data type. For example, if we call the `readInt()` method then it reads 4 bytes available in the file. If 4 bytes are not available then it throws **EOFException**.

### Read Methods for Primitive Types

| Return Type 🔄 | Method 🛠️ |
|----------------|-----------|
| `byte` | `readByte()` |
| `int` | `readUnsignedByte()` |
| `short` | `readShort()` |
| `int` | `readUnsignedShort()` |
| `int` | `readInt()` |
| `long` | `readLong()` |
| `float` | `readFloat()` |
| `double` | `readDouble()` |
| `char` | `readChar()` |
| `boolean` | `readBoolean()` |
| `String` | `readUTF()` |

📝 **Note:** To read String value `readLine()` is also there but it is **deprecated** because it doesn't properly convert bytes to characters.

⚠️ **Caution:** All methods above throw `IOException` if the stream has been closed or another I/O error occurs. They also throw **EOFException** if the input stream reaches the end before reading the required bytes. The `readUTF()` also throws **UTFDataFormatException** if the bytes do not represent a valid modified UTF-8 encoding of a string.

### Other Methods

| Modifier and Type 🔄 | Method 🛠️ | Description 📋 |
|----------------------|-----------|----------------|
| `int` | `read(byte[] b)` | Reads some number of bytes and stores them into buffer array `b` |
| `int` | `read(byte[] b, int off, int len)` | Reads up to `len` bytes of data and stores them into buffer array `b` |
| `void` | `readFully(byte[] b)` | Similar to `read(byte[] b)` |
| `void` | `readFully(byte[] b, int off, int len)` | Similar to `read(byte[] b, int off, int len)` |
| `static String` | `readUTF(DataInput in)` | Reads Unicode character string encoded in modified UTF-8 format and returns them as String |
| `int` | `skipBytes(int n)` | Skips `n` bytes of data |

The `read(byte[] b)` and `read(byte[] b, int off, int len)` methods read some/len number of bytes data, store them into buffer array `b`, and then return the number of bytes available in buffer array `b`. The `readFully(byte[] b)` and `readFully(byte[] b, int off, int len)` do the same but don't return anything.

These methods throw `IOException` if the stream has been closed or another I/O error occurs. The `readUTF(DataInput in)` also throws `UTFDataFormatException` if the bytes do not represent a valid modified UTF-8 encoding of a string.

---

## 3. Java Program Example Using DataInputStream

🔑 **Important Points:**

- 1️⃣ To read data as primitive types using `readXxx()` methods, first of all, data must be written to the file as primitive types using `writeXxx()` methods of [**DataOutputStream class**](057_DataOutputStream_in_Java.md).
- 2️⃣ `readXxx()` methods must be called in the same order in which the `writeXxx()` methods are called otherwise wrong value will be returned or **EOFException** is raised.

In this program, we are using `output.txt` which is written by the `writeXxx()` method of `DataOutputStream` class. We will call `readXxx()` in the same order as we used `writeXxx()`.

> ⚠️ **Warning:** Whenever you are typing characters into the file, they won't be treated as bytes. They are characters, not bytes. See the [program given in DataOutputStream class](057_DataOutputStream_in_Java.md) to generate the `output.txt`.

**Content in `output.txt` (hex):**

```
0000 0061 0000 0000 0000 0064 42c7 cccd
4057 e000 0000 0000 0061 0100 0f6b 6e6f
7770 726f 6772 616d 2e63 6f6d 4865 6c6c
6f2c 2077 6f72 6c64 2100 4a00 6100 7600
6100 2000 7000 7200 6f00 6700 7200 6100
6d61
```

**Reading primitive types from a file:**

```java
// DataInputStream class demonstration
import java.io.FileInputStream;
import java.io.DataInputStream;
import java.io.IOException;
import java.io.FileNotFoundException;

public class DISTest {
   public static void main(String[] args)
           throws IOException, FileNotFoundException {

      // create FileInputStream object
      FileInputStream fis =
           new FileInputStream("output.txt");

      // create DataInputStream object
      DataInputStream dis =  new DataInputStream(fis);

      // read int data
      int n1 = dis.readInt();
      System.out.println(n1);

      // read long
      System.out.println(dis.readLong());

      // read float
      System.out.println(dis.readFloat());

      // read double
      System.out.println(dis.readDouble());

      // read character
      System.out.println(dis.readChar());

      // read boolean
      System.out.println(dis.readBoolean());

      // read String
      System.out.println(dis.readUTF());

      // read last values
      byte[] b = new byte[100];
      System.out.println(dis.read(b));
      for(int i=0; i<b.length; i++) {
         System.out.print((char)b[i]);
      }

      // close stream
      dis.close();
   }
}
```

📤 **Output:**

```
97
100
99.9
95.5
a
true
knowprogram.com
38
Hello, world!Java program
```

---

## 4. Limitations of Java DataInputStream Class

There are many limitations of the `DataInputStream` class. Generally, `DataInputStream` class is used with the combination of `DataOutputStream` class. We have already discussed limitations in the `DataOutputStream` class post.

- 🚨 If the data is written as int type i.e. only 4 bytes then we can't read it using `readLong()` which needs 8 bytes, because 8 bytes are not available. Hence it will throw `EOFException`. EOF => End-Of-File.
- ⚠️ While working with `DataInputStream` and `DataOutputStream` classes, whatever `writeXxx()` method called in the same order `readXxx()` method must be called. If the order is not the same then we will get either the wrong result or `EOFException`.
- 🔗 We have to first write the data using `DataOutputStream` then only we can read them using `DataInputStream` class.
- ❌️ Without writing primitive data in binary format using `DataOutputStream` class, we can't call `readXxx()` methods of `DataInputStream` class. Both classes must be used in combination.

💡 **Tip:** If we creating a file and saving data "0061" in the file, now if we try to read these values using `readXxx()` method then it will give some wrong result because whenever we are typing characters to the file, they won't be treated as bytes. They are characters, not bytes.

Let us assume, we have a file and it contains some bytes generated by `DataOutputStream`. It is "4058 4000 0000 0000" which is written by `writeDouble(97)` method. Now, this data will be read by `readXxx()` methods as:

**Reading the same data with different methods:**

```java
readByte();    // 64
readShort();   // 16472
readInt();     // 1079525376
readLong();    // 4636526185122103296
readFloat();   // 3.3789062
readDouble();  // 97.0
readBoolean(); // true
readUTF();     // EOFException
```

> 🔑 **Key Point:** Always call `readXxx()` methods in the same order as the corresponding `writeXxx()` methods were called to avoid wrong results or `EOFException`.
