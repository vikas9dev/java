# String toString() Java

**String toString() Java** | Here, we will discuss the `toString()` method of the [Java String class](097_String_Class_Methods_In_Java.md). It is the built-in method that is used to return the string itself. While using this method there is no actual conversion that takes place -- it just returns the string without any changes, which is called implicitly.

- [String toString() Method in Java - Example](#string-tostring-method-in-java--example)
- [toString() with Custom Objects](#tostring-with-custom-objects)

---

## 1. String toString() Method in Java - Example

Examples for the `toString()` method:

- 📖 `String: "Hii"` --> After `toString()`: `"Hii"`
- 📖 `int: 0090` --> After `Integer.toString()`: `"0090"`

| Detail 📋 | Description 📝 |
|-----------|---------------|
| **Method Signature** | `public String toString()` |
| **Parameters** | None |
| **Return Type** | `String` |
| **Returns** | The string itself |

**Basic `toString()` example:**

```java
public class Main {
   public static void main(String args[]) {
      String string = "An apple a day keeps a doctor away";
      System.out.print("Output String Value: ");
      System.out.println(string.toString());

      String string1 = "Now a days apples are been coated by wax.";
      System.out.print("Output String Value: ");
      System.out.println(string1.toString());
   }
}
```

📤 **Output:**

```
Output String Value: An apple a day keeps a doctor away
Output String Value: Now a days apples are been coated by wax.
```

**Using `Integer.toString()` to convert int to String:**

```java
public class Main {
   public static void main(String[] args) {
      String string = Integer.toString(52);
      System.out.println(string);
      System.out.println(string.toString());
   }
}
```

📤 **Output:**

```
52
52
```

---

## 2. toString() with Custom Objects

Let us see it through an Object. The below-defined `Student` object contains variables `rollno`, `name`, and `city`. Among them, `name` and `city` are string types. When we display the student object then the `print()` or `println()` method internally calls the `toString()` method and it will invoke the `String.toString()` method to display the string values.

**Student class:**

```java
public class Student {
   int rollno;
   String name;
   String city;

   Student(int rollno, String name, String city) {
      this.rollno = rollno;
      this.name = name;
      this.city = city;
   }

   @Override
   public String toString() {
      return "Student [rollno=" + rollno +
             ", name=" + name + ", city=" + city + "]";
   }
}
```

**Main class:**

```java
public class Main {
   public static void main(String args[]) {
      Student string1 = new Student(1, "John", "Los Angeles");
      Student string2 = new Student(2, "Amelia", "Chicago");

      System.out.println(string1);
      System.out.println(string2);
   }
}
```

📤 **Output:**

```
Student [rollno=1, name=John, city=Los Angeles]
Student [rollno=2, name=Amelia, city=Chicago]
```

> 💡 **Tip:** Always override the `toString()` method in your custom classes to provide meaningful string representations. Without overriding, `System.out.println(object)` will print the class name followed by the hash code (e.g., `Student@1a2b3c4`).

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

**Java Tutorial**

**[String Class Methods](097_String_Class_Methods_In_Java.md)**
