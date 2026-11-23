# InputStreamReader in Java

**InputStreamReader in Java** | A bridge from byte streams to character streams in the `java.io` package

- [Java InputStreamReader Class Methods](#java-inputstreamreader-class-methods)
- [Connecting BufferedReader to Keyboard](#connecting-bufferedreader-to-keyboard)

---

## 1. Java InputStreamReader Class Methods

The `InputStreamReader` class in Java is defined in the `java.io` package. It is extended from [Reader class](062_Reader_Class_in_Java.md) and introduced in Java 1.1 version.

**Class declaration:**

```java
public class InputStreamReader
extends Reader
```

🔄 **The `InputStreamReader` is a bridge from byte streams to character streams.** It reads bytes and decodes them into characters using a specified charset.

It has multiple constructors to take `InputStream` type object:

- 🏗️ `public InputStreamReader(InputStream in)` — Creates an `InputStreamReader` that uses the default charset.
- 🔤 `public InputStreamReader(InputStream in, String charsetName) throws UnsupportedEncodingException` — Creates an `InputStreamReader` that uses the named charset. It throws `UnsupportedEncodingException` when the named charset is not supported.
- 🔧 `public InputStreamReader(InputStream in, Charset cs)` — Creates an `InputStreamReader` that uses the given charset.
- ⚙️ `public InputStreamReader(InputStream in, CharsetDecoder dec)` — Creates an `InputStreamReader` that uses the given charset decoder.

📝 **Note:** Whereas an `OutputStreamWriter` is a bridge from character streams to byte streams. Characters written to it are encoded into bytes using a specified charset. It has several constructors to take `OutputStream` type object.

**Methods:**

| Modifier and Type 🏷️ | Method 🛠️ | Description 📋 |
|----------------------|-----------|----------------|
| `public int` | `read()` | It reads a single character |
| `public int` | `read(char cbuf[], int offset, int length)` | It reads characters into a portion of an array |
| `public boolean` | `ready()` | It tells whether this stream is ready to be read |
| `public void` | `close()` | It closes the connection |
| `String` | `getEncoding()` | It returns the name of the character encoding being used by this stream |

💡 **Tip:** An `InputStreamReader` is ready if its input buffer is not empty, or if bytes are available to be read from the underlying byte stream.

🔗 **Subclasses:** It has only one subclass [FileReader](065_Java_FileReader.md) which is used to read data from the file.

---

## 2. Connecting BufferedReader to Keyboard

To connect [BufferedReader](067_BufferedReader_in_Java.md) object with Keyboard:

1. Pass `System.in` as an argument to `InputStreamReader` object creation
2. Pass `InputStreamReader` object as an argument to `BufferedReader` object creation

**Two-line syntax:**

```java
// create BufferedReader and InputStreamReader object
InputStreamReader isr = new InputStreamReader(System.in);
BufferedReader br = new BufferedReader(isr);
```

**Single-line syntax:**

```java
// it can be written in one line as
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
```

```mermaid
graph LR
    KB[Keyboard] --> IS[System.in]
    IS --> ISR[InputStreamReader]
    ISR --> BR[BufferedReader]
    BR --> APP[Java Application]

    classDef purple fill:#A162F7,stroke:#A162F7,color:#fff
    classDef cyan fill:#00b4d8,stroke:#00b4d8,color:#fff
    classDef green fill:#28C76F,stroke:#28C76F,color:#fff
    classDef orange fill:#FF9F43,stroke:#FF9F43,color:#fff

    class KB orange
    class IS orange
    class ISR cyan
    class BR purple
    class APP green
```
