# String Data Type in Java

**String Data Type in Java** | Understanding the String referenced data type, string literals, and escape sequences in Java.

- [Java String Literal](#java-string-literal)
- [Can We Use the User-Defined Class Name as String?](#can-we-use-the-user-defined-class-name-as-string)
- [Examples of String](#examples-of-string)

---

The string is a referenced data type in Java and it is also a predefined class created by SUN. It is available in `java.lang` package in `java.base` module.

The string data type in Java is used for representing a sequence of characters placed in double quotation marks (`""`). It means for storing a sequence of characters as one group we must create a `String` class type referenced variable.

| Property 🏷️ | Value 📋 |
|-------------|---------|
| **Range** | No limitation on size. We can store any number of characters. |
| **Default value** | `null` |
| **Size** | 2 * number of characters |

---

## 1. Java String Literal

**Any sequence of characters in the double quote is treated as a string literal.**

```java
String s1 = "KnowProgram";
// valid, it is a string

String s2 = KnowProgram;
// invalid, it is not a string
// it must be enclosed in double quotation
```

If we use a sequence of characters directly in a program compiler will not treat it as a string and it will throw an error. So, to tell compiler and JVM to treat a sequence of characters as a string we must place them inside double quotation mark (`""`).

Inside double quotation mark (`""`) we can write 0 to n characters. So, the empty string is also allowed.

```java
String s3 = ""; // valid
String s4 = " "; // valid, white space
String s5 = "Bike Numer 9854"; // valid
```

---

## 2. Can We Use the User-Defined Class Name as String?

We are allowed to create our own class with the name `String`. If we create our own class with name `String` then to access pre-defined `String` class we must use the package name also.

**Problem demonstration:**

```java
//Test.java
 class String{}

 class Program{
     public static void main(String[] args){
         System.out.println("Hello, World!");
     }
 }
```

**Compilation and execution:**

```bash
>javac Test.java
It creates two files String.class and Program.class

>java Program
error: Main method not found in class Program
```

**Why this error comes?**

To find this answer we should know how compilation and execution are done in `Test.java` file. The compilation is done successfully because of no syntax and grammar mistakes. Execution starts in `Program` class due to the command `java Program`.

The first line is `class Program`, the `class` is a keyword and the `Program` is an identifier so no logical error is there. Now, JVM goes for second-line `public static void main(String[] args)`. The `public` and `static` are a keyword, the `void` is return type, `main` is an identifier. Finally, JVM searches for `String`.

JVM always searches for any identifier, first in the current main method, then in the current class, after that in the current Java file, then-current folder, if not found then it goes to Java software file (`java.lang`).

Here JVM found identifier `String` as a class in the current Java file. So, the second line is not the main method. The syntax of the second line looks like the main method but it is not actually the main method. Here, the `String` class is user-defined. So, JVM stops execution and gives an exception that the main method not found.

> 💡 **Tip:** This error comes because in this `Program` class main method with the parameter is not `java.lang.String`, it is our user-defined class `String`. To execute `Program` class we must use `String` class name with package name as [`java.lang.String`](https://docs.oracle.com/javase/7/docs/api/java/lang/String.html).

**Solution:**

```java
//Test.java
 class String{}

 class Program{
     public static void main(java.lang.String[] args){
         System.out.println("Hello, World!");
     }
 }
```

**Compilation and execution:**

```bash
>javac Test.java
>java Program
Hello, World!
```

---

## 3. Examples of String

If we want to display a single quote or double quote, we can not directly use a single quote in a single quote and double quote in double quote. We will get a compile-time error.

**Error demonstration:**

```java
class Test{
     public static void main(String[] args) {

         System.out.println("""");
         // error: ')' expected

         System.out.println(''');
         // error: empty character literal
     }
 }
```

In this case, we must use the escape sequence character as shown below:

**Using escape sequences:**

```java
class Test{
     public static void main(String[] args) {
         System.out.println('\'');
         System.out.println("\'KnowProgram\'");
         System.out.println("\"\"");
         System.out.println("\"KnowProgram\"");
     }
 }
```

📤 **Output:**

```
'
'KnowProgram'
""
"KnowProgram"
```
