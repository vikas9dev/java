# Object Class toString() Method in Java

**Object Class toString() Method in Java** | Retrieving object information in string form using `java.lang.Object`

- [Override toString() in Java](#override-tostring-in-java)
- [Use of toString Method in Java](#use-of-tostring-method-in-java)
- [Relation Between toString() and hashCode() Methods](#relation-between-tostring-and-hashcode-methods)

---

## 1. Object Class toString() Method

The `java.lang.Object.toString()` method is used to retrieve object information in string form.

**Method signature:**

```java
public String toString()
```

Every class has its own class name, hashcode, and state. In `java.lang.Object` class `toString()` method is implemented for returning the class name and hashcode of the current object in the hexadecimal format as `classname@hashCodeInHexadecimalFormat`. It internally calls getClass() method and [hashCode() method](071_Hashcode_in_Java_–_hashCode()_Method.md).

**The toString() implementation in the Object class:**

```java
public String toString() {
  return getClass().getName() + "@"
         + Integer.toHexString(hashCode());
}
```

**Basic demonstration:**

```java
public class Test {
   public static void main(String[] args) {

      Test t1 = new Test();
      System.out.println(t1);
      System.out.println(t1.toString());

      Test t2 = new Test();
      System.out.println(t2);
   }
}
```

📤 **Output:**

```
Test@d716361
Test@d716361
Test@6ff3c5b5
```

Whenever we are trying to print an Object reference then internally `toString()` method will be called. Since the `toString()` method is not defined in the `Test` class, so the compiler will search for it in the superclass. Directly or indirectly every Java class is a subclass of `java.lang.Object` class. Therefore, the `toString()` method will be executed from the `Object` class and display the string `classname@hashCodeInHexadecimalFormat`.

💡 **Tip:** Note that the below two lines give the same result. Whenever we call `print()`/`println()` method to display object then internally it calls `toString()` method.

```java
System.out.println(t1);             // internally toString() is called
System.out.println(t1.toString());
```

**Another example with Student class:**

```java
class Student {

  int id;
  String name;
  String course;

  public Student(int id, String name, String course) {
    this.id = id;
    this.name = name;
    this.course = course;
  }
}

public class Test {
  public static void main(String[] args) {

    Student s1 = new Student(100, "Emma", "Java");
    System.out.println(s1);

    Student s2 = new Student(101, "Noah", "Python");
    System.out.println(s2);
  }
}
```

📤 **Output:**

```
Student@ee7d9f1
Student@1963006a
```

Java toString() Quiz

---

## 2. Override toString() in Java

The above outputs are not meaningful messages. It should display Student object data, rather than its references. If we want to return the object's state from this method we must override it in the subclass. Based on our requirement we can override the `toString()` method in our class to provide our own representation.

**Simple override example:**

```java
public class Test {

   @Override
   public String toString() {
      return "Test";
   }

   public static void main(String[] args) {

      Test t1 = new Test();
      System.out.println(t1);
      System.out.println(t1.toString());

      Test t2 = new Test();
      System.out.println(t2);
   }
}
```

📤 **Output:**

```
Test
Test
Test
```

Now, in the `Test` class `toString()` method is overridden and returns the `"Test"` string. Therefore whenever we try to print object reference then it is executed from the `Test` class and returns the `"Test"` String.

**Student class with meaningful toString():**

```java
class Student {
  int id;
  String name;
  String course;

  public Student(int id, String name, String course) {
    this.id = id;
    this.name = name;
    this.course = course;
  }

  @Override
  public String toString() {
    return "Student [id=" + id +
               ", name=" + name +
               ", course=" + course + "]";
  }
}

public class Test {
  public static void main(String[] args) {
    Student s1 = new Student(100, "Emma", "Java");
    System.out.println(s1);

    Student s2 = new Student(101, "Noah", "Python");
    System.out.println(s2);
  }
}
```

📤 **Output:**

```
Student [id=100, name=Emma, course=Java]
Student [id=101, name=Noah, course=Python]
```

In the `Student` class `toString()` method is overridden and returns the state or data of the object. Therefore whenever we are trying to print an object reference then it will display the id and name of the `Student` object.

---

## 3. Use of toString Method in Java

**In all [collection classes](192_Java_Collection_Framework_Overview.md), all wrapper classes, [Arrays](033_Arrays_Class_Java_With_Examples.md), `String`, `StringBuffer`, and `StringBuilder` classes the `toString()` method is overridden to display the content.** That's why while using these classes we are getting object data rather than the reference of the object.

**Demonstration with built-in classes:**

```java
import java.util.ArrayList;
import java.util.Arrays;
public class Test {
   public static void main(String[] args) {

      // String class
      String s = "KnowProgram";
      System.out.println(s);

      // Wrapper classes
      Integer io = Integer.valueOf(10);
      System.out.println(io);
      Double d = Double.valueOf(19.5);
      System.out.println(d);

      // ArrayList class
      ArrayList<Character> al = new ArrayList<Character>();
      al.add('K');
      al.add('P');
      System.out.println(al);

      // Arrays
      int arr[] = new int[]{1, 2, 3, 4, 5};
      System.out.println(Arrays.toString(arr));
   }
}
```

📤 **Output:**

```
KnowProgram
10
19.5
[K, P]
[1, 2, 3, 4, 5]
```

See More: Arrays.toString() in Java

---

## 4. Relation Between toString() and hashCode() Methods

When the `toString()` method is not overridden in the class then the `toString()` method is executed from the [Java Object class](069_Object_Class_in_Java.md). **Object class `toString()` method internally calls `hashCode()` method.**

But if we are overriding the `toString()` method then it may or may not call `hashCode()`, it completely depends on the implementation logic.

### Case 1: Both toString() and hashCode() methods are not overridden

```java
class A {

  int x;

  A(int x){
    this.x = x;
  }
}

class Test {
  public static void main(String[] args) {
    A a1 = new A(18);
    System.out.println(a1);
  }
}
```

📤 **Output:**

```
A@6ff3c5b5
```

📝 **Note:** Here `toString()` and `hashCode()` methods are executed from `Object` class and returns `className@hashCodeInHexadecimalFormat`.

### Case 2: Only hashCode() method is overridden

```java
class A {

  int x;

  A(int x){
    this.x = x;
  }

  @Override
  public int hashCode(){
    return 100;
  }
}

class Test {
  public static void main(String[] args) {
    A a1 = new A(18);
    System.out.println(a1);
  }
}
```

📤 **Output:**

```
A@64
```

Whenever we try to print object reference then the `toString()` method is called. Since `toString()` is not overridden in the `A` class so it will be called from the `Object` class. The `toString()` of the `Object` class internally calls the `hashCode()` method, but the `hashCode()` method is overridden in class `A`. So, the `hashCode()` method will be executed from the `A` class.

💡 **Tip:** The value returned by the `hashCode()` method is in integer format which will be converted to hexadecimal format by the `toString()` method of the `Object` class. In our example, `hashCode()` returned `100`. The hexadecimal format of integer value 100 is `64`. Hence we get `A@64`.

### Case 3: The hashCode() and toString() method, both are overridden

```java
class A {

  int x;

  A(int x){
    this.x = x;
  }

  @Override
  public int hashCode(){
    return 9;
  }

  @Override
  public String toString() {
    return "" + x;
  }
}

class Test {
  public static void main(String[] args) {
    A a1 = new A(18);
    System.out.println(a1);
  }
}
```

📤 **Output:**

```
18
```

Since `toString()` method is overridden and its implementation logic is not calling any other methods, it directly returns the value in string format. Hence `hashCode()` method won't get any chance to execute.

### Case 4: Only toString() is overridden

It is similar to the previous case. When `toString()` is overridden then it may or may not call `hashCode()`, it depends on its implementation logic.
