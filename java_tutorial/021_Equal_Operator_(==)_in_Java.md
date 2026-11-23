# Equal Operator (==) in Java

**Equal Operator (==) in Java** | Understanding how the equality operator compares primitives by value and objects by reference.

- [Comparing Null using Equal Operator in Java](#comparing-null-using-equal-operator-in-java)

---

In Java equal operator is used to compare two primitives based on their value and two objects based on their references. After comparison, it gives a boolean result either `true`/`false`. It is widely used in conditional statements.

**Syntax:** `LHS value == RHS value`

🔑 **Important points on Java Equal operator:**

1. ⚖️ Equal operator can be used to compare both primitive values, and objects.
2. 🔍 Equal operator compares primitives based on their values, and objects based on their reference.
3. ❌️ The equal (`==`) operator can't compare incompatible objects/values, for this we get compile-time error.
4. 🏷️ It is an operator and in Java we can't override operators.

**Example to demonstrate equal operator for primitive values:**

```java
public class Test {
  public static void main(String[] args) {

    int a = 5;
    int b = 10;
    int c = 5;

    System.out.println(a == b); // false
    System.out.println(a == c); // true
    System.out.println(b == c); // false

    System.out.println('A' == 'A'); // true
    System.out.println('A' == 'B'); // false

    System.out.println(true == true); // true
    System.out.println(false == true); // false
  }
}
```

📤 **Output:**

```
false
true
false
true
false
true
false
```

The equal (`==`) operator can't compare incompatible values, for this we get the compile-time error. For example `boolean` is a primitive data type but it is incompatible with remaining all other data types.

**Incompatible types error:**

```java
public class Test {
  public static void main(String[] args) {

    int a = 5;
    double d = 20.5;
    boolean b = true;

    System.out.println(a == b);
    System.out.println(d == b);
  }
}
```

📤 **After compilation:**

```
Test.java:8: error: incomparable types: int and boolean
System.out.println(a == b);
^
Test.java:9: error: incomparable types: double and boolean
System.out.println(d == b);
^
2 errors
```

While comparing referenced variables, if both variables are referencing to the same object then it gives the result as `true`, else it gives the result `false`.

**Array reference comparison:**

```java
public class Test {
  public static void main(String[] args) {

    int[] arr1 = {10, 20, 30, 40, 50};
    int[] arr2 = {10, 20, 30, 40, 50};
    int[] arr3 = arr1;

    System.out.println(arr1 == arr2); // false
    System.out.println(arr1 == arr3); // true
  }
}
```

📤 **Output:**

```
false
true
```

**Object reference comparison:**

```java
public class Test {
  public static void main(String[] args) {

    Test t1 = new Test();
    Test t2 = new Test();
    Test t3 = t1;

    System.out.println(t1 == t2); // false
    System.out.println(t1 == t3); // true
  }
}
```

📤 **Output:**

```
false
true
```

> 💡 **Tip:** If we want to compare objects based on their content but not based on their reference then we have to use the equals() method of [java.lang.Object class](069_Object_Class_in_Java.md). Also see: Difference Between == and equals() in Java.

Using an equal operator in Java, We can't compare incompatible objects else we will get a compile-time error.

**Incompatible objects error:**

```java
public class Test {
  public static void main(String[] args) {
    int[] arr = {10, 20, 30, 40, 50};
    Test t1 = new Test();
    System.out.println(arr == t1); // error
  }
}
```

📤 **After compilation:**

```
Test.java:5: error: incomparable types: int[] and Test
System.out.println(arr == t1); // error
^
1 error
```

**Comparison summary using `==`:**

| Comparison Using == Operator ⚖️ | Valid? ✅ | Return 📋 |
|-------------------------------|---------|----------|
| **Two objects** | ✅ Yes | `false` |
| **Two primitive variables** | ✅ Yes | `false`/`true` |
| **Two nulls** | ✅ Yes | `true` |
| **Null with object** | ✅ Yes | `false` |
| **Object with null** | ✅ Yes | `false` |
| **Null referenced with null** | ✅ Yes | `true` |
| **Null referenced with object** | ✅ Yes | `false` |
| **Object with null referenced** | ✅ Yes | `false` |
| **Incompatible objects** | ❌️ No | error |

---

## 1. Comparing Null using Equal Operator in Java

1️⃣ **If we compare two nulls with each other using an equal operator then it gives `true`.**

```java
public class Test {
  public static void main(String[] args) {
    System.out.println(null == null); // true
  }
}
```

📤 **Output:**

```
true
```

2️⃣ **If we compare `null` with null reference variable using equal operator then also it gives `true`.**

```java
public class Test {
  public static void main(String[] args) {
    int[] arr = null;
    Test t1 = null;
    System.out.println(arr == null); // true
    System.out.println(t1 == null); // true
  }
}
```

📤 **Output:**

```
true
true
```

3️⃣ **If we compare `null` with object reference variable using equal operator then it gives `false`.**

```java
public class Test {
  public static void main(String[] args) {
    int[] arr = {10, 20, 30, 40, 50};
    Test t1 = new Test();
    System.out.println(arr == null); // false
    System.out.println(t1 == null); // false
  }
}
```

📤 **Output:**

```
false
false
```

4️⃣ **If we compare `null` with Objects using an equal operator then also it gives `false`.**

```java
public class Test {
  public static void main(String[] args) {
    int[] arr = {10, 20, 30, 40, 50};
    Test t1 = new Test();
    System.out.println(null == new Test()); // false
  }
}
```

📤 **Output:**

```
false
```

**Null comparison summary:**

| Using == Operator to Compare null With ⚖️ | Return Value 📋 |
|------------------------------------------|----------------|
| **Another null** | `true` |
| **Null reference variable** | `true` |
| **Object reference variable** | `false` |
| **Object** | `false` |
