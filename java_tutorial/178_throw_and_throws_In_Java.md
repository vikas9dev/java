# throw and throws In Java

**throw and throws In Java** | In the [introduction of Exception Handling](176_Exception_Handling_in_Java.md), we have seen various concepts including exception hierarchy, Checked vs Unchecked Exception, and Fully Checked vs Partially Checked Exception. Later we discussed how to handle the exception using the [try-catch-finally block](177_try_catch_finally_in_Java.md) with different test cases.

- [throw keyword in Java](#throw-keyword-in-java)
- [throws Keyword In Java](#throws-keyword-in-java)
- [throws keyword Summary](#throws-keyword-summary)
- [Summary on Exception Handling Keyword](#summary-on-exception-handling-keyword)
- [Various Possible Compile time-errors in Exception Handling](#various-possible-compile-time-errors-in-exception-handling)
- [Customized / User-defined Exception](#customized--user-defined-exception)

---

## 1. throw keyword in Java

**Example 1 - Exception raised by JVM:**

```java
public class Test {
   public static void main(String[] args) {
      System.out.println(10/0);
   }
}
```

📤 **Output:**

```
Exception in thread "main" java.lang.ArithmeticException: / by zero
at Test.main(Test.java:3)
```

**Example 2 - Exception raised manually using throw:**

```java
public class Test {
   public static void main(String[] args) {
      throw new ArithmeticException("divided by zero");
   }
}
```

📤 **Output:**

```
Exception in thread "main" java.lang.ArithmeticException: divided by zero
at Test.main(Test.java:3)
```

- 🚀 `throw` — Hand over our created exception object to the JVM manually.
- ⚙️ `new ArithmeticException("divided by zero")` — Creation of `ArithmeticException` object explicitly.

Sometimes we can create exception objects explicitly & we can hand them over to the JVM manually. For that, we have to use the `throw` keyword. Hence, the **main objective of the throw keyword: to hand over our created exception object to the JVM manually.**

The results of the above 2 programs are the same:

- 🤖 In the 1st program: In this case, the main method is responsible for creating an exception object and handing it over to the JVM.
- 👨‍💻 In 2nd program: In this case, the programmer creates an exception object explicitly & hands it over to the JVM manually.

The `throw` keyword is best used for user-defined exceptions or customized exceptions but not for pre-defined exceptions.

**Custom exception usage:**

```java
withdraw(double amount) {
   if (amount > balance) {
      throw new InsufficientFundsException();
   }
}
```

### Case-1: Exception Object Must Be Initialized

Before throwing the exception object, it must be initialized.

**Initialized exception (valid):**

```java
public class Test {
   static ArithmeticException e = new ArithmeticException();
   public static void main(String[] args) {
      throw e;
   }
}
```

📤 **Output:**

```
Exception in thread "main" java.lang.ArithmeticException
at Test.(Test.java:2)
```

**Uninitialized exception (NullPointerException):**

```java
public class Test {
   static ArithmeticException e;
   public static void main(String[] args) {
      throw e;
   }
}
```

📤 **Output:**

```
Exception in thread "main" java.lang.NullPointerException: Cannot throw an exception because "Test.e" is null at Test.main(Test.java:4)
```

> 📝 **Note:** We are trying to throw variable "a" which is not initialized in the program. By default static reference variables contain `null`.

### Case-2: Unreachable Statement After throw

After the throw statement, we are not allowed to write any statement directly otherwise we will get compile time error: `unreachable statement`.

**Valid (exception by JVM):**

```java
// valid
public class Test {
   public static void main(String[] args) {
      System.out.println(10/0);
      System.out.println("Hello");
   }
}
```

📤 **Output:**

```
Exception in thread "main" java.lang.ArithmeticException: / by zero
at Test.main(Test.java:3)
```

**Compile-time error (unreachable statement):**

```java
// compile time error
public class Test {
   public static void main(String[] args) {
      throw new ArithmeticException("/ by zero");
      System.out.println("Hello");
   }
}
```

📤 **Compile-time error:**

```
Test.java:4: error: unreachable statement
System.out.println("Hello");
^
1 error
```

🧠 **In Simple Words:** In the 1st program, just by seeing the syntax compiler doesn't know `System.out.println(10/0)` will throw any error. At runtime due to 10/0, we will get `ArithmeticException`. But in the 2nd program, just by seeing the syntax `throw new ...` the compiler knows that this line will throw an exception & the remaining line will never execute. Hence we will get the compile time error: `unreachable statement.`

### Case-3: throw Only for Throwable Types

We can use the `throw` keyword only for `Throwable` types. If we are trying to use it for a normal Java object then we will get compile time error: `incompatible types`.

**Invalid (normal Java class):**

```java
public class Test {
   public static void main(String[] args) {
      throw new Test();
   }
}
```

📤 **Compile-time error:**

```
Test.java:3: error: incompatible types: Test cannot be converted to Throwable
throw new Test();
^
1 error
```

**Valid (extends RuntimeException):**

```java
public class Test extends RuntimeException {
   public static void main(String[] args) {
      throw new Test();
   }
}
```

📤 **Output:**

```
Exception in thread "main" Test
at Test.main(Test.java:3)
```

---

## 2. throws Keyword In Java

**Example - checked exception without handling:**

```java
import java.io.*;
public class Test {
   public static void main(String[] args) {
      PrintWriter pw = new PrintWriter("abc.txt");
      pw.println("Hello");
   }
}
```

📤 **Compile-time error:**

```
Test.java:4: error: unreported exception FileNotFoundException; must be caught or declared to be thrown
PrintWriter pw = new PrintWriter("abc.txt");
^
1 error
```

In our program, if there is a possibility of **raising a checked exception** then we must handle that checked exception otherwise we will get compile time error: `unreported exception Xxx; must be caught or declared to be thrown`.

**Another example:**

```java
public class Test {
   public static void main(String[] args) {
      Thread.sleep(1000); // 1 sec
   }
}
```

📤 **Compile-time error:**

```
Test.java:3: error: unreported exception InterruptedException; must be caught or declared to be thrown
Thread.sleep(1000); // 1 sec
^
1 error
```

We can handle this compile time error:

1. By using try-catch
2. By using the `throws` keyword

**Handling exceptions using try-catch:**

```java
public class Test {
   public static void main(String[] args) {
      try {
         Thread.sleep(1000); // 1 sec
      } catch (InterruptedException e) {}
   }
}
```

> 📝 **Note:** Compiler doesn't worry what code we have written in the catch block. It just checks whether the `Thread.sleep(1000)` is inside the try block or not.

**Handling Exception using the throws keyword:**

We can use the `throws` keyword to delegate the responsibility of exception handling to the caller (it may be another method or JVM) then the caller method is responsible for handling that exception.

```java
public class Test {
   public static void main(String[] args)
       throws InterruptedException {
      Thread.sleep(1000); // 1 sec
   }
}
```

🔑 **Conclusion on throws:**

- 🏷️ `throws` keyword is required only for checked exceptions & the use of the `throws` keyword on unchecked exceptions has no impact.
- ⚙️ The `throws` keyword is required only to convince the compiler & the use of the `throws` keyword doesn't prevent abnormal termination of the program.

**throws propagation example:**

```java
public class Test {
   public static void main(String[] args) throws InterruptedException {
      m1();
   }
   public static void m1() throws InterruptedException {
      m2();
   }
   public static void m2() throws InterruptedException {
      Thread.sleep(1000); // 1 sec
      System.out.println("m2");
   }
}
```

> ⚠️ **Caution:** In the above program if we remove at least one `throws` statement then the code won't compile. If there is a chance of raising a checked exception in the `m1()` method then the `m1()` method also must handle it.

**Missing throws in m1() - compile error:**

```java
public class Test {
   public static void main(String[] args) throws InterruptedException {
      m1();
   }
   public static void m1() {
      m2();
   }
   public static void m2() throws InterruptedException {
      Thread.sleep(1000); // 1 sec
      System.out.println("m2");
   }
}
```

**Missing throws in m1() at place2 - compile error:**

```java
public class Test {
   public static void main(String[] args) throws InterruptedException { // place1
      m1();
   }
   public static void m1() {  // place2
      Thread.sleep(1000);
      System.out.println("m1");
   }
}

// Compile-time error at place-2.
```

---

## 3. throws keyword Summary

- 🔄 We can use it to delegate the responsibility of exception handling to the caller (It may be method or JVM).
- ✅ It is required only for checked exceptions and usage of the `throws` keyword for unchecked exceptions has no impact.
- ⚙️ It requires only to convince the compiler and usage of `throws` doesn't prevent abnormal termination of the program.

💡 **Tip:** It is recommended to use the try-catch block over the `throws` keyword.

### Case 1: throws for Methods and Constructors Only

We can use the `throws` keyword for methods & constructors but not for classes.

```java
public class Test {
   Test() throws Exception {} // valid
   public static void main(String[] args) throws Exception {} // valid
}
```

```java
public class Test throws Exception {} // invalid
```

### Case 2: throws Only for Throwable Types

We can use the `throws` keyword only for throwable types. If we are trying to use it for normal Java classes then we will get compile time error: `incompatible types`.

```java
public class Test {
   public static void main(String[] args) throws Test {}
}
```

📤 **Compile-time error:**

```
Test.java:2: error: incompatible types: Test cannot be converted to Throwable
public static void main(String[] args) throws Test {}
^
1 error
```

```java
// valid
public class Test extends RuntimeException {
   public static void main(String[] args) throws Test {}
}
```

### Case 3: Handling Checked Exceptions

If the program throws unchecked exceptions either manually or by the JVM, we must handle unchecked exceptions.

**Checked exception without handling:**

```java
public class Test {
   public static void main(String[] args) {
      throw new Exception();// checked exception
   }
}
```

📤 **Compile-time error:**

```
Test.java:3: error: unreported exception Exception; must be caught or declared to be thrown
throw new Exception();// checked exception
^
1 error
```

**Unchecked exception (no compile error):**

```java
public class Test {
   public static void main(String[] args) {
      throw new Error();// unchecked exception
   }
}
```

### Case 4: Fully Checked Exception Rule

Within the try block if there is no chance of raising an exception then we can't write the catch block for that exception otherwise we will get compile time error: `Exception Xxx is never thrown in the body of the corresponding try statement`. **But this rule is only applicable to fully checked exceptions.**

**Unchecked exception (valid):**

```java
public class Test {
   public static void main(String[] args) {
      try {
         System.out.println("Hello");
      } catch(ArithmeticException e) {
         // unchecked exception
      }
   }
}
```

📤 **Output:** `Hello`

**Partially checked exception (valid):**

```java
public class Test {
   public static void main(String[] args) {
      try {
         System.out.println("Hello");
      } catch(Exception e) {
         // partially checked exception
      }
   }
}
```

📤 **Output:** `Hello`

**Fully checked exception (compile error):**

```java
import java.io.*;
public class Test {
   public static void main(String[] args) {
      try {
         System.out.println("Hello");
      } catch(IOException e) {
         // fully checked exception
      }
   }
}
```

📤 **Compile-time error:**

```
Test.java:6: error: exception IOException is never thrown in body of corresponding try statement
} catch(IOException e) {
^
1 error
```

**Another fully checked exception (compile error):**

```java
public class Test {
   public static void main(String[] args) {
      try {
         System.out.println("Hello");
      } catch(InterruptedException e) {
         // fully checked exception
      }
   }
}
```

📤 **Compile-time error:**

```
Test.java:5: error: exception InterruptedException is never thrown in body of corresponding try statement
} catch(InterruptedException e) {
^
1 error
```

**Unchecked Error (valid):**

```java
public class Test {
   public static void main(String[] args) {
      try {
         System.out.println("Hello");
      } catch(Error e) {
         // unchecked exception
      }
   }
}
```

📤 **Output:** `Hello`

---

## 4. Summary on Exception Handling Keyword

| Keyword 🏷️ | Purpose 📋 |
|------------|-----------|
| **`try`** | To maintain risky code |
| **`catch`** | To maintain exception handling code |
| **`finally`** | To maintain cleanup code |
| **`throw`** | To handover our created exception object to the JVM manually |
| **`throws`** | To delegate the responsibility of exception handling to the caller |

---

## 5. Various Possible Compile time-errors in Exception Handling

1. 🚨 **Unreported exception Xxx; must be caught or declared to be thrown** — When there is a statement that may raise a checked exception & we are not handling it.
2. 🛡️ **Exception Xxx has already been caught** — try with multiple catch blocks; the order of catch blocks is important.
3. ⚠️ **Exception Xxx is never thrown in the body of the corresponding try statement** — When we are handling a fully checked exception but there is no chance to raise it in the try block.
4. 🚫 **Unreachable statement** — There is some code after the `throw ...` statement.
5. 💥 **Incompatible types;** found: Test; required: java.lang.Throwable
6. ❌️ **try without catch or finally**
7. ❌️ **catch without try**
8. ❌️ **finally without try**

---

## 6. Customized / User-defined Exception

- 🎯 `throw` keyword is best suitable for user-defined or customized exceptions but not for pre-defined exceptions.
- ✅ It is highly recommended to define customized exception as unchecked i.e. we should extend the custom exception class from `RuntimeException` but not from the `Exception` class.
