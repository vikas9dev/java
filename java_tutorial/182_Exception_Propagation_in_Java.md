# Exception Propagation in Java

**Exception Propagation in Java** | The process of sending an exception from called method to calling method is called exception propagation.

- [Catching Exception in Called Method](#catching-exception-in-called-method)
- [Catching Exception in Calling Method](#catching-exception-in-calling-method)
- [Another Example of Exception Propagation in Java](#another-example-of-exception-propagation-in-java)
- [Use of Exception Propagation in Java](#use-of-exception-propagation-in-java)

---

Whenever an exception is propagated & that exception is not caught in the calling method then execution of both called and calling method is terminated abnormally.

**Basic propagation example:**

```java
public class Test {

  // called method
  public static void display(){
    System.out.println("display() started.");
    System.out.println(9/0); // Exception raised
    System.out.println("display() ended.");
  }

  // calling method
  public static void main(String[] args) {
    System.out.println("main() started.");
    display();
    System.out.println("main() Ended.");
  }
}
```

📤 **Output:**

```
main() started.
display() started.
Exception in thread "main" java.lang.ArithmeticException: / by zero
at Test.display(Test.java:6)
at Test.main(Test.java:13)
```

In this program, `main()` called `display()` method. Here the `main()` method is the calling method and the `display()` method is the called method.

There is an `ArithmeticException` occurring in the `display()` method. The `display()` method didn't handle this exception, so the execution of the `display()` method is terminated, and the exception is propagated to the calling method i.e. `main()` method. The `main()` method also didn't handle the exception therefore, execution of the `main()` method is also terminated.

```mermaid
graph LR
    D["display()"] -->|Exception propagated| M["main()"]
    M -->|Exception propagated| JVM["JVM"]
    JVM -->|Abnormal termination| END["Program Ends"]

    classDef red fill:#EA5455,stroke:#EA5455,color:#fff
    classDef orange fill:#FF9F43,stroke:#FF9F43,color:#fff
    classDef purple fill:#A162F7,stroke:#A162F7,color:#fff

    class D red
    class M orange
    class JVM purple
    class END red
```

The above exception can be handled at two levels:

- 🛡️ In the called method Or,
- 🛡️ In the calling method

Also see: Different ways to get the exception message, [Develop User-defined Custom exception](185_Develop_User_defined_Custom_Exception_in_Java.md), [Java Custom Exception Example](186_Java_Custom_Exception_Example.md)

---

## 1. Catching Exception in Called Method

Let us understand first how to handle the exception in the called method.

If the exception will be caught in the called method (`display()` method) then the execution of the called method will not be terminated and the **exception will not be propagated** to the calling method (`main()` method).

**Handling in called method:**

```java
public class Test {

  // called method
  public static void display(){
    System.out.println("display() started.");
    try {
      System.out.println(9/0); // Exception
    } catch(ArithmeticException e){
      System.out.println("Exception caught in display() method");
    }
    System.out.println("display() ended.");
  }

  // calling method
  public static void main(String[] args) {
    System.out.println("main() started.");
    display();
    System.out.println("main() Ended.");
  }
}
```

📤 **Output:**

```
main() started.
display() started.
Exception caught in display() method
display() ended.
main() Ended.
```

✅ The execution of the `display()` method is completed normally because the exception raised in the `display()` method is caught by the catch block. After execution of the `display()` method, control came back to the main method and main method execution resumed.

> 📝 **Note:** The exception is raised in the called method but that exception is handled using the try-catch block so, the exception is not propagated and execution of both methods is completed normally.

---

## 2. Catching Exception in Calling Method

The exception can be caught in the calling method. But in this case `display()` method execution will be terminated and an **exception is propagated** to the main method. Hence the execution of the `display()` method was completed abnormally but the execution of the `main()` method was completed normally.

**Handling in calling method:**

```java
public class Test {

  // called method
  public static void display(){
    System.out.println("display() started.");
    System.out.println(9/0); // Exception
    System.out.println("display() ended.");
  }

  // calling method
  public static void main(String[] args) {
    System.out.println("main() started.");
    try {
      display();
    } catch(ArithmeticException e){
      System.out.println("Exception caught in main() method");
    }
    System.out.println("main() Ended.");
  }
}
```

📤 **Output:**

```
main() started.
display() started.
Exception caught in main() method
main() Ended.
```

---

## 3. Another Example of Exception Propagation in Java

The above examples are small examples of exception propagation in Java. In real-time, the exception can be propagated to multiple methods. The below program shows when an exception is propagated to the 2 different methods.

**Multi-level propagation:**

```java
public class Test {

  public static void m1(){
    System.out.println("m1() start");
    m2();
    System.out.println("m1() end");
  }

  public static void m2(){
    System.out.println("m2() start");
    System.out.println(9/0);
    System.out.println("m2() end");
  }

  public static void main(String[] args) {
    System.out.println("main() start");
    m1();
    System.out.println("main() end");
  }
}
```

📤 **Output:**

```
main() start
m1() start
m2() start
Exception in thread "main" java.lang.ArithmeticException: / by zero
at Test.m2(Test.java:9)
at Test.m1(Test.java:4)
at Test.main(Test.java:14)
```

```mermaid
graph LR
    M2["m2()"] -->|Exception propagated| M1["m1()"]
    M1 -->|Exception propagated| MAIN["main()"]
    MAIN -->|Exception propagated| JVM["JVM"]

    classDef red fill:#EA5455,stroke:#EA5455,color:#fff
    classDef orange fill:#FF9F43,stroke:#FF9F43,color:#fff
    classDef purple fill:#A162F7,stroke:#A162F7,color:#fff
    classDef cyan fill:#00b4d8,stroke:#00b4d8,color:#fff

    class M2 red
    class M1 orange
    class MAIN cyan
    class JVM purple
```

In this program, the exception is raised in the `m2()` method. The exception is not handled by the `m2()` method therefore, execution of the `m2()` method is terminated and the exception is propagated to the calling method `m1()`.

The `m1()` is also not handling the exception so, the execution of the `m1()` method is terminated and the exception is propagated to its own calling method. For the `m1()` method the calling method is the `main()` method.

The exception is propagated to the `main()` method and it also does not handle the exception. Hence, execution of `main()` is terminated and an exception is displayed on the console.

We can handle the above exception in 3 different ways:

1. Handle the exception in the `m2()` method
2. Handle the exception in the `m1()` method
3. Handle the exception in the `main()` method

**Handle the exception in m2() method:**

```java
// Handling the exception in m2() method
public class Test {
  public static void m1(){
    System.out.println("m1() start");
    m2();
    System.out.println("m1() end");
  }

  public static void m2(){
    System.out.println("m2() start");
    try {
      System.out.println(9/0);
    } catch(ArithmeticException e){
      System.out.println("Exception caught in m2()");
    }
    System.out.println("m2() end");
  }

  public static void main(String[] args) {
    System.out.println("main() start");
    m1();
    System.out.println("main() end");
  }
}
```

📤 **Output:**

```
main() start
m1() start
m2() start
Exception caught in m2()
m2() end
m1() end
main() end
```

**Handle the exception in m1() method:**

```java
// Handling the exception in m1() method
public class Test {
  public static void m1(){
    System.out.println("m1() start");
    try {
      m2();
    } catch(ArithmeticException e){
      System.out.println("Exception caught in m1()");
    }
    System.out.println("m1() end");
  }

  public static void m2(){
    System.out.println("m2() start");
    System.out.println(9/0);
    System.out.println("m2() end");
  }

  public static void main(String[] args) {
    System.out.println("main() start");
    m1();
    System.out.println("main() end");
  }
}
```

📤 **Output:**

```
main() start
m1() start
m2() start
Exception caught in m1()
m1() end
main() end
```

**Handling the exception in main() method:**

```java
// Handling the exception in main() method
public class Test {
  public static void m1(){
    System.out.println("m1() start");
    m2();
    System.out.println("m1() end");
  }

  public static void m2(){
    System.out.println("m2() start");
    System.out.println(9/0);
    System.out.println("m2() end");
  }

  public static void main(String[] args) {
    System.out.println("main() start");
    try {
      m1();
    } catch(ArithmeticException e){
      System.out.println("Exception caught in main()");
    }
    System.out.println("main() end");
  }
}
```

📤 **Output:**

```
main() start
m1() start
m2() start
Exception caught in main()
main() end
```

---

## 4. Use of Exception Propagation in Java

In real-time one method is called through many different methods. Sometimes we need to find the flow of execution of the method that is called through which methods. In that situation, we have two options: by debugging and by exception propagation.

🔍 Debugging process is useful if we want to find more information but if we only want to find only the order of method calls then the exception propagation process will be very useful for us.

> 💡 **Tip:** Raise the exception in the method where you want to see the execution flow and observe the exception message.

**Finding execution flow using exception propagation:**

```java
class FindExecutionFlow {
  static void m1(){ m2(); }
  static void m2(){ display(); }
  static void m3(){ test(); }
  static void m4() { display(); }
  static void test() { display1(); }
  static void test0() { int x = 5/0; }
  static void display(){ m3(); }
  static void display1() { test0(); }
  static void display2() { test(); }
  public static void main(String[] args) {
    m1();
    display2();
    m4();
  }
}
```

📤 **Output:**

```
Exception in thread "main" java.lang.ArithmeticException: / by zero
at FindExecutionFlow.test0(FindExecutionFlow.java:7)
at FindExecutionFlow.display1(FindExecutionFlow.java:9)
at FindExecutionFlow.test(FindExecutionFlow.java:6)
at FindExecutionFlow.m3(FindExecutionFlow.java:4)
at FindExecutionFlow.display(FindExecutionFlow.java:8)
at FindExecutionFlow.m2(FindExecutionFlow.java:3)
at FindExecutionFlow.m1(FindExecutionFlow.java:2)
at FindExecutionFlow.main(FindExecutionFlow.java:12)
```

> 🔑 **Key Point:** By observing the exception message, we can conclude that the execution flow for the `test0()` method is `test0()` -> `display1()` -> `test()` -> `m3()` -> `display()` -> `m2()` -> `m1()` -> `main()`.
