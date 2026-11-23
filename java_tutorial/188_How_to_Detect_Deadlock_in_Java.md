# How to Detect Deadlock in Java

**How to Detect Deadlock in Java** | Using thread dumps and tools to identify [deadlock](187_Deadlock_in_Java_with_Example.md) situations in Java programs.

- [Detect Deadlock in Java Through Thread Dump](#detect-deadlock-in-java-through-thread-dump)

---

Most of the time just by seeing output and program, we can't predict whether it is a deadlock or not. In this post, we will discuss how to detect deadlock in Java and how to detect deadlock in Java programmatically.

First of all, we will take two programs and use them to check whether a deadlock situation came or not. These are simple Java programs, you can use your own programs.

**Program 1 - deadlock situation:**

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

**Program 2 - to check whether it is a deadlock situation or not.** For more see: [Starvation in Java](189_Starvation_in_Java_with_Example.md)

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

---

## 1. Detect Deadlock in Java Through Thread Dump

We can use a full thread dump, it gives information about the running thread. With the help of thread dump, we can detect deadlock in Java. Different ways to get thread dump information:

### a) Use CTRL+\ in Unix and CTRL+BREAK in Windows

When the program is stuck then type CTRL+\ in Unix or CTRL+BREAK in the Windows operating system.

**Compile and run:**

```bash
> javac MyThread.java
> java MyThread
```

📤 **Output:**

```
Main thread Started.
Thread-0 Started.
Calling display()
Calling show()
<program-stuck>
// Now, type CTRL+\ in Unix or CTRL+BREAK in Windows.
```

At a certain point, you will get the below information:

**Thread dump deadlock detection:**

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

### b) Detect Deadlock Using the jcmd Command

From Java 8 version onwards, we can use the `jcmd` command to get the thread dump. Steps to get thread dump information through `jcmd` command:

1. 🔍 **Find PID of the program:** Open a new CMD or terminal, and type `jcmd` command. It will list out all running Java programs with PID and name in the operating system.
2. 📋 **Type `jcmd <PID> Thread.print`**

It will print the thread dump on your console and will also print if your program has a deadlock. You can analyze your Java program with more `jcmd` options listed by command `jcmd <PID> help`.

**Find the PID:**

```bash
> jcmd
5280 jdk.jcmd/sun.tools.jcmd.JCmd
5158 MyThread
```

**Get thread dump:**

```bash
> jcmd 5158 Thread.print
```

### c) Using "kill -3 PID"

Here, PID is the process id. You can find PID through the `jcmd` command. In this approach, the thread dump information will display in the console where the program is running, not in the console where we typed this command.

```bash
> jcmd
5280 jdk.jcmd/sun.tools.jcmd.JCmd
5158 MyThread

> kill -3 5158
```

| Method 🛠️ | Platform 🖥️ | Output Location 📍 |
|-----------|------------|-------------------|
| **CTRL+\ / CTRL+BREAK** | Unix / Windows | Same console |
| **`jcmd <PID> Thread.print`** | All (Java 8+) | New console |
| **`kill -3 <PID>`** | Unix/Linux | Program's console |

> 💡 **Tip:** The `jcmd` approach is the most versatile method as it works on all platforms and provides the output in the console where you typed the command.
