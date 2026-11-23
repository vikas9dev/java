# Try with Resources & Multi Catch block in Java

**Try with Resources & Multi Catch block in Java** | Java 1.7 version enhancement for [exception handling](176_Exception_Handling_in_Java.md) introducing two new concepts.

- [Try with Resources in Java](#try-with-resources-in-java)
- [Multi Catch Block](#multi-catch-block)
- [Important Points](#important-points)

---

## 1. Try with Resources in Java

Until the 1.6 version, whatever resources we open as part of try block compulsory we should close them in the finally block.

**Before Java 1.7 (manual resource closing):**

```java
import java.io.*;
public class Test {
   public static void main(String[] args) {
      BufferedReader br = null;
      try {
         br = new BufferedReader(new FileReader("input.txt"));
         // use br based on requirement
      } catch(IOException e) {
         // handling code
      } finally {
         try {
            if(br != null) br.close();
         } catch(IOException e) {
            // handling code
         }
      }
   }
}
```

Until 1.6 version, it is highly recommended to write finally block to close resources that are open as a part of the try block.

❌️ **Problems with this approach:**

- The programmer must close resources inside finally block which increases the complexity of programming.
- We must have to write finally block. It increases the burden on the programmer.
- If by mistake we forget to close the resource then the resource will be wasted.
- Readability becomes a bit low.

To overcome the above problem try with resources was introduced in the 1.7 version. The main advantage of try with resources is whatever resources we open as a part of the try block will be closed by itself by the JVM once control reaches the end of the try block either normally or abnormally. Hence we are not required to close them explicitly so that the complexity of programming will be reduced. We are not required to write finally block. Hence length of the code is reduced and readability will be improved.

✅ **Advantage of try with resources:** Whatever resource we open as part of the try block will be closed by JVM itself, we are not required to close them explicitly. Now, the complexity of the program will be reduced. Finally block is not required hence the length of the code is also reduced.

**Java 1.7+ (automatic resource closing):**

```java
import java.io.*;
public class Test {
   public static void main(String[] args) {
      try(BufferedReader br = new BufferedReader(
         new FileReader("input.txt"))) {
         // use br based on requirement
      } catch(IOException e) {
         // handling code
      }
   }
}
```

> 📝 **Note:** The `br` will be closed once control reaches the end of the try block either normally or abnormally and we are not responsible for closing them explicitly.

### Important Points on Try with Resources

**1. We can declare multiple resources but these resources should be separated with a semicolon symbol.**

**Multiple resources syntax:**

```java
try(R1; R2; R3; R4) {
}
```

**Multiple resources example:**

```java
import java.io.*;
public class Test {
   public static void main(String[] args) {
      try(FileWriter fw = new FileWriter("output.txt");
          FileReader fr = new FileReader("input.txt")
         ) {
         // use fw & fr based on requirement
      } catch(IOException e) {
         // handling code
      }
   }
}
```

**2. All resources should be AutoClosable resources.** A resource is said to be AutoClosable if & only if the corresponding class implements `java.lang.AutoClosable` interface. All IO-related resources, database-related resources, and network-related resources already implement the `AutoClosable` interface. Being a programmer we are not required to do anything just we should be aware of this point.

> 💡 **Tip:** `AutoClosable` marker interface came in 1.7 version to support try with resource & it contains only one abstract method `close()`: `public void close()`.

**3. All resource reference variables are implemented as final therefore within the try block we can't perform re-assignment otherwise we will get a compile-time error.**

**Re-assignment attempt (compile error):**

```java
import java.io.*;
public class Test {
   public static void main(String[] args) {
      try(FileWriter fw = new FileWriter("output.txt")) {
         fw = new FileWriter("file1.txt");
      } catch(IOException e) {
         // handling code
      }
   }
}
```

📤 **Compile-time error:**

```
Test.java:5: error: auto-closeable resource fw may not be assigned
fw = new FileWriter("file1.txt");
^
1 error
```

**4. Until the 1.6 version try should be associated with either catch/finally but from the 1.7 version we can take only try with resources without catch/finally.**

**Until the 1.6 version:**

```java
try {
} finally {
}
```

**Since the 1.7 version:**

```java
try(R) {
}
```

> 🔑 **Key Point:** The main advantage of try with resources is we are not required to write finally block explicitly because we are not required to close resources explicitly.

---

## 2. Multi Catch Block

Until the 1.6 version even though multiple different exceptions have the same handling code but for every exception type we have to write a separate catch block. It increases the length of code & reduces readability.

**Before Java 1.7 (separate catch blocks):**

```java
import java.io.*;
public class Test {
   public static void main(String[] args) {
      try {
         // code
      } catch(ArithmeticException ae) {
         ae.printStackTrace();
      } catch(IOException ioe) {
         ioe.printStackTrace();
      } catch(NullPointerException npe) {
         System.out.println(npe.getMessage());
      } catch(InterruptedException ie) {
         System.out.println(ie.getMessage());
      }
   }
}
```

To overcome this problem, the multi-catch block was introduced in the 1.7 version. According to this, we can write a single catch block that can handle multiple different types of exceptions.

**Java 1.7+ (multi-catch block):**

```java
import java.io.*;
public class Test {
   public static void main(String[] args) {
      try {
         // code
      } catch(ArithmeticException | IOException e) {
         e.printStackTrace();
      } catch(NullPointerException | InterruptedException e) {
         System.out.println(e.getMessage());
      }
   }
}
```

✅ The main advantage of this approach is: the length of the code will be reduced & readability will be improved.

**Multi-catch example:**

```java
public class Test {
   public static void main(String[] args) {
      try {
         System.out.println(9/0);
         String s = null;
         System.out.println(s.length());
      } catch(ArithmeticException | NullPointerException e) {
         e.printStackTrace();
      }
   }
}
```

> 📝 **Note:** In the above example, whatever exception raised is either `ArithmeticException` or `NullPointerException` the same catch block can handle them.

---

## 3. Important Points

**Related exceptions in multi-catch (compile error):**

```java
public class Test {
   public static void main(String[] args) {
      try {
         System.out.println(9/0);
      } catch(ArithmeticException | Exception e) {
         e.printStackTrace();
      }
   }
}
```

🚨 Compile-time error: `Alternatives in a multi-catch statement cannot be related by subclassing`

> ⚠️ **Caution:** In the multi-catch block, there should not be any relation between exception types (either child to parent, parent to child, or same type) otherwise we will get the compile-time error.

🔄 **Exception Propagation:** Inside a method if an exception is raised & if we are not handling that exception then the exception object will be propagated to the caller. Then caller method is responsible for handling exceptions. This process is called exception propagation.

🔁 **Re-throwing Exception:** We can use this approach to convert one exception type to another exception type.

```java
try {
    System.out.println(10/0);
} catch(ArithmeticException e) {
   throw new NullPointerException();
}
```
