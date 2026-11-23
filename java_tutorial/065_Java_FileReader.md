# Java FileReader

**Java FileReader** | Reading character/text data from files using the `java.io` package

- [Constructors](#constructors)
- [Methods](#methods)
- [Java FileReader Example](#java-filereader-example)
- [Example Using read(char[] ch)](#example-using-readchar-ch)
- [Limitation of FileReader Class](#limitation-of-filereader-class)

---

## 1. Constructors

The `FileReader` class in Java is used to read character or text data from the file. It is defined in the `java.io` package and it is a subclass of `InputStreamReader` class. The [InputStreamReader](063_InputStreamReader_in_Java.md) is the subclass of the [Reader class](062_Reader_Class_in_Java.md). Both the `InputStreamReader` and `Reader` classes are abstract classes. All these classes were introduced in Java 1.1 version.

Since `FileReader` is a connection based, where one end is a Java application and another end is a File. We must always pass the file information to the constructor. Therefore, it doesn't contain 0 parameter constructor.

It has a total of 5 constructors:

- 📄 `public FileReader(String fileName) throws FileNotFoundException`
- 📁 `public FileReader(File file) throws FileNotFoundException`
- 🔧 `public FileReader(FileDescriptor fd)`

**New constructors added in Java 11 version:**

- 🔤 `public FileReader(String fileName, Charset charset) throws IOException`
- 🔤 `public FileReader(File file, Charset charset) throws IOException`

> ⚠️ **Caution:** In all these constructors, we get `FileNotFoundException` if the named file does not exist, or it is a directory rather than a regular file, or for some other reason file cannot be opened for reading.

---

## 2. Methods

`FileReader` class doesn't contain any own methods. All methods of super class and interfaces are inherited to the `FileReader`. Some important methods are:

| Return Type 🏷️ | Method 🛠️ | Description 📋 |
|----------------|-----------|----------------|
| `int` | `read()` | It reads a single character at a time |
| `int` | `read(char[] ch)` | It reads characters, stores them to the passed char array, and returns the number of characters it read |
| `boolean` | `ready()` | It tells whether the stream is ready to be read |
| `void` | `close()` | It closes the stream and releases any system resources associated with it |

---

## 3. Java FileReader Example

The `read()` method reads a single character from the file and returns its [Unicode value](017_Unicode_Character_Set_in_Java.md). If the next character is not available i.e. at end of the file then it returns `-1`. Since `read()` method returns Unicode value represented as `int` value, so at the time of printing, we must use typecasting.

We have a file `data.txt` in the current working directory. The text in the file `data.txt` is:

```
Hello World!
Number = 20
Welcome to Java.
```

**Reading file character by character:**

```java
// Java program to read the data.txt
import java.io.FileReader;
import java.io.IOException;
public class FileReaderDemo {

   public static void main(String[] args)
                  throws IOException {

      // create FileReader object
      FileReader fr = new FileReader("data.txt");

      // define a int variable to
      // store returned value and call read()
      int i = fr.read();
      while(i != -1) {

         // convert int to char and display
         System.out.print((char)i);
         i = fr.read();
      }

      // close the stream
      fr.close();
   }
}
```

📤 **Output:**

```
Hello World!
Number = 20
Welcome to Java.
```

**Alternative read logic:**

```java
int i ;
while( (i= fr.read()) != -1) {
   System.out.print((char)i);
}
```

💡 **Tip:** Instead of checking `data == -1` better to use `ready()` method. The `ready()` method tells whether the stream is ready to be read or not. When it encounters the end of the file then it returns `false`.

**Using ready() method:**

```java
while(fr.ready()) {
   // convert int to char and display
   System.out.print((char)fr.read());
}
```

---

## 4. Example Using read(char[] ch)

Another alternate method `read(char[] ch)` is also given, which reads enough characters from the file, stores into the char array, and returns the number of characters copied from the file.

**Fixed array size behavior:**

```java
// Array smaller than file content
char[] ch = new char[20];
System.out.println( fr.read(ch) ); // 20

// Array larger than file content
char[] ch = new char[5000];
System.out.println( fr.read(ch) ); // 100
```

If we fix the size of the char array then we may not get the complete data from the file or have wastage of memory. If the file contains 100 characters, and we declare char array size as 20 then it will read only 20 characters from the file. Similarly, when we declare char array size as 5000 and the file contains only 100 characters, so it reads only 100 characters and remaining memory is wasted.

📝 **Note:** To solve this problem first find the length of characters available in the file, and we can find it using the [length() method of java.io.File class](048_File_Class_in_Java.md). But `length()` method returns a `long` value and while declaring the char array size we must declare size within the `int` range only, so use type-casting.

**Complete example with dynamic array size:**

```java
import java.io.File;
import java.io.FileReader;
import java.io.IOException;
public class FileReaderDemo {
   public static void main(String[] args)
                  throws IOException {

      // create file class object
      File file = new File("data.txt");

      // find length
      long fileLength = file.length();

      // create FileReader class object
      FileReader fr = new FileReader(file);

      // declare char array
      char[] ch = new char[(int)fileLength];

      // read character from file and store
      // into the char array
      int total = fr.read(ch);

      // display char array
      for(char c: ch) {
         System.out.print(c);
      }

      System.out.println("Length of the file = "
                                   + fileLength );
      System.out.println("Total character read = "
                                        + total );
      fr.close();
   }
}
```

📤 **Output:**

```
Hello World!
Number = 20
Welcome to Java.
Length of the file = 42
Total character read = 42
```

> 📝 **Note:** This technique will work only when number of characters available in the file doesn't exceed the `int` range, else use `read(int ch)` method.

---

## 5. Limitation of FileReader Class

1. ❌️ Using `FileReader` class in Java we can't read one line at a time from the file. We can read only one character at a time. It reduces the reading performance of the application. It gives very low performance when characters in the file are very large and file size exceeds the range of `int` data type.

2. ❌️ `FileReader` can be used to read data only from the file not from the console because it doesn't contain any constructor which can connect to another stream.

💡 **Tip:** To solve this problem and to read one line at a time we must use **`BufferedReader`** class, it is the most convenient way to read character/text data either from the file or console.
