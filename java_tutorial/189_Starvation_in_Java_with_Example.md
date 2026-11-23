# Starvation in Java with Example

**Starvation in Java with Example** | Understanding thread starvation, how it differs from [deadlock](187_Deadlock_in_Java_with_Example.md), and how to identify starvation situations.

- [Starvation Example with Synchronized Block](#starvation-example-with-synchronized-block)
- [Starvation with Infinite Loop](#starvation-with-infinite-loop)
- [Deadlock vs Starvation in Java](#deadlock-vs-starvation-in-java)

---

**Starvation describes a situation where a thread is unable to gain regular access to shared resources and is unable to make progress. This happens when shared resources are made unavailable for long periods by "greedy" threads.**

For example, suppose an object provides a synchronized method that often takes a long time to return. If one thread invokes this method frequently, other threads that also need frequent synchronized access to the same object will often be blocked.

🧠 **In Simple Words:** When two threads are having different priority then the thread having higher priority will get the first chance to execute. Low priority thread has to wait until completing all high priority threads. It may have to wait for a long time period for its execution but waiting will end at a certain point. This situation is an example of starvation.

Let us understand starvation in Java through an example: Assume there are 10,000 threads running. Among them, one thread is having priority=1 (lowest priority), and the remaining all threads are having a priority greater than 1 (priority > 1). In this case, the thread having priority=1 has to wait till the completion of all remaining threads having high priority.

---

## 1. Starvation Example with Synchronized Block

```java
class MyThread extends Thread {
   public void run() {
      String threadName = Thread.currentThread().getName();
      System.out.println(threadName + " Started");
      synchronized(MyThread.class) { // lock
         // doing some useful work
         try {
            Thread.sleep(2000); // 2 sec
         } catch (InterruptedException ie){}
      }
      System.out.println(threadName + " End");
   }
}

public class Test {
   public static void main(String[] args) {
      System.out.println("Start of Main thread");
      MyThread mt[] = new MyThread[10];
       for (int i=0; i<mt.length; i++) {
          mt[i] = new MyThread(); // create thread
          mt[i].start();
       }
       System.out.println("End of Main thread");
   }
}
```

📤 **Output:**

```
Start of Main thread
End of Main thread
Thread-9 Started
Thread-8 Started
Thread-0 Started
Thread-6 Started
Thread-7 Started
Thread-4 Started
Thread-2 Started
Thread-5 Started
Thread-3 Started
Thread-1 Started
Thread-9 End
Thread-1 End
Thread-7 End
Thread-3 End
Thread-4 End
Thread-5 End
Thread-2 End
Thread-6 End
Thread-0 End
Thread-8 End
```

In this example, the main thread created 10 child threads. To execute some portion of the `run()` method (synchronized block) each child thread needs the lock of the current class. At a time only one thread can get the lock of one object. And to complete execution, each thread required more than 2 seconds time.

> 📝 **Note:** Among these 10 threads, there will be some threads executing at last. They were waiting for a long period of time because the thread was unable to gain regular access to shared resources (lock of current class) and was unable to make progress. In the above output, thread-8 waited for a long period of time.

---

## 2. Starvation with Infinite Loop

```java
public class Main {
   public static void main(String[] args) {
      System.out.println("Main thread Started");
      MyThread t1 = new MyThread();
      MyThread t2 = new MyThread();
      t1.start();
      t2.start();
      System.out.println("Main thread Ended");
   }
}

class MyThread extends Thread {
   public void run() {
      String threadName = Thread.currentThread().getName();
      System.out.println(threadName + " Started.");
      synchronized(MyThread.class) {
         System.out.println(threadName + " synchronized block.");
         while(true) { } // infinite loop
      }
      // System.out.println(threadName + " Ended.");
   }
}
```

📤 **Output:**

```
Main thread Started.
Main thread Ended.
Thread-0 Started.
Thread-1 Started.
Thread-0 synchronized block.
```

> ⚠️ **Caution:** To terminate the program execution, type CTRL + C in the command prompt.

This program is also an example of starvation. In this program, we created two threads. The first thread starts execution and gets the lock of the current class, but there is an infinite loop therefore **the first thread itself will never complete** and the lock of the current class will never be released. Hence the second thread will never get a chance to get the lock of the current class.

> 🔑 **Key Point:** This situation is **not a deadlock situation**. In deadlock two threads are waiting for each other forever. See more: [Deadlock in Java with Example](187_Deadlock_in_Java_with_Example.md). But in this case, **only the second thread is waiting for completion of the first thread execution** so that it can get the lock of the current class. The **first thread is not waiting for any resources** or any thread to complete execution, it is doing its own job i.e. executing infinite while loop.

You can also use tools to detect whether it is a deadlock or not. See more: [how to detect deadlock in Java?](188_How_to_Detect_Deadlock_in_Java.md) When you use Java's "JCMD" tool then you can see the logs below, but for deadlock situations, you will get a clear message showing "deadlock occurred".

**JCMD tool output for starvation (not deadlock):**

```
"Thread-0" ... waiting for monitor entry
java.lang.Thread.State: BLOCKED (on object monitor)
at MyThread.run(Main1.java:17)
- waiting to lock <0x00000000c7b1a710> (a java.lang.Class for MyThread)

"Thread-1" ... runnable
java.lang.Thread.State: RUNNABLE
at MyThread.run(Main1.java:18)
- locked <0x00000000c7b1a710> (a java.lang.Class for MyThread)
```

---

## 3. Deadlock vs Starvation in Java

**What is the difference between deadlock and starvation in Java?**

| Aspect 🏷️ | Deadlock 🔒 | Starvation 🍽️ |
|-----------|-----------|--------------|
| **Definition** | Long time waiting where waiting **never ends** | Long time waiting where waiting **may end** at a certain point |
| **Thread Behavior** | Threads are waiting **for each other** | Only one thread is waiting; the other is busy working |
| **Severity** | ❌️ Very severe; program stuck forever | ⚠️ Lesser problem; waiting eventually ends |
| **Detection** | Detectable via thread dump ("Found deadlock") | No explicit "starvation" message in dumps |
| **Prevention** | Avoid nested locks, unnecessary locks | Use fair scheduling, adjust thread priorities |

> 📝 **Note:** Compared to deadlock, starvation is a much lesser problem in concurrent software designing but still, designers are likely to encounter it. Designers have to write code in such a way that a starvation situation should not occur.
