# Different Ways to Get Exception Message in Java

**Different Ways to Get Exception Message in Java** | In the `Throwable` class of Java, three methods are given to get the exception message from catch blocks. `Throwable` class is the superclass of all exceptions.

- [Exception Messages displayed by the JVM](#exception-messages-displayed-by-the-jvm)
- [Get Exception Message in Java Using printStackTrace()](#get-exception-message-in-java-using-printstacktrace)
- [Get Exception Message in Java Using toString()](#get-exception-message-in-java-using-tostring)
- [Get Exception Message in Java Using getMessage()](#get-exception-message-in-java-using-getmessage)
- [Difference Between printStackTrace(), toString() and getMessage() Method](#difference-between-printstacktrace-tostring-and-getmessage-method)
- [Exercise](#exercise)

---

The three methods of `Throwable` class to print exception object stack trace are:

1. 📋 **`printStackTrace()`**
2. 🏷️ **`toString()`**
3. 💬 **`getMessage()`**

These methods are useful when we write `catch` block with superclass as a parameter. But before going further first we have to observe how JVM displays the exception message and how much the above-said methods display similar exception messages in Java.

---

## 1. Exception Messages displayed by the JVM

By default, the JVM displays the name of the thread, exception name, the reason for the exception, and the line/place of the exception where it occurs.

🖥️ **The exception message format, displayed by JVM:**

`Exception in thread <thread-name> <exception-name> : <reason for the exception> <place of the exception>`

**Example to demonstrate how JVM displays an exception message:**

```java
public class Test {
   public static void main(String[] args) {
      System.out.println(9/0);
   }
}
```

📤 **Output:**

```
Exception in thread "main" java.lang.ArithmeticException: / by zero
at Test.main(Test.java:3)
```

---

## 2. Get Exception Message in Java Using printStackTrace()

The `printStackTrace()` method of `java.lang.Throwable` prints exception name, the reason for the exception, and line/place of the exception where it occurs. It doesn't display the thread name where the exception occurs.

The prototype of the `printStackTrace()` method is:

- `public void printStackTrace()`

🖥️ **The exception message format, displayed by `printStackTrace()`:**

`Exception name: <reason of the exception> <place of the exception>`

**Usage example:**

```java
catch(Exception e) {
   e.printStackTrace();
}
```

**Full demonstration:**

```java
public class Test {
   public static void main(String[] args) {
      try {
         System.out.println(9/0);
      } catch(ArithmeticException ae) {
         ae.printStackTrace();
      }
   }
}
```

📤 **Output:**

```
java.lang.ArithmeticException: / by zero
at Test.main(Test.java:4)
```

---

## 3. Get Exception Message in Java Using toString()

The `toString()` method is an overridden method in the `java.lang.Throwable` class, its return type is `String`. It returns the exception name, and reason of the exception as a string.

🖥️ **The exception message format, displayed by `toString()`:**

`Exception name: <reason of the exception>`

To display the exception message using the `toString()` method, we can call the `toString()` method or we can directly use the parameter name.

**Usage example:**

```java
catch(ArithmeticException e) {
   System.out.println(e.toString());
   // Or,
   System.out.println(e);
}
```

**Full demonstration:**

```java
public class Test {
   public static void main(String[] args) {
      try {
         System.out.println(9/0);
      } catch(ArithmeticException ae) {
         System.out.println(ae);
      }
   }
}
```

📤 **Output:**

```
java.lang.ArithmeticException: / by zero
```

---

## 4. Get Exception Message in Java Using getMessage()

The `getMessage()` method of `java.lang.Throwable` class returns `String`. It gives only the reason for the exception. Most of the time we use the `getMessage()` method to display the message of the exception.

🖥️ **The exception message format, displayed by `getMessage()`:**

`<reason for the exception>`

**Usage example:**

```java
catch(Exception e) {
   System.out.println(e.getMessage());
}
```

**Full demonstration:**

```java
public class Test {
   public static void main(String[] args) {
      try {
         System.out.println(9/0);
      } catch(ArithmeticException ae) {
         System.out.println(ae.getMessage());
      }
   }
}
```

📤 **Output:**

```
/ by zero
```

---

## 5. Difference Between printStackTrace(), toString() and getMessage() Method

| Way to get Message 🛠️ | Thread Name 🧵 | Exception Name 🏷️ | Reason for Exception 📋 | Place of Exception 📍 |
|------------------------|---------------|-------------------|------------------------|---------------------|
| **JVM** | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes |
| **`printStackTrace()`** | ❌️ No | ✅ Yes | ✅ Yes | ✅ Yes |
| **`toString()`** | ❌️ No | ✅ Yes | ✅ Yes | ❌️ No |
| **`getMessage()`** | ❌️ No | ❌️ No | ✅ Yes | ❌️ No |

**Program to Demonstrate Different Ways to Get Exception Message in Java:**

```java
class DisplayExceptionMsg {

   public static void main(String[] args) {

     try {
       System.out.println(9/0);
     } catch(ArithmeticException e) {

       // getMessage() method
       System.out.println("The getMessage() method Output: ");
       System.out.println(e.getMessage());
       System.out.println();

       // toString() method
       System.out.println("The toString() method Output: ");
       System.out.println(e.toString());
       // Or,
       System.out.println(e);
       System.out.println();

       // printStackTrace()
       System.out.println("The printStackTrace() method Output: ");
       e.printStackTrace();
       System.out.println();

       // JVM default message
       System.out.println("JVM default exception message: ");
       throw e;
       /* By using above statement we are
        * re-throwing the caught exception.
        *
        * This exception will be caught
        * by JVM default handler.
        */
    }
  }
}
```

📤 **Output:**

```
The getMessage() method Output:
/ by zero

The toString() method Output:
java.lang.ArithmeticException: / by zero
java.lang.ArithmeticException: / by zero

The printStackTrace() method Output:
java.lang.ArithmeticException: / by zero
at DisplayExceptionMsg.main(Test.java:6)

JVM default exception message:
Exception in thread "main" java.lang.ArithmeticException: / by zero
at DisplayExceptionMsg.main(Test.java:6)
```

---

## 6. Exercise

**Question:** From the below options find which exception message is displayed by the JVM or by which method of `java.lang.Throwable` class?

**Msg1:**

```
java.lang.ArithmeticException: / by zero
at FindExecutionFlow.main(ExceptionPropagation.java:15)
```

**Msg2:**

```
Exception in thread "main" java.lang.ArithmeticException: / by zero
at FindExecutionFlow.main(ExceptionPropagation.java:15)
```

> 💡 **Tip:** The exception message of Msg1 is displayed by the `printStackTrace()` and the second exception message is displayed by the JVM. The main difference in the exception message displayed by JVM and `printStackTrace()` is thread-name. The JVM displayed the name of the thread where the exception occurs but the `printStackTrace()` method doesn't display thread-name.

**Related Java topics:**

- 🛠️ [Develop User-defined Custom exception](185_Develop_User_defined_Custom_Exception_in_Java.md)
- 💻 [Java Custom Exception Example](186_Java_Custom_Exception_Example.md)
- 🧵 Java Inline Thread Creation
