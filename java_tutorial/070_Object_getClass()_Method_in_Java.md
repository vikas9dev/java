# Object getClass() Method in Java

**Object getClass() Method in Java** | Retrieving runtime class information using `java.lang.Object` class

- [Get Class Name in Java](#get-class-name-in-java)
- [Using getClass() Method in Java to Get Class Information](#using-getclass-method-in-java-to-get-class-information)
- [Different Ways to Get Runtime Class Object in Java](#different-ways-to-get-runtime-class-object-in-java)

---

## 1. Object getClass() Method

We can use the `getClass()` method of [java.lang.Object class](069_Object_Class_in_Java.md) to get the runtime class definition of a runtime class object.

**Method signature:**

```java
public final native Class<?> getClass()
```

🏷️ **Return value:** The `Class` object that represents the runtime class of this object.

Let us first understand what is runtime class and the object of a runtime class. How it is related to the `getClass()` method in Java.

- 🏗️ **Runtime class:** The class that is loaded into JVM at execution time is called the runtime class.
- 📦 **Runtime class object:** Every class bytecode is stored using `java.lang.Class` object. This `java.lang.Class` object is called the runtime class object.

After loading every `.class` file, JVM creates one object of `java.lang.Class` type in the heap area. We can use this object to get class-level information like class name, method information, constructor information, etc. The `getClass()` method of the `Object` class is used very frequently in the reflection API.

Assume there is a class called `A`. Using the `getClass()` method we can get the runtime class object of the `A` class.

**Basic usage:**

```java
A a1 = new A();
Class cls = a1.getClass();
```

**Example on pre-defined classes:**

```java
import java.util.ArrayList;

public class Test {
  public static void main(String[] args) {

    String str = new String();
    System.out.println("Class of str: " + str.getClass());

    ArrayList al = new ArrayList();
    System.out.println("Class of al: " + al.getClass());
  }
}
```

📤 **Output:**

```
Class of str: class java.lang.String
Class of al: class java.util.ArrayList
```

**Example on custom classes:**

```java
class A { }

public class Test {
  public static void main(String[] args) {

    Test t1 = new Test();
    System.out.println("Class of t1: " + t1.getClass());

    A a1 = new A();
    System.out.println("Class of a1: " + a1.getClass());
  }
}
```

📤 **Output:**

```
Class of t1: class Test
Class of a1: class A
```

---

## 2. Get Class Name in Java

To get the name of a Java class, call the `getName()` method on the runtime class object. This `getName()` method is defined in `java.lang.Class` class.

**Method signature:**

```java
public String getName()
```

Assume there is a class called `A`. Below code shows retrieving the class name of runtime class object using the `getClass()` method in Java:

**Step-by-step approach:**

```java
// create object of class
A a1 = new A();

// get runtime object
Class cls = a1.getClass();

// get class name
String name = cls.getName();
```

The above lines of code can be written in a single line as follows:

**Single-line approach using getClass().getName():**

```java
String name = a1.getClass().getName();
```

**Java program to get the class name:**

```java
class A { }

class Test {
  public static void main(String[] args) {

    Test t1 = new Test();
    String classname = t1.getClass().getName();
    System.out.println(classname);

    A a1 = new A();
    classname = a1.getClass().getName();
    System.out.println(classname);
  }
}
```

📤 **Output:**

```
Test
A
```

---

## 3. Using getClass() Method in Java to Get Class Information

We can use the runtime class objects to get more information on the class. Some important methods are:

- 🔍 `getFields()` — Returns all public fields
- 🏗️ `getConstructors()` — Returns all public constructors
- 🛠️ `getMethods()` — Returns all public methods

📝 **Note:** On calling the above methods on the runtime class object, they will give information of the **current class**, and all its **superclass**.

**Java program to display all methods of a class:**

```java
import java.lang.reflect.*;
class Test {

  // methods
  public void m1(){}
  public void m2(){}
  public void m3(){}

  public static void main(String[] args) {

    Test t1 = new Test();
    Class cls = t1.getClass();

    // display class name of runtime class object
    String classname = cls.getName();
    System.out.println("Class Name: "+ classname);

    // display all methods of this Class object
    Method[] methods = cls.getMethods();
    System.out.println("Methods: ");
    for(Method m : methods) {
      System.out.print(m.getName() + " ");
    }
  }
}
```

📤 **Output:**

```
Class Name: Test
Methods:
m3 main m2 m1 wait wait wait equals toString hashCode getClass notify notifyAll
```

`Test` class is a direct child class of `java.lang.Object` class therefore methods of `Object` class are also available to the child class.

💡 **Tip:** Another simple way to display all methods of a class is by using [javap tool](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/javap.html). The `javap` is also a tool like `javac` and `java`. Open cmd and type `javap <classname>`.

**Using javap tool:**

```bash
> javap Test
```

📤 **Output:**

```
Compiled from "Test.java"
class Test {
  Test();
  public void m1();
  public void m2();
  public void m3();
  public static void main(java.lang.String[]);
}
```

---

## 4. Different Ways to Get Runtime Class Object in Java

In Java, the `getClass()` method is not the only way to get the runtime class object. Different ways to get the object of a given class are:

| Approach 🏷️ | Syntax 🛠️ |
|-------------|-----------|
| **Using `.class`** | `Class cls = classname.class;` |
| **Using `Class.forName()`** | `Class cls = Class.forName(classname);` |
| **Using `getClass()`** | `Class cls = obj.getClass();` |

Let us take a `Test` class for demonstration purposes:

**Test class:**

```java
public class Test {
  public static int i = m1();

  static {
    System.out.println("Test class: Static block executed");
  }

  public static void main(String[] args) {
    System.out.println("Test class: main method executed");
  }

  public static int m1() {
    System.out.println("Test class: Static variable initialized");
    return 5;
  }
}
```

### 1. Using classname.class

```java
// classname.class demonstration
public class Example1 {
  public static void main(String[] args) {
    Class<Test> t1 = Test.class;
    System.out.println("Name of class: " + t1.getName());
  }
}
```

📤 **Output:**

```
Name of class: Test
```

📝 **Note:** In this approach, using `Test.class` the Test class is loaded and stored in the JVM, and the runtime class object is returned. The Test class static variables are not initialized, static block and the main method of the Test class are also not executed.

### 2. Using Class.forName()

```java
// Class.forName() demonstration
public class Example2 {
  public static void main(String[] args)
      throws ClassNotFoundException {
    Class<?> t1 = Class.forName("Test");
    System.out.println("Name of class: "
                      + t1.getName());
  }
}
```

📤 **Output:**

```
Test class: Static variable initialized
Test class: Static block executed
Name of class: Test
```

📝 **Note:** In this approach, `Class.forName("Test")` loads the Test class, creates `java.lang.Class` object, initializes static variables, and executes static blocks. Finally, the runtime class object is returned. The main method will not be executed.

### 3. Using getClass()

```java
// getClass() demonstration
public class Example3 {
  public static void main(String[] args){

    // creating object of class
    System.out.println("Creating an object of Test class");
    Test t1 = new Test();
    System.out.println("Test class object is created");

    // get class reference
    Class cls = t1.getClass();
    System.out.println("getClass() is called");

    // get name of class
    System.out.println("Name of class: " + cls.getName());
  }
}
```

📤 **Output:**

```
Creating an object of Test class
Test class: Static variable initialized
Test class: Static block executed
Test class object is created
getClass() is called
Name of class: Test
```

📝 **Note:** In this approach, the already created `Class` object reference is returned because the Test class has already loaded due to its object creation.

> 🔑 **Key Point:** Whenever the constructor is called for the first time (assuming the class was not used before that statement) then the class is loaded, static variables are initialized, and static blocks are executed. But `getClass()` is not performing these operations.
