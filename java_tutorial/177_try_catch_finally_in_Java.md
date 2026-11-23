# try-catch-finally in Java

**try-catch-finally in Java** | Handling exceptions using try-catch block and the role of the finally block. Also see: [Exception Handling in Java](176_Exception_Handling_in_Java.md)

- [Control flow in try-catch](#control-flow-in-try-catch)
- [Methods to Print Exception Information](#methods-to-print-exception-information)
- [try with multiple Catch blocks](#try-with-multiple-catch-blocks)
- [finally Block](#finally-block)

---

## 1. Without try-catch

**Without exception handling:**

```java
public class Test {
   public static void main(String[] args) {
      System.out.println("Statement1");
      System.out.println(9/0);
      System.out.println("Statement3");
   }
}
```

📤 **Output:**

```
Statement1
Exception in thread "main" java.lang.ArithmeticException: / by zero
at Test.main(Test.java:4)
```

❌️ It is an abnormal termination.

**With exception handling:**

```java
public class Test {
   public static void main(String[] args) {
      System.out.println("Statement1");
      try {
         System.out.println(9/0);
      } catch (ArithmeticException e) {
         System.out.println(9/1);
      }
      System.out.println("Statement3");
   }
}
```

📤 **Output:**

```
Statement1
9
Statement3
```

✅ It is normal termination.

It is highly recommended to handle exceptions. The code which may raise an exception is called risky code. We have to define the code inside the try-catch block & corresponding handling code we have to define in the catch block.

**Basic try-catch structure:**

```java
try {
   // risky code
} catch(Exception e) {
   // Handling code
}
```

---

## 2. Control flow in try-catch

- 🛡️ Within the try block if anywhere exception is raised then the rest of the try block won't be executed even though we handled that exception hence within the try block we have to take only risky code and the length of the try block should be as less as possible.
- ⚠️ In addition, to try block, there may be a chance of raising of an exception inside catch & finally blocks.
- 💥 If any statement which is not part of the try-catch block & raises an exception then it is always abnormal termination.

**Control flow structure:**

```java
try {
   statement1;
   statement2;
   statement3;
} catch(Exception e) {
   statement4;
}
statement5;
```

| Case 📋 | Scenario ⚙️ | Output 📤 | Termination 🏷️ |
|---------|------------|----------|----------------|
| **Case-1** | No exception | statement1, statement2, statement3, statement5 | ✅ Normal |
| **Case-2** | Exception at statement2, catch matched | statement1, statement4, statement5 | ✅ Normal |
| **Case-3** | Exception at statement2, catch not matched | statement1 | ❌️ Abnormal |
| **Case-4** | Exception at statement4 or statement5 | Depends | ❌️ Abnormal |

---

## 3. Methods to Print Exception Information

`Throwable` class defines the following methods to print exception information. Learn more: Different ways to get the exception message

| Method 🛠️ | Printable Format 📋 |
|-----------|-------------------|
| **`printStackTrace()`** | Name of exception; Description; Stack trace |
| **`toString()`** | Name of exception; Description |
| **`getMessage()`** | Description |

---

## 4. try with multiple Catch blocks

The way of handling an exception varies from exception to exception. Hence, for every exception type it is highly recommended to take a separate catch block i.e. try with multiple catch blocks is also possible & recommended to use.

**Worst programming practice:**

```java
// worst programming practice
try {
   // risky code
} catch(Exception e) {
   // Handling code
}
```

**Best programming practice:**

```java
// best programming practice
try {
   // risky code
} catch(ArithmeticException ae) {
   // perform alternative arithmetic operations
} catch(SQLException e) {
   // Use MySQL database instead of Oracle database
} catch(Exception e) {
   // Use local file instead of remote file
} catch(Exception e) {
   // default exception Handling code
}
```

> ⚠️ **Caution:** If try with multiple catch blocks present then the order of catch blocks is very important. We have to take the child first & then the parent otherwise we will get compile time error saying: `Exception Xxx has already been caught`.

**Wrong order (compile-time error):**

```java
try {
   // risky code
} catch(Exception e) {
   // exception Handling code
} catch(ArithmeticException ae) {
   // exception Handling code
}
```

🚨 Compile time error: `Exception java.lang.ArithmeticException has already been caught`.

**Correct order:**

```java
try {
   // risky code
} catch(ArithmeticException ae) {
   // exception Handling code
} catch(Exception e) {
   // exception Handling code
}
```

**Duplicate catch block (compile-time error):**

```java
try {
   // risky code
} catch(ArithmeticException ae) {
   // exception Handling code
} catch(ArithmeticException ae) {
   // exception Handling code
}
```

🚨 Compile time error: `Exception java.lang.ArithmeticException has already been caught`. We can't declare 2 catch blocks for the same exception otherwise we will get a compile-time error.

**Example-1 (valid):**

```java
// valid
try {
} catch (Exception e) {
}
```

**Example-2 (valid):**

```java
// valid
try {
} catch (X e) {
} catch (Y e) {
}
```

**Example-3 (invalid):**

```java
// invalid
try {
} catch (X e) {
} catch (X e) {
}
```

🚨 Both catch blocks handle the same exception. Compile time error: `exception X has already been caught`.

---

## 5. finally Block

**Difference between final, finally, and finalize?**

🔒 **final:** The `final` is a modifier applicable for classes, methods, and variables. If a class is declared as final then we can't extend that class i.e. we can't create a child class for that class i.e. inheritance is not possible for the final class. If a method is final then we can't override that method in the child class. If a variable is declared as final then we can't perform re-assignment for that variable.

🛡️ **finally:** The `finally` is a block always associated with try-catch to maintain cleanup code.

```java
try {
   // risky code
} catch(Exception e) {
   // handling code
} finally {
   // cleanup code
}
```

The specialty of the finally block is: It will be executed always irrespective of whether the exception is raised or not raised or whether handled or not handled.

🗑️ **finalize():** The `finalize()` is a method always invoked by the garbage collector just before destroying an object to perform cleanup activities. Once the `finalize()` method completes immediately garbage collector destroys that object.

The finally block is responsible for performing cleanup activity related to the try block i.e. whatever resources we opened as a part of the try block will be closed inside the finally block. Whereas the `finalize()` method is responsible for performing cleanup activities related to the object i.e. whatever resources associated with the object will be deallocated before destroying an object by using `finalize()` method.

### Various Possible Combinations of try-catch-finally

1. In try-catch-finally block order is important.
2. Whenever we are writing try then compulsory we have to write either catch or finally otherwise we will get compile time error i.e. try without catch or finally is invalid.
3. Whenever we are writing a catch block compulsory try block must be required i.e. catch without a try is invalid.
4. Whenever we are writing finally block compulsory we should write try block i.e. finally without try is invalid.
5. Inside try-catch & finally block, we can declare try-catch & finally blocks i.e. nesting of try-catch finally is allowed.
6. For try-catch & finally blocks curly brackets are mandatory.

**Example-4 (valid):**

```java
// valid
try {
} catch (X e) {
} finally {
}
```

**Example-5 (valid):** If we don't want to handle any exception but before abnormal termination cleanup activity will be performed.

```java
// valid
try {
} finally {
}
```

**Example-6 (valid):**

```java
// valid
try {
} catch (X e) {
}
try {
} catch (Y e) {
}
```

**Example-7 (valid):**

```java
// valid
try {
} catch (X e) {
}
try {
} finally {
}
```

**Example-8 (invalid):** Compile-time error: try without catch (or) finally.

```java
// invalid
try {
}
```

**Example-9 (invalid):** Compile-time error: finally without try

```java
// invalid
finally {
}
```

**Example-10 (invalid):** Compile-time error: catch without try

```java
// invalid
catch(X e) {
}
```

**Example-11 (invalid):** We will get 2 compile time errors. Compile-time error: try without catch or finally; Compile-time error: catch without try.

```java
// invalid
try {
}
System.out.println("Hello");
catch(X e) {
}
```

**Example-12 (invalid):** Compile-time error: catch without try.

```java
// invalid
try {
} finally {
}
catch(X e) {
}
```

The above code snippet will work as below.

```java
try {
} finally {
}
// separate part
catch(X e) {
}
```

**Example-13 (invalid):** The second catch block becomes alone. Compile-time error: catch without try.

```java
// invalid
try {
} catch(X e) {
}
System.out.println("Hello");
catch(Y e) {
}
```

**Example-14 (invalid):** Compile-time error: finally without try

```java
// invalid
try {
} catch(X e) {
}
System.out.println("Hello");
finally {
}
```

**Example-15 (valid):**

```java
// valid
try {
   try {
   } catch (X e) {
   }
} catch(X e) {
}
```

**Example-16 (invalid):** In inner catch compile time error: try without catch or finally

```java
// invalid
try {
   try {
   }
} catch(X e) {
}
```

**Example-17 (valid):**

```java
// valid
try {
   try {
   } finally {
   }
} catch(X e) {
}
```

**Example-18 (valid):**

```java
// valid
try {
} catch(X e) {
   try {
   } finally {
   }
}
```

**Example-19 (invalid):** Compile-time error: finally without try

```java
// invalid
try {
} catch(X e) {
   finally {
   }
}
```

**Example-20 (valid):**

```java
// valid
try {
} catch(X e) {
} finally {
   try {
   } catch(X e) {
   }
}
```

**Example-21 (invalid):** Compile-time error: finally without try

```java
// invalid
try {
} catch(X e) {
} finally {
   finally {
   }
}
```

**Example-22 (invalid):** There can be only one finally block for 1 try block. Compile-time error: finally without try

```java
// invalid
try {
} catch(X e) {
} finally {
} finally {
}
```

**Example-23 (invalid):** For try-catch-finally block, `{ }` is mandatory.

```java
// invalid
try
   System.out.println("try");
catch(X e) {
   System.out.println("catch");
} finally {
}
```

**Example-24 (invalid):**

```java
// invalid
try {
}
catch(X e)
   System.out.println("catch");
finally {
}
```

**Example-25 (invalid):**

```java
// invalid
try {
}
catch(X e) {
}
finally {
   System.out.println("finally");
}
```
