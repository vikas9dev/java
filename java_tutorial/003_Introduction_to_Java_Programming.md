# Introduction to Java Programming

**Introduction to Java Programming** | What is Java, the history of Java, Java version history, features of Java, and the applications of Java.

- [History of Java](#history-of-java)
- [Introduction to Java: Java Version](#introduction-to-java-java-version)
- [Features of Java](#features-of-java)
- [Applications of Java](#applications-of-java)
- [Prerequisites to Learn Java](#prerequisites-to-learn-java)

_Java is a simple, secured, high-level, platform-independent, multithread, Object-oriented programming language._

It's one of the most popular and widely used **programming language**, **platform**, and **technology**. Java is not only a language it is also a platform and technology.

A platform is an environment that helps to develop and run programs written in any programming language. Java has its own software-based platform called **JVM** (Java virtual machine) to execute the programs. Apart from Java, the other programming languages that use JVM are [Kotlin](https://kotlinlang.org/) (used for developing Android applications), [Scala](https://www.scala-lang.org/), [Jython](https://www.jython.org/), [JRuby](https://www.jruby.org/), [Groovy](https://groovy-lang.org/), and many [more](https://en.wikipedia.org/wiki/List_of_JVM_languages).

- 💻 Java is a **programming language** because it provides its own syntaxes and semantics for developing new programs.
- 🖥️ It is a **platform** because it provides its own execution environment called JVM. Java program is not executed directly by the operating system, it is executed by JVM.
- 📚 It is **technology** because it provides a pre-defined rich set of API (library) for fast and easy development.

Java was developed by [SUN microsystems, Inc.](https://en.wikipedia.org/wiki/Sun_Microsystems) (Sun for short) for developing internet-based, high-performance, distributed, dynamically extensible applications. [Oracle Corporation](https://en.wikipedia.org/wiki/Oracle_Corporation) acquired Sun microsystems on January 27, 2010; Now, Java is owned by Oracle Corporation.

Java was invented by [James Gosling](https://en.wikipedia.org/wiki/James_Gosling). He with his team of 11 members invented Java language in SUN microsystems.

---

## 1. History of Java

The Java platform was initially developed to address the problems of building software for network consumer electronic devices. It was designed to support multiple host architectures and to allow secure delivery of software components.

The language was initially called **_OAK_** after an oak tree that stood outside Gosling's Office. They were unable to register this programming language with the name OAK because already some other product was already registered with the same name. Later the project went by the name **_Green_** and was finally renamed **Java**, from [Java coffee](https://en.wikipedia.org/wiki/Java_coffee). Java Arabica coffee is grown on the [island of Java](https://en.wikipedia.org/wiki/Java) in Indonesia.

Earlier C++ was the language that was object-oriented but it has many problems like it is platform dependent. Gosling designed Java with a C/C++ style that system and application programmers would find familiar.

> 📝 **Note:** There is **no abbreviation** or technical meaning for Java. Java specifically does not have any meaning rather it refers to the hot, aromatic drink Coffee. This is the reason the Java programming language icon is the coffee cup.

---

## 2. Introduction to Java: Java Version

SUN microsystems released the public implementation as Java 1.0 on January 23, 1996. It promised _"**write once, run anywhere**" (**WORA**)_ on popular platforms such as Windows operating system, Linux, and Mac OS. Java first version was released as 1.0 followed by 1.1, 1.2, 1.3, 1.4 || 5.0 (1.5), 6(1.6), 7(1.7), 8(1.8) || 9, 10, 11, 12, 13, and so on.

| Java Version 📋 | Release Date 📅 |
|-----------------|----------------|
| **JDK 1.0** | January 23, 1996 |
| **JDK 1.1** | February 19, 1997 |
| **J2SE 1.2** | December 8, 1998 |
| **J2SE 1.3** | May 8, 2000 |
| **J2SE 1.4** | February 6, 2002 |
| **J2SE 5.0** | September 30, 2004 |
| **Java SE 6** | December 11, 2006 |
| **Java SE 7** | July 28, 2011 |
| **Java SE 8** | March 18, 2014 |
| **Java SE 9** | September 21, 2017 |
| **Java SE 10** | March 20, 2018 |
| **Java SE 11** | September 25, 2018 |
| **Java SE 12** | March 19, 2019 |
| **Java SE 13** | September 17, 2019 |
| **Java SE 14** | March 17, 2020 |
| **Java SE 15** | September 15, 2020 |
| **Java SE 16** | March 16, 2021 |
| **Java SE 17** | September 14, 2021 |
| **Java SE 18** | March 22, 2022 |
| **Java SE 19** | September 2022 |
| **Java SE 20** | March 2023 |
| **Java SE 21** | September 2023 |
| **Java SE 22** | March 2024 |
| **Java SE 23** | September 2024 |

The acquisition of Sun Microsystems by Oracle Corporation was completed on January 27, 2010. Oracle Corporation is the current owner of the official implementation of the Java SE platform.

Up to the Java 9 version, every new version was released either for 2/3/4 years once. Due to this, the Java language was unable to support the latest requirement and latest technologies for developing the project. Hence after the Java9 version, from the Java10 version onwards Oracle corporation has introduced a **_6-Months release cadence_**. It means after every 6 months we will get a new version of Java with the latest features to support new technologies and requirements for the projects. In this 6-Month release cadence, in every new version, we get 5-6 new features. So, learning and using these features in our projects is easy for us.

Among these versions only Java 8, Java 11, Java 17, and Java 21 versions are LTS (Long Term Support) versions, remaining all other versions are supported only up to the release of the next version. You will see most of the Java programmers are working with LTS versions only.

| Java Version (LTS) 🏷️ | Extended Support Until 📅 |
|------------------------|--------------------------|
| **Java SE 8** | December 2030 |
| **Java SE 11** | September 2026 |
| **Java SE 17** | September 2029 |
| **Java SE 21** | September 2031 |

---

## 3. Features of Java

Java came into the market with the main 10 following features.

1. Simple
2. Secure
3. Robust
4. Portable
5. Architectural natural
6. OOP
7. Multithread
8. High performance
9. Distributed
10. Dynamic natural

Let us understand all these features one by one.

### Simple

Java is a very **_simple programming language_** both from learning and developing points of view.

_From the learning point of view_, Java is simple because it has a **_similar syntax_** to C/C++ programming languages. Java omits many features that can make Java language complex, confusing, and unsafe. So, **_Java doesn't have multiple inheritance, structure, union, template, operator overloading, explicit memory allocation_** e.t.c. Java also **_doesn't support pointer_** creation in a program, But Java software has pointers internally.

_From the development point of view_, Java is simple because it provides a rich set of pre-defined libraries (**_API_**). Using these huge pre-defined libraries API we don't need to write more code. Hence development becomes easy for us.

### Secure

Java is secure from the code and data point of view.

- 🔒 Java is secure _from the code point of view_ because Java compiled code doesn't execute directly. Before its execution, the **_Bytecode verifier_** verifies the byte code. If there will be any malicious code or virus then execution will be terminated.
- 🛡️ From the _data point of view_, it is secure because it has **_accessibility modifiers_** and **_encapsulation_**. Using access modifiers (`private`, `public`, `default` and `protected`) we can hide the direct access of the data, available in one program to another program. Or, we can provide data access to another program via a method that is encapsulation.

### Robust

Java is robust, it means reliable. It is strong in type checking and terminating functions safely. Java is a **_strictly typed checking language_**, it does not allow storing high range values in a lesser range variable. For example, if we write `int x = 8.2;` then the compiler will throw an error. The variable `x` is of `int` data type and `8.2` is of the `double` data type. The `double` data type has a greater range value than an `int` data type.

The main features that make it robust are Exception handling, garbage collection, and memory allocation.

Java terminates function safely. It guarantees fail-safe by using an exception handling mechanism. With **exception handling** mechanisms we can stop terminating program execution and save the results. When the execution of a program failed then the program doesn't terminate immediately and we don't lose the value generated in the previous lines.

### Portable

Java programs are **portable**. One Java program written in one computer can run in a different operating system. Java program is portable because its memory size is **fixed** across all operating systems and processors. Hence, we get the same result on all platforms. It can run in any operating system because of its **platform-independency** nature.

But when it came to C/C++ programming language then the size of data types is dependent on the compiler or you can say that the system architecture i.e. 32-bit compiler or 64-bit compiler. The size of data type `int` is 2 bytes in 32-bit architecture and 4 bytes in 64-bit architecture. Another factor on which the size of data type depends is the compiler on which you perform any program i.e. In turbo c/c++ the size of `int` is 2 bytes but in the compiler like code blocks, dev c/c++ e.t.c is 4 bytes.

### Architectural Natural

Java is a **platform-independent** language. Irrespective of other computer hardware, software devices, and operating systems Java programs can run on any computer and in any operating system because of Java virtual machines (JVM).

### OOP

Java is an **object-oriented programming language**. Every program in Java develops around an object by using a concept called class. Every class-based programming language is an object-oriented programming (OOP) language.

### Multithread

Java is a multithreaded programming language. In Java, we can execute **multiple tasks** concurrently. Multithreading is one of the Java features, and it allows concurrent execution of two or more parts of a program for maximum utilization of the CPU.

### High Performance

Due to the multithread nature and JIT compiler, Java programs are executed **fast** and give **high performance**. Java architecture is designed to reduce overheads.

### Distributed

Java is a distributed language. The Java program placed in one computer can be accessed via the network from another computer **directly from** a **program**. Objects on one Java virtual machine (JVM) can execute procedures on a remote JVM. Java can be used to create distributed applications, the EJB (Enterprise Java Beans) and RMI (Remote Method Invocation) are used for this purpose.

### Dynamic Natural

From the memory and functionality point of view, Java is a dynamic programming language. From the memory point of view, Java can allocate multiple copies of memory for the same variable at the execution time by using the `new` Keyword. Also from the functionality point of view, Java is dynamic. Once we develop the project then we can **add more features** and modify existing features dynamically without modifying the source code. It is possible because of the OOP concept, inheritance, and polymorphism.

### Other Features

- 📦 **Byte coded:** Java program not compiled into machine language code like C, C++. Java program is compiled into a special instruction set called byte code.
- 🔄 **Interpreted:** In Java, to convert byte code to machine language code and further to execute this machine language code, inside JVM the interpreter is used. Java program is executed by an interpreter so, Java is called interpreted programming language.
- 🗑️ **Garbage collector:** Java is an automatic memory management programming language. In Java we need not destroy object memory, it is automatically destroyed by a special program called garbage collector.
- 🌐 **Open Source:** Java is open-source software. It is freely available to download. Its source code is available for programmers either for reading or modifying. Any third-party company or programmer can suggest and add more functionalities to the software.

---

## 4. Applications of Java

Java is used from desktop to web applications, scientific supercomputers to gaming consoles, and cell phones to the internet. Java is used in every nook and corner. We use Java for developing different types of applications given below.

1. 🖥️ Desktop applications. Example: Calculator, Trader Console
2. 🌐 Web servers and applications servers
3. 🏦 Enterprise applications. Example: bank applications.
4. 🔗 Interoperable applications. Example: Facebook
5. 📱 Mobile applications. Example: Android apps
6. 🎮 Gaming applications
7. 🤖 Robotics application
8. 💾 Database connections like Oracle database e.t.c.

---

## 5. Prerequisites to Learn Java

There are no prerequisites to learning Java. Anyone can learn Java as the first programming language. There is no need to have knowledge of C/C++ programming languages. If you already know the C/C++ programming language then it will be added advantage for you.

In the Introduction to Java, you got the basics of Java. At KnowProgram, you will get depth knowledge of Java. Just follow all these Java tutorials and practice Java programming examples for logical questions, after that you will have a strong base of Java programming language. To make learning Java programming easy we made a note of important topics, You can get the Java note and start learning Java: **Get Java Note**

And then you can easily learn Java technologies like JDBC (Java Database Connectivity), Servlet, and JSP (for developing web/enterprise applications), Frameworks like Spring, Hibernate, and Web services.

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!
