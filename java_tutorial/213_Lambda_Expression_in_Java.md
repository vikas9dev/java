# Lambda Expression in Java

**Lambda Expression in Java** | Lambda ( λ ) in calculus is a big change in the mathematical world which has been introduced in 1930. Because of the benefits of Lambda calculus slowly these concepts started using in the programming world.

- [What is Lambda Expression In Java?](#what-is-lambda-expression-in-java)
- [How to Write Lambda Expressions In Java?](#how-to-write-lambda-expressions-in-java)
- [Points To Consider While Writing Lambda Expression in Java](#points-to-consider-while-writing-lambda-expression-in-java)
- [Invoking Lambda Expression In Java by Using Functional Interface](#invoking-lambda-expression-in-java-by-using-functional-interface)
- [Lambda Expression in Java with Collection](#lambda-expression-in-java-with-collection)
- [Sorting List of Custom Class Objects with Lambda Expression In Java](#sorting-list-of-custom-class-objects-with-lambda-expression-in-java)
- [Advantages of Lambda Expression in Java](#advantages-of-lambda-expression-in-java)

---

The Main Objective of Lambda Expression is:

- ⚡ To bring benefits of functional programming into Java.
- 📖 To write more readable, maintainable & concise code.
- 🔧 To use APIs very easily and effectively.
- 🔄 To enable parallel processing.

---

## 1. What is Lambda Expression In Java?

Lambda Expression is just an anonymous (nameless) function. That means the function which doesn't have the name, return type, and access modifiers. Lambda Expression is also known as anonymous functions or closures.

Lambda is an anonymous function with the following specialty:

- 🚫 Not having a name.
- 🚫 Not having modifiers.
- 🚫 Not having any return type.

---

## 2. How to Write Lambda Expressions In Java?

Let us start with simple programs to learn how to write lambda expressions in Java.

**Example-1: Write a lambda expression to print "Hello World!"**

A simple Java method can be written as:

**Normal method:**

```java
public void m1() {
   System.out.println("Hello World!");
}
```

In lambda expression, it can be written as:

**Lambda expression (full form):**

```java
() -> {
   System.out.println("Hello World!");
}
```

Or, it can be written as:

**Lambda expression (one-liner with braces):**

```java
() -> { System.out.println("Hello World!"); }
```

Or, it can be further simplified as:

**Lambda expression (simplified):**

```java
() -> System.out.println("Hello World!");
```

**Example-2: Write lambda expression to find the sum of 2 Numbers.**

**Normal method:**

```java
public void add(int a, int b) {
   System.out.println(a+b);
}
```

If the type of the parameter can be decided by the compiler automatically based on the context then we can remove types also. In lambda expression, it can be written as follows, and can be further simplified:

**Lambda with types:**

```java
(int a, int b) -> System.out.println(a+b);
```

**Lambda without types (type inference):**

```java
(a,b) -> System.out.println(a+b);
```

**Example-3: Write lambda expression to find the String length.**

**Normal method:**

```java
public String str(String str) {
   return str.length;
}
```

Using lambda expression it can be written as:

**Lambda with type:**

```java
(String str) -> return str.length;
```

**Lambda simplified:**

```java
(str) -> str.length;
```

---

## 3. Points To Consider While Writing Lambda Expression in Java

**1) A lambda expression can have zero or more number of parameters (arguments).**

- `() -> System.out.println("Hello World!"); // No Parameter`
- `(int a) -> System.out.println(a); // 1 Parameter`
- `(int a, int b) -> return a+b; // 2 Parameters`

**2)** Usually we specify the type of parameter. If the compiler expects the type based on the context then we can remove type (Type Inference) i.e. **we don't have to write the type of parameter**.

**With types:**

```java
(int a, int b) -> System.out.println(a+b);
```

It can be written as:

**Without types:**

```java
(a, b) -> System.out.println(a+b);
```

**3) If multiple parameters are present then these parameters should be separated with a comma (`,`).**

**4) If the zero number of parameters is available then we have to use an empty parameter [ like `()`].**

- `() -> System.out.println("Hello World!");`

**5) If only one parameter is available** and if the compiler can expect the type **then we can remove the type and parenthesis also.**

- `(int a) -> System.out.println(a);`
- `(a)-> System.out.println(a);`
- `a -> System.out.println(a);`

**6)** Similar to the method body, the lambda expression body also can contain multiple statements. If more than one statement is present then we have to enclose it inside within curly braces. **If one statement is present then curly braces are optional**.

**7) No need to use the "return" keyword while returning some value.**

- `str -> return str.length;`
- `str -> str.length;`

**8)** Once we write a lambda expression we can call that expression just like a method, for this **functional interfaces are required**.

---

## 4. Invoking Lambda Expression In Java by Using Functional Interface

We can call lambda expression through a functional interface therefore you must have knowledge about the functional interface. See more: [Functional Interface In Java](212_Functional_Interface_In_Java.md)

**Example-1: Print the "Hello World!" message using the lambda expression.**

First, let us see how it could be written without using lambda expression and through the functional interface.

**Without Lambda Expression:**

```java
// Without Lambda Expression
interface Interf {
   public void m1();
}

class Demo implements Interf {
   public void m1() {
      System.out.println("Hello World!");
   }
}

public class Test {
   public static void main(String[] args) {
      Interf i = new Demo();
      i.m1();
   }
}
```

📤 **Output:**

```
Hello World!
```

**With Lambda Expression:**

```java
// with Lambda Expression
@FunctionalInterface
interface Interf {
   public void m1();
}

public class Test {
   public static void main(String[] args) {
      Interf i = () -> System.out.println("Hello World!");
      i.m1();
   }
}
```

**Example-2: Find the sum of 2 numbers using lambda expression and functional interface.**

**Without lambda expression:**

```java
interface Interf {
   public void sum(int a,int b);
}

class Demo implements Interf {
   public void sum(int a,int b) {
      System.out.println("The sum: " + (a+b));
   }
}

public class Test {
   public static void main(String[] args) {
      Interf i = new Demo();
      i.sum(20, 5);
      i.sum(30, 40);
      i.sum(50, 60);
   }
}
```

📤 **Output:**

```
The sum: 25
The sum: 70
The sum: 110
```

**With lambda expression:**

```java
interface Interf {
   public void sum(int a,int b);
}

public class Test {
   public static void main(String[] args) {
      Interf i = (a, b) -> System.out.println("The sum: " + (a+b));
      i.sum(20, 5);
      i.sum(30, 40);
      i.sum(50, 60);
   }
}
```

**Example-3: Finding square root value using lambda expression and functional interface.**

**Without lambda expression:**

```java
interface Interf {
   public int square(int x);
}

class Demo implements Interf {
    public int square(int x) {
      return x*x;
   }
}

public class Test {
   public static void main(String[] args) {
      Interf i = new Demo();
      System.out.println(i.square(20));
      System.out.println(i.square(30));
      System.out.println(i.square(40));
   }
}
```

📤 **Output:**

```
400
900
1600
```

**With Lambda Expression:**

```java
interface Interf {
   public int square(int x);
}

public class Test {
   public static void main(String[] args) {
      Interf i = x -> x*x;
      System.out.println(i.square(20));
      System.out.println(i.square(30));
      System.out.println(i.square(40));
   }
}
```

**Example-4: Creating and starting a new Thread using the lambda expression.** The Runnable interface contains only one abstract method: the `run()` method, therefore Runnable is a functional interface.

**Without lambda expression:**

```java
class MyRunnable implements Runnable {
   @Override
   public void run() {
      for(int i=0; i<5; i++) {
         System.out.println("Child thread");
      }
   }
}

public class Test {
   public static void main(String[] args) {
      Runnable r = new MyRunnable();
      Thread t = new Thread(r);
      t.start();
      for(int i=0; i<5; i++) {
         System.out.println("Main Thread");
      }
   }
}
```

**With lambda expression:**

```java
public class Test {
   public static void main(String[] args) {
      Runnable r = () -> {
         for(int i=0; i<5; i++) {
            System.out.println("Child thread");
         }
      };

      Thread t = new Thread(r);
      t.start();

      for(int i=0; i<5; i++) {
         System.out.println("Main Thread");
      }
   }
}
```

> 💡 **Tip:** In examples 1, 2, and 3 you can notice that first we are creating a functional interface and invoking the lambda expression. Since you are a beginner to the lambda expression, therefore, we have defined a functional interface manually to help you understand better. But defining a functional interface is not required. The `java.util.function` package already contains many functional interfaces like Predicate, Function, Consumer, Supplier, and e.t.c. Using those pre-defined functional interfaces we can directly invoke lambda expression.

**Finding square root value using `Function` functional interface:**

Function interface of `java.util.function` package contains only one abstract method: `apply()` method.

```java
import java.util.function.Function;

public class Test {
    public static void main(String[] args) {
        Function<Integer, Integer> func = n -> n * n;
        System.out.println(func.apply(5));
        System.out.println(func.apply(-3));
    }
}
```

📤 **Output:**

```
25
9
```

---

## 5. Lambda Expression in Java with Collection

### Sort List Using Lambda Expression

List (ArrayList, LinkedList, Vector, or Stack) never talks about sorting order. If we want to sort for the list then we should use the Collections class `sort()` method. The `Collections.sort(list)` is meant for the default natural sorting order. For example:

- 🔤 String objects: Alphabetical Order
- 🔢 Numbers: Ascending order

**List program for default natural sorting order:**

```java
import java.util.ArrayList;
import java.util.Collections;
public class Test {
   public static void main(String[] args) {
      ArrayList<Integer> al = new ArrayList<Integer>();
      al.add(10);
      al.add(0);
      al.add(5);
      al.add(15);
      al.add(20);
      System.out.println("Before Sorting: " + al);
      Collections.sort(al);
      System.out.println("After Sorting: " + al);
   }
}
```

📤 **Output:**

```
Before Sorting: [10, 0, 5, 15, 20]
After Sorting: [0, 5, 10, 15, 20]
```

Instead of the default natural sorting order if we want customized sorting order then we should go for the Comparator interface. The comparator interface contains only one abstract method: `compare()`. Hence it is a **Functional interface**. Method declaration: **`public int compare(obj1, obj2)`**. It returns:

- ➖ -ve if obj1 < obj2
- ➕ +ve if obj1 > obj2
- 0️⃣ 0 if obj1 = obj2

`Collections.sort(list, Comparator)` is meant for customized sorting orders.

**List program for customized sorting order (descending order) without lambda expression:**

Here we have to define a class implementing from the Comparator interface.

**MyComparator class:**

```java
import java.util.Comparator;
public class MyComparator implements Comparator<Integer> {
   @Override
   public int compare(Integer i1, Integer i2) {
      if(i1 > i2) return -1;
      else if(i1 < i2) return 1;
      else return 0;
   }
}
```

Instead of an if-else statement, we can also use a ternary operator:

**MyComparator with ternary:**

```java
import java.util.Comparator;
public class MyComparator implements Comparator<Integer> {
   @Override
   public int compare(Integer i1, Integer i2) {
      return (i1 > i2) ? -1 : (i1 < i2) ? 1 : 0;
   }
}
```

**Test class with custom sorting:**

```java
import java.util.ArrayList;
import java.util.Collections;
public class Test {
   public static void main(String[] args) {
      ArrayList<Integer> al = new ArrayList<Integer>();
      al.add(10);
      al.add(0);
      al.add(5);
      al.add(15);
      al.add(20);
      System.out.println("Before Sorting: " + al);
      Collections.sort(al, new MyComparator());
      System.out.println("After Sorting: " + al);
   }
}
```

📤 **Output:**

```
Before Sorting: [10, 0, 5, 15, 20]
After Sorting: [20, 15, 10, 5, 0]
```

Since Comparator is a functional interface therefore we can directly use lambda expression instead of creating a separate class to implement the Comparator interface.

**List program for customized sorting order (descending order) with the lambda expression:**

```java
import java.util.ArrayList;
import java.util.Collections;
public class Test {
   public static void main(String[] args) {
      ArrayList<Integer> al = new ArrayList<Integer>();
      al.add(10);
      al.add(0);
      al.add(5);
      al.add(15);
      al.add(20);
      System.out.println("Before Sorting: " + al);

      // use lambda expression for compare()
      Collections.sort(al,
            (i1, i2) -> (i1 > i2) ? -1 : (i1 < i2) ? 1 : 0);

      System.out.println("After Sorting: " + al);
   }
}
```

📤 **Output:**

```
Before Sorting: [10, 0, 5, 15, 20]
After Sorting: [20, 15, 10, 5, 0]
```

### Sort Set Using Lambda Expression

In the case of Set, if we want Sorting order then we should go for TreeSet.

1. **`TreeSet t = new TreeSet();`** - This TreeSet object meant for default natural sorting order
2. **`TreeSet t = new TreeSet(Comparator c);`** - This TreeSet object is meant for Customized Sorting Order

**TreeSet program for default natural sorting order:**

```java
import java.util.TreeSet;
public class Test {
   public static void main(String[] args) {
      TreeSet<Integer> ts = new TreeSet<Integer>();
      ts.add(10);
      ts.add(0);
      ts.add(5);
      ts.add(15);
      ts.add(20);
      System.out.println(ts);
   }
}
```

📤 **Output:**

```
[0, 5, 10, 15, 20]
```

**TreeSet program for customized sorting order (descending order) without lambda expression:**

**MyComparator class:**

```java
import java.util.Comparator;
public class MyComparator implements Comparator<Integer> {
   @Override
   public int compare(Integer i1, Integer i2) {
      return (i1 > i2) ? -1 : (i1 < i2) ? 1 : 0;
   }
}
```

**Test class:**

```java
import java.util.TreeSet;
public class Test {
   public static void main(String[] args) {
      TreeSet<Integer> ts =
          new TreeSet<Integer>(new MyComparator());
      ts.add(10);
      ts.add(0);
      ts.add(5);
      ts.add(15);
      ts.add(20);
      System.out.println(ts);
   }
}
```

📤 **Output:**

```
[20, 15, 10, 5, 0]
```

**TreeSet program for customized sorting order (Descending Order) with a lambda expression:**

```java
import java.util.TreeSet;
public class Test {
   public static void main(String[] args) {
      TreeSet<Integer> ts = new TreeSet<Integer>(
            (i1, i2) -> (i1 > i2) ? -1 : (i1 < i2) ? 1 : 0);
      ts.add(10);
      ts.add(0);
      ts.add(5);
      ts.add(15);
      ts.add(20);
      System.out.println(ts);
   }
}
```

📤 **Output:**

```
[20, 15, 10, 5, 0]
```

### Sort Map Using Lambda Expression

In the case of Map, if we want the default natural sorting order of keys then we should go for TreeMap. (Sorting will be always based on the key, but not on the value).

1. **`TreeMap m = new TreeMap();`** - This TreeMap object meant for the default natural sorting order of keys
2. **`TreeMap t = new TreeMap(Comparator c);`** - This TreeMap object is meant for Customized Sorting Order of keys

**TreeMap program for default natural sorting order:**

```java
import java.util.TreeMap;
public class Test {
   public static void main(String[] args) {
      TreeMap<Integer, String> tm = new TreeMap<Integer, String>();
      tm.put(100, "Durga");
      tm.put(600, "Sanjay");
      tm.put(300, "Bunny");
      tm.put(700, "Vinny");
      tm.put(600, "Pinny");
      System.out.println(tm);
   }
}
```

📤 **Output:**

```
{100=Durga, 300=Bunny, 600=Pinny, 700=Vinny}
```

**TreeMap program for customized sorting order (descending order) with a lambda expression:**

```java
import java.util.TreeMap;
public class Test {
   public static void main(String[] args) {
      TreeMap<Integer, String> tm = new TreeMap<Integer, String>(
            (i1, i2) -> (i1 > i2) ? -1 : (i1 < i2) ? 1 : 0);
      tm.put(100, "Durga");
      tm.put(600, "Sanjay");
      tm.put(300, "Bunny");
      tm.put(700, "Vinny");
      tm.put(600, "Pinny");
      System.out.println(tm);
   }
}
```

📤 **Output:**

```
{100=Durga, 300=Bunny, 600=Pinny, 700=Vinny}
```

---

## 6. Sorting List of Custom Class Objects with Lambda Expression In Java

We have an Employee class with fields `eno` and `ename`. We want to sort employees based on eno in descending order. Use lambda expression for this purpose. Use a [List](195_List_Interface_in_Java.md) to store employees.

To solve this problem we have to use the Comparator interface. Since it is a functional interface therefore we can use the lambda expression.

**Employee class:**

```java
public class Employee {

    private Integer eno;
    private String  ename;

    public Employee(Integer eno, String ename) {
        this.eno = eno;
        this.ename = ename;
    }

    public Integer getEno() {
        return eno;
    }

    public void setEno(Integer eno) {
        this.eno = eno;
    }

    public String getEname() {
        return ename;
    }

    public void setEname(String ename) {
        this.ename = ename;
    }

    @Override
    public String toString() {
        return eno + " - " + ename;
    }
}
```

**Test class - sort by eno descending:**

```java
import java.util.ArrayList;
import java.util.Collections;

public class Test {
    public static void main(String[] args) {
        ArrayList<Employee> al = new ArrayList<Employee>();
        al.add(new Employee(100, "William"));
        al.add(new Employee(200, "Rocket"));
        al.add(new Employee(150, "Sophia"));
        al.add(new Employee(50, "John"));
        al.add(new Employee(400, "Ameila"));

        System.out.println("Before sorting: " + al);
        Collections.sort(al,
                (e1, e2) -> (e1.getEno() > e2.getEno()) ?
                        -1 : (e1.getEno() < e2.getEno()) ? 1 : 0);
        System.out.println("After sorting: " + al);
    }
}
```

📤 **Output:**

```
Before sorting: [100 - William, 200 - Rocket, 150 - Sophia, 50 - John, 400 - Ameila]
After sorting: [400 - Ameila, 200 - Rocket, 150 - Sophia, 100 - William, 50 - John]
```

**Example-2: Sort employees based on descending order of the name, if two employees' names are the same then sort them based on their employee number in ascending order.**

```java
import java.util.ArrayList;
import java.util.Collections;

public class Test {
    public static void main(String[] args) {
        ArrayList<Employee> al = new ArrayList<Employee>();
        al.add(new Employee(100, "William"));
        al.add(new Employee(200, "William"));
        al.add(new Employee(150, "Sophia"));
        al.add(new Employee(50, "Ameila"));
        al.add(new Employee(400, "Ameila"));

        System.out.println("Before sorting: " + al);
        Collections.sort(al,
                (e1, e2) -> (e1.getEname().compareTo(e2.getEname()) > 0) ?
                        -1 : (e1.getEname().compareTo(e2.getEname()) < 0) ?
                         1 : (
                                 (e1.getEno() > e2.getEno()) ?
                                  1 : (e1.getEno() < e2.getEno()) ?
                                  -1 : 0
                             )
                         );
        System.out.println("After sorting: " + al);
    }
}
```

📤 **Output:**

```
Before sorting: [100 - William, 200 - William, 150 - Sophia, 50 - Ameila, 400 - Ameila]
After sorting: [100 - William, 200 - William, 150 - Sophia, 50 - Ameila, 400 - Ameila]
```

---

## 7. Advantages of Lambda Expression in Java

The following are the main advantages of Lambda Expression in Java:

- 📖 We can reduce the length of the code so that the readability of the code will be improved.
- 🧹 We can resolve the complexity of anonymous inner classes.
- 🔄 We can provide Lambda expression in the place of an object.
- ⚡ We can pass a lambda expression as an argument to methods.
