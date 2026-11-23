# Catch All Exceptions in Java

**Catch All Exceptions in Java** | How to catch all exceptions with a single catch block using the `java.lang.Exception` parameter and why it's important to also use specific catch blocks.

- [Catching All Exceptions with Exception Parameter](#catching-all-exceptions-with-exception-parameter)
- [Best Practice: Multiple Catch Blocks with Backup](#best-practice-multiple-catch-blocks-with-backup)

---

In Java, we can catch all exceptions with a single catch block using the `java.lang.Exception` parameter. We should use this catch block only for stopping abnormal terminations irrespective of the exception thrown from its corresponding try statement.

> ⚠️ **Caution:** We can't handle `Error` type exceptions either by using catch block or throws keyword. Example: `OutOfMemoryError`, `StackOverflowError`, `VirtualMachineError`, `NoClassDefFoundError` and e.t.c. Because these types of exceptions are caused due to the lack of system resources. Errors are not recoverable. If `OutOfMemoryError` occurs, being a programmer we can't do anything & the program will be terminated abnormally. System admin or server admin is responsible to increase heap memory.

---

## 1. Catching All Exceptions with Exception Parameter

**Program to demonstrate how to catch all exceptions in Java:**

```java
class Division{
  public static void main(String[] args) {
    try{
      int a = Integer.parseInt(args[0]);
      int b = Integer.parseInt(args[1]);
      int c = a/b;
      System.out.println("Result: " + c);
    } catch(Exception e){
      System.out.println("Exception in the program");
    }
  }
}
```

**Test cases:**

| Test Case 🧪 | Command ⚙️ | Exception Raised ⚠️ | Output 📤 |
|-------------|-----------|-------------------|----------|
| No values passed | `java Division` | `ArrayIndexOutOfBoundsException` | Exception in the program |
| String passed | `java Division A` | `NumberFormatException` | Exception in the program |
| Only one value | `java Division 10` | `ArrayIndexOutOfBoundsException` | Exception in the program |
| Second value is string | `java Division 10 a` | `NumberFormatException` | Exception in the program |
| Second value is 0 | `java Division 10 0` | `ArithmeticException` | Exception in the program |
| Valid values | `java Division 10 2` | None | Result: 5 |

Based on the above all test-cases we can conclude that due to the `java.lang.Exception` parameter it can handle all exceptions, which was raised during the program execution. No need to write multiple catch blocks for different exceptions.

❌️ **Problem:** Whenever an exception is raised, the catch block will be executed and for different wrong values, we are not able to figure out what is the problem in the program. For example, our program gives the message "Exception in the program" when we pass the second number as a string (`NumberFormatException`), and it again gives the same output when the second number was zero (`ArithmeticException`). So we will not find the actual reason for the exception.

> 🔑 **Key Point:** It is always recommended to write a catch block with an `Exception` parameter even though we are writing multiple catch blocks.

We must always define `Exception` parameter catch block in the below two situations:

- 🛡️ As a backup catch of all catch blocks, or
- 🛡️ To stop abnormal terminations irrespective of the exception raised in the program

---

## 2. Best Practice: Multiple Catch Blocks with Backup

**Coding standards for handling exceptions:** We can use multiple catch blocks for handling known exceptions, but the last catch block should have a `java.lang.Exception` parameter which will be used to handle the unknown exception which may be raised in the program. The last catch block will be treated as a backup catch block, and program execution will be terminated normally.

**Sample program to catch all exceptions in Java:**

```java
class Division{
  public static void main(String[] args) {
    try{
      int a = Integer.parseInt(args[0]);
      int b = Integer.parseInt(args[1]);
      int c = a/b;
      System.out.println("Result: " + c);
    } catch(ArrayIndexOutOfBoundsException aiobe){
      System.out.println("Enter 2 integer values");
    } catch(NumberFormatException nfe){
      System.out.println("Passed value should be integer");
    } catch(ArithmeticException ae){
      System.out.println("2nd Number is 0, pass other value");
    } catch(Exception e){
      // for backup
      System.out.println("Exception in the program");
    }
  }
}
```

📤 **Output for the different input values:**

| Command ⚙️ | Output 📤 |
|-----------|----------|
| `java Division` | Enter 2 integer values |
| `java Division A` | Passed value should be integer |
| `java Division 10` | Enter 2 integer values |
| `java Division 10 A` | Passed value should be integer |
| `java Division 10 0` | 2nd Number is 0, pass other value |
| `java Division 10 2` | Result: 5 |

> 💡 **Tip:** Always use specific catch blocks for known exceptions and add `catch(Exception e)` as the last backup catch block. This gives meaningful error messages while still preventing abnormal termination.
