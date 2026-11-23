# Difference Between == and equals() in Java

**Difference Between == and equals() in Java** | In Java, we can compare objects in two ways -- either by using its reference or by using its state/data/values. We compare objects by using the `==` operator or by using the `equals()` method.

- [== vs equals() in Java](#-vs-equals-in-java)
- [Relation Between == Operator and equals() method in Java](#relation-between--operator-and-equals-method-in-java)
- [Equal (==) Operator in Java](#equal--operator-in-java)
- [equals() Method in Java](#equals-method-in-java)

1. ⚙️ **[Equal Operator (==)](021_Equal_Operator_(==)_in_Java.md)** -- It compares primitives based on their values, and objects based on their reference.

2. ⚖️ **equals() method** -- It compares objects either by using their reference or by using their data, it depends on the implementation logic.

> 📝 **Note:** It is not true that the `equals()` method always compares two objects with their data. The default implementation of `equals()` method given in [java.lang.Object class](069_Object_Class_in_Java.md) compares objects based on their reference. To compare objects based on their data we must override the `equals()` method.

---

## 1. == vs equals() in Java

The below table shows the major differences between the `==` operator and `equals()` method in Java.

🧠 **In Simple Words:** In general we use the `==` operator for reference comparison and the `equals()` method for state/data comparison in Java programming language.

| Feature ⚖️ | Equal (==) operator 🔹 | equals() method 🔸 |
|---------|----------------------|-------------------|
| **Applicable to** | Both primitive values and objects | Objects only, not primitives |
| **Comparison basis** | Primitives by values, objects by reference | Objects by reference or state (depends on implementation) |
| **Incompatible types** | ❌️ Compile-time error | ✅ Returns `false` |
| **Overridable** | ❌️ No (it is an operator) | ✅ Yes (it is a method) |

Now let us see the different test cases for the `==` operator in Java:

| Comparison using == ⚙️ | Valid? ✅ | Return 📤 |
|---------|--------|--------|
| **Two objects** | Yes | `false` |
| **Two primitive variables** | Yes | `false`/`true` |
| **Two nulls** | Yes | `true` |
| **Null with object** | Yes | `false` |
| **Object with null** | Yes | `false` |
| **Null referenced with null** | Yes | `true` |
| **Null referenced with object** | Yes | `false` |
| **Object with null referenced** | Yes | `false` |
| **Incompatible objects** | No | Error |

Now let us see the different test cases for the `equals()` method in Java. In the equals() method we demonstrated these comparisons with example code, you can check there.

| Comparison using equals() ⚖️ | Valid? ✅ | Return 📤 |
|---------|--------|--------|
| **Two objects** | Yes | `false`/`true` |
| **Two primitive variables** | No | Error |
| **Two nulls** | No | Error |
| **Null with object** | No | Error |
| **Object with null** | Yes | `false` |
| **Null referenced with null** | No | NPE* |
| **Null referenced with object** | No | NPE* |
| **Two Null referenced** | No | NPE* |
| **Object with null referenced** | Yes | `false` |
| **Incompatible objects** | Yes | `false` |

NPE* => **NullPointerException**, Error => Compile-time error

---

## 2. Relation Between == Operator and equals() method in Java

Assume `t1` and `t2` are objects of the `Test` class.

1. 🔑 **If `t1 == t2` is true** then **`t1.equals(t2)` is always true.** If two referenced variables are pointing to the same object then the state/data of these objects will be always the same.
2. 📝 If **`t1==t2` is false** then **`t1.equals(t2)` can be true or false**.

| `t1==t2` 🔹 | `t1.equals(t2)` 🔸 |
|---------|----------------|
| `true` | `true` |
| `false` | `true`/`false` |

3. 📝 If **`t1.equals(t2)` is true** then **`t1 == t2` can be true or false**.
4. 🔑 If **`t1.equals(t2)` is false** then **`t1 == t2`** will be **always false**.

| `t1.equals(t2)` 🔸 | `t1==t2` 🔹 |
|----------------|---------|
| `true` | `true`/`false` |
| `false` | `false` |

Now let us see the examples of these differences in detail.

---

## 3. [Equal (==) Operator in Java](021_Equal_Operator_(==)_in_Java.md)

The equal (`==`) operator compares primitives based on their values and objects based on their reference.

**Comparing two primitive values using == operator:**

```java
int x = 9;
int y = 10;
int z = 9;

System.out.println(x == y); // false
System.out.println(x == z); // true
System.out.println(y == z); // false
```

We can't use the equal (`==`) operator to compare incompatible types values otherwise the compiler will throw an error. For example `boolean` is an incompatible primitive data type with the remaining other data types, therefore we can't compare `boolean` with other primitive data types.

**Incompatible type comparison:**

```java
int a = 9;
double b = 10.5;
boolean c = true;

System.out.println(a == b); // false

System.out.println(b == c); // error
// error: incomparable types: double and boolean

System.out.println(a == c); // error
// error: incomparable types: int and boolean
```

**Comparing two objects using the equal (==) operator:**

For two objects if both referenced variables are pointing to the same object then the equal (`==`) operator returns `true`, else it returns `false`.

```java
public class Test {
   public static void main(String[] args) {

      Test t1 = new Test();
      Test t2 = new Test();
      Test t3 = t1;

      System.out.println(t1 == t2); // false
      System.out.println(t1 == t3); // true
      System.out.println(t2 == t3); // false
   }
}
```

We can't use an equal (`==`) operator to compare incompatible types of objects, otherwise, the compiler will throw an error.

**Incompatible object comparison:**

```java
class A{}

public class Test {
   public static void main(String[] args) {

      Test t1 = new Test();
      A a1 = new A();

      System.out.println(t1 == a1); // error
      // error: incomparable types: Test and A
   }
}
```

**Comparing null values using the equal (==) operator:**

There are four cases:

| Comparing null with 🔍 | Return value 📤 |
|---------|--------|
| **Another null** | `true` |
| **Null reference variable** | `true` |
| **Object reference variable** | `false` |
| **Object** | `false` |

```java
Test t1 = null;
Test t2 = new Test();

// Comparing null with other null
System.out.println(null == null); // true

// Comparing null with null reference variable
System.out.println(null == t1); // true

// Comparing null with object reference variable
System.out.println(null == t2); // false

// Comparing null with object
System.out.println(null == new Test()); // false
```

---

## 4. equals() Method in Java

By default `equals()` method of [java.lang.Object class](069_Object_Class_in_Java.md) compares two objects with their reference. In the Object class, the `equals()` method is implemented to compare two objects with their references. Since the `equals()` method is an instance/non-static method, therefore we can't compare two primitive values using the `equals()` method -- an object is required.

**Object comparison with equals():**

```java
public class Test {
   public static void main(String[] args) {

      Test t1 = new Test();
      Test t2 = new Test();
      Test t3 = t1;

      System.out.println(t1.equals(t2)); // false
      System.out.println(t1.equals(t3)); // true
      System.out.println(t2.equals(t3)); // false
   }
}
```

Like the equal(`==`) operator, the `equals()` method will not throw an error for comparing incompatible objects, rather it returns `false` because the compiler checks only whether it is possible to invoke the `equals()` method using the `c1` object by passing `t1` object or not. Since this invocation is possible, so the compiler will not throw an error. JVM checks references stored in both variables, and if those references are different it returns `false`.

**Incompatible object comparison with equals():**

```java
class A{}

public class Test {
   public static void main(String[] args) {

      Test t1 = new Test();
      A a1 = new A();

      System.out.println(t1.equals(a1)); // false
   }
}
```

**Comparing two null values using the equals() method:**

We can't invoke the method using `null`, it leads to a compile-time error. If we invoke the `equals()` method using the null referenced variable, then it raises `NullPointerException`.

```java
Test t1 = null;
Test t2 = new Test();

System.out.println(null.equals(null)); // error
// error: <null> cannot be dereferenced

System.out.println(t1.equals(null)); // exception
// Exception java.lang.NullPointerException

System.out.println(t2.equals(null)); // false
// equals method can be invoked by passing null
```

> 💡 **Tip:** When the `==` operator is already there to compare objects then why is `equals()` method given in Java? In Java, the equal (`==`) operator compares only the reference of the objects, so the `equals()` method is given to compare objects with the state. The `equals()` method is implemented in `java.lang.Object` class with default implementation comparing objects with references. Using the `equals()` method, if we want to compare objects using their state then we must override it in the subclass.

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

**Java Tutorial**

**Java.lang.Object Class**
- [Object Class in Java](069_Object_Class_in_Java.md)
- getClass() method
- [hashCode() Method](071_Hashcode_in_Java_–_hashCode()_Method.md)
- toString() Method
- Java equals() Method
- == vs equals() in Java
- HashCode() vs equals()
- [Clone() Method in Java](074_Clone()_Method_in_Java.md)
- Object Class Quiz Set-1
- Object Class Quiz Set-2
- equals() Method Quiz
- Hashcode Value Quiz

**Math Class in Java**
- [Java Math class & methods](078_Java_Math_Class_with_Examples.md)
- [Import Math class in Java](077_Import_Math_Class_in_Java.md)
- [Math.PI in Java Example](079_PI_in_Java_–_Math.PI_Java_Example.md)
- Math.sqrt() method in Java
- Math.pow() method in Java
- Math.max() method in Java
- Math.abs() method in Java
- Math.ceil() method in Java
- Math.floor() method in Java
- Math.round() method in Java
- Math.random() method Java
