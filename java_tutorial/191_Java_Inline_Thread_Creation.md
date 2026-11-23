# Java Inline Thread Creation

**Java Inline Thread Creation** | In Java, a thread created with an anonymous inner class or by using a lambda expression is called an inline thread.

- [Inline Thread Creation Using Thread class](#inline-thread-creation-using-thread-class)
- [Inline Thread Creation using Runnable Interface](#inline-thread-creation-using-runnable-interface)
- [Inline Thread Creation using Lambda Expression](#inline-thread-creation-using-lambda-expression)

---

## 1. Inline Thread Creation Using Thread class

Anonymous thread object means a thread that is created without extending from `Thread` class or implementing from `Runnable` interface explicitly is called an "anonymous" thread object. The other name for the anonymous thread object is the "inline" thread.

Using an anonymous inner class we can create a `Thread` without extending from `Thread` class or implementing from `Runnable` interface explicitly.

🧵 **Syntax to create an inline thread using Thread class:**

```java
new Thread() {
  public void run(){
    //code.....
  }
}.start();
```

🛠️ **Creating inline thread using Thread class:**

```java
class CustomThread{
  public static void main(String[] args) {
    System.out.println("main thread execution started");

    new Thread() {
      public void run(){
        for(int i=1; i<=5; i++){
          System.out.println("run: "+i);
        }
      }
    }.start();

    System.out.println("main thread execution completed");
  }
}
```

📤 **Output:**

```
main thread execution started
main thread execution completed
run: 1
run: 2
run: 3
run: 4
run: 5
```

🧵 One custom thread is created and the `run()` method is executed from the anonymous inner class. Along with the main thread, the inline thread is executed concurrently.

---

## 2. Inline Thread Creation using Runnable Interface

🧵 **Syntax to create an inline thread using Runnable interface:**

```java
new Thread(
  new Runnable(){
    public void run(){
      //code....
    }
  }
).start();
```

🛠️ **Inline thread creation using Runnable interface:**

```java
class InlineThread_Runnable{
   public static void main(String[] args) {
     System.out.println("main thread execution started");
     System.out.println("Inline thread creation using Runnable interface");

     new Thread(
       new Runnable(){
         public void run(){
           System.out.println("Inline thread execution started");
           for(int i=0; i<=1; i++){
             System.out.println("run :"+i);
           }
           try{Thread.currentThread().sleep(200);}
           catch(InterruptedException e){}
           System.out.println("Inline thread execution completed");
         }
       }
     ).start();

     try{Thread.currentThread().sleep(100);}
     catch(InterruptedException e){}
     System.out.println("main thread execution completed");
   }
}
```

📤 **Output:**

```
main thread execution started
Inline thread creation using Runnable interface
Inline thread execution started
run: 0
run: 1
main thread execution completed
Inline thread execution completed
```

---

## 3. Inline Thread Creation using Lambda Expression

🧵 **Lambda expression syntax for inline thread from the Runnable interface:**

```java
new Thread( ()-> /* code..*/).start();
```

🛠️ **Inline thread creation using Lambda expression:**

```java
class InlineThread_Runnable {
   public static void main(String[] args) {
     System.out.println("main thread execution started");

     new Thread(
       ()-> System.out.println("Inline thread")
       //Only one statement so semicolon isn't required.
     ).start();

     System.out.println("main thread execution completed");
   }
}
```

📤 **Output:**

```
main thread execution started
main thread execution completed
Inline thread
```

---

## 4. When to Use an Inline Thread

💡 **Tip:** If we want thread representation (some implementation) only one time not repeatedly then we should use an inline thread. But if we want to use implementation repeatedly with the concurrent flow of execution then instead of using an inline thread, we should create thread objects by using `Thread` class or through `Runnable` interface.

📝 **Note:** Inline thread is not the "official" Java term. It is invented by textbook authors or software industry experts.

🔗 **Useful links:**

- [What is an inline thread](https://stackoverflow.com/questions/2000218/what-is-inline-thread)
- [Green threads](https://en.wikipedia.org/wiki/Green_threads)
- [Green thread vs non-green threads](https://stackoverflow.com/questions/5713142/green-threads-vs-non-green-threads)

📚 **Also learn:**

- [Deadlock in Java with Example](187_Deadlock_in_Java_with_Example.md)
- [How to Detect Deadlock in Java](188_How_to_Detect_Deadlock_in_Java.md)
- [Starvation in Java with Example](189_Starvation_in_Java_with_Example.md)
- [Daemon Thread in Java](190_Daemon_Thread_in_Java_with_Examples.md)
