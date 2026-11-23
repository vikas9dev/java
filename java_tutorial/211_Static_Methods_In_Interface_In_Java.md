# Static Methods In Interface In Java

**Static Methods In Interface In Java** | From Java 1.8 version onwards, we can also define static methods in an interface. Let us see what it means, how to define static methods in an interface, how to use them, and more. Also see: [Java 8: Default Methods In Interface](210_Default_Methods_In_Interface_In_Java.md)

- [Static Methods To Overriding](#static-methods-to-overriding)
- [Main Method in an Interface in Java](#main-method-in-an-interface-in-java)

---

- 🔌 From Java 1.8 version onwards in addition to default methods, we can also write static methods inside the interface to define utility functions.
- ⚠️ Interface static methods by default are not available to the implementation classes hence by using implementation class reference we can't call interface static methods. We should call interface static methods by using the interface name.

**Calling static methods via interface name:**

```java
interface A {
   public static void sum(int a, int b) {
      System.out.println("The Sum: " + (a + b));
   }
}

class Test implements A {
   public static void main(String[] args) {
      // t1.sum(10, 20); // Compile-time Error
      // Test.sum(10, 20); // Compile-time Error
      // sum(10, 20) // Compile-time Error
      A.sum(10, 20);
   }
}
```

> 🔑 **Key Point:** The main purpose of public static methods in the interface is to provide general utility methods. Any class can use these static methods without implementing the interface, just by using the interface name.

**Using static method without implementing interface:**

```java
interface A {
    public static void sum(int a, int b) {
        System.out.println("The Sum: " + (a + b));
    }
}

class Main {
    public static void main(String[] args) {
        A.sum(10, 20);
    }
}
```

📤 **Output:**

```
The Sum: 30
```

---

## 1. Static Methods To Overriding

As interface static methods by default are not available to the implementation class, the overriding concept is not applicable. Based on our requirement we can define the exact same method in the implementation class, it's valid and it is not overriding.

**Example-1: Static method with same signature in implementation class:**

```java
interface A {
    public static void m1() {
    }
}

class Test implements A {
    // valid
    public static void m1() {
        // it is not overriding
    }
}
```

**Example-2: Instance method with same name in implementation class:**

```java
interface A {
    public static void m1() {
    }
}

class Test implements A {
    // valid
    public void m1() {
        // it is not overriding
    }
}
```

💡 **Tip:** In the child class, we can define methods with the same name by changing the modifier. The below example is valid and it is not overriding.

**Private method in parent, public in child:**

```java
class P {
  private void m1() {}
}

class C extends P {
  // not overriding
  public void m1() {}
}
```

---

## 2. Main Method in an Interface in Java

Since we can define static methods inside the interface therefore we are also able to define the `main()` method in any interface. From Java 1.8 version onwards we can write the `main()` method inside the interface and hence we can run the interface directly from the command prompt.

**Interface with main method:**

```java
interface A {
   public static void main(String[] args) {
      System.out.println("Interface Main Method");
   }
}
```

📤 **Output:**

```
Interface Main Method
```
