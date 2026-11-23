# Develop User-defined Custom Exception in Java

**Develop User-defined Custom Exception in Java** | How to create custom exceptions, the best procedure, and which class to extend from.

- [Procedure to Develop Custom Exception Class](#procedure-to-develop-custom-exception-class)
- [Java Custom Exception Example](#java-custom-exception-example)
- [A Custom Exception should be Derived From Which Class & Why?](#a-custom-exception-should-be-derived-from-which-class--why)
- [Developing User-Defined Unchecked Exception](#developing-user-defined-unchecked-exception)

---

**The new class developed by a programmer deriving from either `Throwable` or any one of its subclass is called custom exception or user-defined exception.**

Most of the cases custom exception classes are derived from the **`Exception` class** because they must be handled by the programmer when they are thrown.

All exception classes defined by SUN are based on the Java language and API requirements but not for the development of our projects. So, according to the business requirements programmer must develop their own exception class with suitable and meaningful names relevant to the project context.

---

## 1. Procedure to Develop Custom Exception Class

User-defined or custom exception development is a two steps process:

1️⃣ **Define a packaged public class deriving from `java.lang.Exception` class.**

2️⃣ **Define public no-arg and String parameter constructors with `super()` call.**
   - No-arg constructor for creating an exception object without the message.
   - Parameterized constructor for creating an exception object with the message.

**Custom exception template:**

```java
public class ExampleException extends Exception {

   // No-arg constructor with super() call
   public ExampleException (){
     super();
   }

   // String-arg constructor with super() call
   public ExampleException (String msg) {
     super(msg);
   }

}
```

> 💡 **Tip:** We can create custom exceptions just by defining a class that is inherited from the `Exception` class but it is **recommended** to develop a no-arg and String-arg constructor with `super()` call.

---

## 2. Java Custom Exception Example

**Develop a Java program to add only positive numbers, if the user passes negative numbers then throw your own checked exception `NegativeNumberException`.**

In this Java program, we will create a custom exception `NegativeNumberException`. Later, we will develop another class `Addition`. In the `Addition` class, the `add(int a, int b)` method throws `NegativeNumberException` if any of the passing numbers is negative otherwise it returns the sum of numbers. The `add()` method will be called and the exception will be caught by try/catch block.

1️⃣ **NegativeNumberException.java:**

```java
// NegativeNumberException.java
public class NegativeNumberException extends Exception {

  // No-arg constructor with super() call
  public NegativeNumberException(){
    super();
  }

  // String-arg constructor with super() call
  public NegativeNumberException(String msg){
    super(msg);
  }

}
```

2️⃣ **Addition.java:**

```java
// Addition.java
public class Addition {

  public static int add(int a, int b)
           throws NegativeNumberException {

    if(a<0 || b<0)
    throw new NegativeNumberException("Pass only +ve number");

    return a+b;

  }
}
```

> 📝 **Note:** If any passed number is negative then it will throw `NegativeNumberException`. No need to write else block, because when if-condition fails then it returns the sum of the passing numbers.

3️⃣ **Calculator.java:**

```java
 // Calculator.java
 import java.util.Scanner;

 public class Calculator {

   public static void main(String[] args) {

     // declare variables
     int a = 0, b = 0;

     // Create Scanner class object
     Scanner scan = new Scanner(System.in);

     // read inputs
     System.out.print("Enter first number: ");
     a = scan.nextInt();
     System.out.print("Enter second number: ");
     b = scan.nextInt();

     // call add method
     try {
       int sum = Addition.add(a, b);
       System.out.println("Sum = " + sum);
     } catch(NegativeNumberException e) {
       System.out.println(e.getMessage());
     }
   }
}
```

📤 **Output:**

```
Enter first number: -5
Enter second number: 20
Pass only +ve number
```

In the next post, we will develop more [Java custom exception examples](186_Java_Custom_Exception_Example.md) based on real-time.

> 📝 **Note:** We can create our custom exception derived from anyone of `Error`, `RuntimeException`, `Throwable`, `Exception`, or one of its sub-class. But generally, we develop java user-defined custom exceptions for the business logic so it should be derived from the `Exception` class.

---

## 3. A Custom Exception should be Derived From Which Class & Why?

**Why should we extend the custom exception class from the `java.lang.Exception` class only?**

For making sure it is compulsory handling by the programmer, it is recommended to derive custom exception from `Exception` class only.

**What happens if we extend our custom exception class from `java.lang.Error`, `java.lang.Throwable`, or `java.lang.RuntimeException`?**

| Base Class 🏷️ | Recommendation 📋 | Reason ⚙️ |
|--------------|-------------------|----------|
| **`java.lang.Error`** | ❌️ Not Recommended | We are not writing exceptions for handling errors in JVM internal logic |
| **`java.lang.Throwable`** | ❌️ Not Recommended | Creates a new category of exception; won't be caught by `catch(Exception e)` |
| **`java.lang.RuntimeException`** | ⚠️ Only if unchecked needed | Compiler doesn't verify exception handling; business logic exceptions should be checked |
| **`java.lang.Exception`** | ✅ Recommended | Compiler checks handling; ensures proper exception management |

🔑 **Key Point:** We should create a custom exception class for throwing these exceptions when a condition is failed and also for forcing the compiler to validate or to check whether the exception is handled. So, it is recommended to derive the exception from `java.lang.Exception` class. The exceptions derived from the `Exception` class are checked exception and handling of those exceptions checked by the compiler.

---

## 4. Developing User-Defined Unchecked Exception

**Q) Can we develop checked exceptions?**
Yes, we can develop checked exceptions derived from `java.lang.Exception` class.

**Q) Can we develop unchecked exceptions?**
Yes, we can develop unchecked exceptions derived from `java.lang.RuntimeException` class.

Many people think that we can't develop a java custom exception as an unchecked exception. But it is wrong, we can develop unchecked exceptions.

> ⚠️ **Caution:** In real-time application development, it is not recommended to develop the unchecked exception. The program is given only for knowledge and practice purposes.

Here we will develop the previous exception `NegativeNumberException` as an unchecked exception. To develop unchecked exceptions, our custom exception should be derived from `java.lang.RuntimeException` class.

**NegativeNumberException (unchecked):**

```java
public class NegativeNumberException extends RuntimeException {

   public NegativeNumberException(){super();}

   public NegativeNumberException(String msg){
      super(msg);
   }

}
```

**Addition.java:**

```java
public class Addition {

  public static int add(int a, int b)
          throws NegativeNumberException {

      if(a<0 || b<0) throw
          new NegativeNumberException("Pass only +ve number");

      return a+b;
    }

 }
```

**Calculator.java (without catching):**

```java
//Without catching the exception
public class Calculator {

  public static void main(String[] args) {

    // Catching the Exception is optional
    // Compiler will not give error
    int sum = Addition.add(-5,7);
    System.out.println("Sum = " + sum);
  }

}
```

📤 **Output:**

```
Exception in thread "main" NegativeNumberException: Pass only +ve number
at Addition.add(Addition.java:5)
at Calculator.main(Calculator.java:7)
```

> 📝 **Note:** In this program the `NegativeNumberException` is inherited from `RuntimeException` class so, it is an unchecked exception i.e. compiler doesn't verify the exception handling. Hence, we can write a program without throwing or handling the exception.

**Calculator.java (with try-catch):**

```java
//Catching exception using try-catch block
public class Calculator {

   public static void main(String[] args){

     // Catching the Exception is optional
     try {
       int sum = Addition.add(-5,7);
       System.out.println("Sum = " + sum);
     } catch(NegativeNumberException e) {
       System.out.println(e.getMessage());
     }

   }
 }
```

📤 **Output:**

```
Pass only +ve number
```

**Q) Can we develop partial checked exceptions?**
No, we can't create partial checked exceptions. For partial checked exceptions our custom exception should have both checked and unchecked exceptions, which is not possible.

Learn more: [Unchecked Exceptions -- The Controversy](https://docs.oracle.com/javase/tutorial/essential/exceptions/runtime.html)

**Related Java topics:**

- 🛠️ Different ways to get the exception message in Java
- 🧵 Java Inline Thread Creation
