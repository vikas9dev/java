# Deadlock in Java with Example

**Deadlock in Java with Example** | Understanding deadlock situations, what causes them, and how to avoid them in multithreaded Java programs.

- [Deadlock Example in Java](#deadlock-example-in-java)
- [How to solve or avoid deadlock in Java](#how-to-solve-or-avoid-deadlock-in-java)

---

**If two threads are waiting for each other to complete their execution then such a type of infinite waiting situation is called deadlock.**

Let us understand it through an **example:** Assume there are two threads. The first thread is waiting for the completion of the second thread, once the second thread execution is completed then the first thread will continue its execution. Similarly, the second thread is waiting for the completion of the first thread, once the first thread execution is completed then the second thread will continue its execution. Both threads are waiting for each other an infinite number of times.

Let us understand the deadlock through a **real-life example:** You and your friend want to go to the movie on Saturday evening, you both bought tickets a few days ago. There are two roads to go to the movie hall either passing through your house or passing through your friend's house, the overall distance is approximately the same.

On Saturday evening, you are waiting for your friend at your home so that when he/she comes then both will go together. Similarly, your friend is waiting for you at his/her own home so that when you come then both will go together. Due to some reason neither you want to call/message your friend nor your friend wants. Both of you also don't want to go alone, just waiting for each other. This situation is nothing but a deadlock situation where two threads are waiting for each other forever.

```mermaid
graph LR
    T1["Main Thread"] -->|Holds lock of A, Waiting for lock of B| T2["Thread-0"]
    T2 -->|Holds lock of B, Waiting for lock of A| T1

    classDef purple fill:#A162F7,stroke:#A162F7,color:#fff
    classDef cyan fill:#00b4d8,stroke:#00b4d8,color:#fff

    class T1 purple
    class T2 cyan
```

---

## 1. Deadlock Example in Java

What is the keyword that causes deadlock? The `synchronized` keyword. **Synchronization is the only reason for a deadlock situation**, hence while using the synchronized keyword we must be careful because the wrong implementation could lead to the deadlock situation.

> 🔑 **Key Point:** In Java, if we don't use the `synchronized` keyword then we never encounter the deadlock situation.

**Program to demonstrate deadlock in Java using the synchronized method:**

```java
public class MyThread extends Thread {

   public static A a = new A();
   public static B b = new B();

   public static void main(String[] args) {
      System.out.println("Main thread Started.");
      MyThread t1 = new MyThread();
      t1.start();
      a.m1(b);
      System.out.println("Main thread Ended.");
   }

   public void run() {
      System.out.println("Thread-0 Started.");
      b.m2(a);
      System.out.println("Thread-0 Ended.");
   }
}

class A {
   public synchronized void m1(B b) {
      try {
         Thread.sleep(2000); // 2 sec
      } catch (InterruptedException ie) {}
      System.out.println("Calling display()");
      b.display();
   }
   public synchronized void show() {
      System.out.println("show() method");
   }
}

class B {
   public synchronized void m2(A a) {
      try {
         Thread.sleep(2000); // 2 sec
      } catch (InterruptedException ie) {}
      System.out.println("Calling show()");
      a.show();
   }
   public synchronized void display() {
      System.out.println("display() method");
   }
}
```

📤 **Output:**

```
Main thread Started.
Thread-0 Started.
Calling display()
Calling show()
<program-stuck>
```

> ⚠️ **Caution:** To terminate the above program, type CTRL+C in the console window.

**In this program, there are two threads: main thread and thread-0.** The `a.m1(b);` line will be executed by the main thread whereas `b.m2(a);` line will be executed by thread-0.

🔒 The **`m1()` method** is called on "a" object and since it is a synchronized method trying to perform an update operation on "a" object therefore to execute the `m1()` method, the main thread needs the lock of "a" object. The lock of "a" object is available, currently not used by other threads therefore the main thread got lock of "a" object.

🔒 Similar story with `b.m2(a);` line. The **`m2()` method** is a synchronized method and called on "b" objects therefore thread-0 requires the lock of the "b" object. Currently, the lock of "b" is available therefore thread-0 will get the lock of the "b" object.

While executing `m1()` method **main thread** encounters `b.display()` method. The `display()` method is also a synchronized method which is called on the "b" object therefore to execute the `display()` method the main thread needs a lock of the "b" object. But currently, the "b" object lock is held by thread-0 and busy in the execution of the `m2()` method. Therefore the main thread will enter into the waiting state to get the lock of the "b" object. So, **currently, the main thread is holding the lock of the "a" object and waiting to get the lock of the "b" object.**

At the same time, while executing `m2()` method **thread-0** encounters `a.show()` method. To execute the `show()` method, thread-0 needs the lock of "a" object because the `show()` method is a synchronized method and called on "a" object. But "a" object lock is already held by the main thread performing its own operation. Therefore thread-0 will be entered into the waiting state to get the lock of "a" object. So, **currently, thread-0 is holding the lock of the "b" object and waiting to get the lock of the "a" object.**

In the current situation, the main thread is holding "a" object lock and waiting to get "b" object lock meanwhile thread-0 is holding "b" object lock and waiting to get "a" object lock. Until getting the "b" object lock, the main thread won't release the lock of the "a" object. Similarly, till getting the lock of the "a" object thread-0 won't release the lock of the "b" object. **Hence both threads will wait for each other forever.** This situation is nothing but a deadlock in Java.

You can use different tools to check whether a program is reached in a deadlock situation or not. See more: [**How to detect deadlock in Java?**](188_How_to_Detect_Deadlock_in_Java.md) In the thread dump we can find the following message:

**Thread dump output:**

```
Found one Java-level deadlock:
=============================
"main":
waiting to lock monitor 0x00007f3be00f0180 (object 0x00000000c7b1ad70, a B),
which is held by "Thread-0"

"Thread-0":
waiting to lock monitor 0x00007f3b7c000f70 (object 0x00000000c7b1a2c0, a A),
which is held by "main"
```

If you read carefully "Java stack information for the threads" then you will find the main thread is waiting to lock "b" at the 38th line i.e `display()` method, and currently, it holds the lock of "a" object since the 8th line i.e. `a.m1(b)` method call. Similarly, thread-0 is waiting to lock "a" object at the 26th line, and currently, it holds the lock of the "b" object since line 13 i.e. `b.m2(a)` method call.

The above program was an example of a deadlock in Java where all methods were synchronized, and one synchronized method is called from another synchronized method. Now, let us see **another program where synchronized blocks are used, and nested synchronized blocks lead to deadlock situations.**

**Deadlock in Java from the synchronized block:**

```java
public class Test {
   private static String str1 = "Know Program";
   private static String str2 = "Learn Java";

   public static void main(String[] args) {
      MyThread1 t1 = new MyThread1();
      MyThread2 t2 = new MyThread2();
      t1.start();
      t2.start();
   }

   private static class MyThread1 extends Thread {
      public void run() {
         synchronized(str1) {
            System.out.println("str1 locked by Thread-0");
            try {Thread.sleep(1000);} catch (Exception e) {}
            System.out.println("Thread-0 trying to get lock of str2");
            synchronized(str2) {
               System.out.println("str2 locked by Thread-0");
            }
         }
      }
   }

   private static class MyThread2 extends Thread {
      public void run() {
         synchronized(str2) {
            System.out.println("str2 locked by Thread-1");
            try {Thread.sleep(1000);} catch (Exception e) {}
            System.out.println("Thread-1 trying to get lock of str1");
            synchronized(str1) {
               System.out.println("str1 locked by Thread-0");
            }
         }
      }
   }
}
```

📤 **Output:**

```
str2 locked by Thread-1
str1 locked by Thread-0
Thread-1 trying to get lock of str1
Thread-0 trying to get lock of str2
<program-stuck>
```

**Thread dump for synchronized block deadlock:**

```
Found one Java-level deadlock:
=============================
"Thread-0":
waiting to lock monitor 0x00007f10c0002310 (object 0x00000000c7b19330, a java.lang.String),
which is held by "Thread-1"

"Thread-1":
waiting to lock monitor 0x00007f10b4001930 (object 0x00000000c7b192f8, a java.lang.String),
which is held by "Thread-0"

Java stack information for the threads listed above:
===================================================
"Thread-0":
at Test$MyThread1.run(Test.java:19)
- waiting to lock <0x00000000c7b19330> (a java.lang.String)
- locked <0x00000000c7b192f8> (a java.lang.String)
"Thread-1":
at Test$MyThread2.run(Test.java:32)
- waiting to lock <0x00000000c7b192f8> (a java.lang.String)
- locked <0x00000000c7b19330> (a java.lang.String)

Found 1 deadlock.
```

---

## 2. How to solve or avoid deadlock in Java

There is no resolution technique (solution) for deadlock in Java but there are several prevention techniques available to avoid deadlock in Java.

Avoiding deadlock in Java is a complex process and not easy to catch but if we try, then we can avoid this. The deadlock situation occurred due to synchronized keywords therefore while using the synchronized method or synchronized block be careful. We can't completely solve deadlock but we can use the below techniques to avoid deadlock situations.

| Prevention Technique 🛡️ | Description 📋 |
|--------------------------|---------------|
| **1) Avoid nested locks** | Avoid nested locks as much as possible |
| **2) Avoid unnecessary locks** | Use locks only on necessary objects |
| **3) Use thread join** | Use `join(long ms)` or `join(long ms, int ns)` to wait for a certain period of time |

**Related Terminologies:**

- 🔄 **Starvation:** Starvation describes a situation where a thread is unable to gain regular access to shared resources and is unable to make progress. This happens when shared resources are made unavailable for long periods by "greedy" threads. See more: [What is starvation in Java, the difference between deadlock vs starvation?](189_Starvation_in_Java_with_Example.md)

- 🏃 **Livelock:** A thread often acts in response to the action of another thread. If the other thread's action is also a response to the action of another thread, then livelock may result. As with deadlock, livelocked threads are unable to make further progress.

Also see: Interview questions on deadlock and Java multithreading
