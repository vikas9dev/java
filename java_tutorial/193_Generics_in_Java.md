# Generics in Java

**Generics in Java** | The main objectives of generics are to provide type safety and to resolve type-casting problems.

- [Type Safety](#type-safety)
- [Type Casting](#type-casting)
- [How to use Generics?](#how-to-use-generics)
- [Generics Class](#generics-class)
- [Bounded Types](#bounded-types)
- [Important Points](#important-points)
- [Generic Methods & Wild Character (?)](#generic-methods--wild-character-)
- [Generic Methods](#generic-methods)
- [Communication with Non-Generic Code](#communication-with-non-generic-code)
- [Conclusions](#conclusions)

---

## 1. Type Safety

Arrays are type safe i.e. we can give the guarantee for the type of element present inside the array. For example: if our programming requirement is to hold only string type of objects then we can choose a string array. By mistake, if we are trying to add any other type of object then we will get a compile time error.

```java
String str[] = new String[10];
str[0] = "KnowProgram";
str[1] = "Java";
str[2] = 10; // Compile time error
str[2] = null;
```

If we try to add an integer number to the string array then we will get the compile time error: `incompatible types: int cannot be converted to String.`

Therefore String array can contain only string-type elements. We can give a guarantee for the type of elements present inside the array. Hence arrays are safe to use concerning type i.e. arrays are type-safe.

🛠️ **Collection without generics:**

```java
import java.util.*;
public class Test {
   public static void main(String[] args) {
      ArrayList al = new ArrayList();
      al.add("KnowProgram");
      al.add(10);
      al.add(null);
      al.add(new StringBuffer("Java"));
      System.out.println(al);

      String name1 = (String)al.get(0);
      String name2 = (String)al.get(1);
      String name3 = (String)al.get(2);
   }
}
```

📤 **Output:**

```
[KnowProgram, 10, null, Java]
Exception in thread "main" java.lang.ClassCastException: class java.lang.Integer cannot be cast to class java.lang.String.
```

But collections are not type safe i.e. we can't give guarantee for the type of element present inside the collection. For example: if our program requirement is to hold only `String` type of objects & if we choose `ArrayList`, and try to add any other type of object then we won't get any compile time error but the program may fail at Runtime.

> ⚠️ **Caution:** We can't give guarantee for the type of elements present inside the collection. Due to this, collections are not safe to use concerning type i.e. Collections are not type-safe.

---

## 2. Type Casting

In the case of arrays, at the time of retrieval, it is not required to perform type casting because it is a guarantee for the type of elements present inside the array.

```java
String str[] = new String[10];
str[0] = "KnowProgram";
String name = str[0]; // type casting not required
```

But in the case of collection at the time of retrieval, we must perform type casting because there is no guarantee for the type of elements present inside the collection.

```java
ArrayList al = new ArrayList();
al.add("KnowProgram");
String name1 = al.get(0); // Compile time error
String name2 = (String)al.get(0);
```

At the third line, we get the compile time error: `incompatible types: Object cannot be converted to String.`

Hence type casting is a bigger headache in collections. To overcome the above problems of collection, the generics concept was introduced in the 1.5 version.

🔑 **Key Point:** The main objectives of generics are:

- 🛡️ To provide type safety
- ⚙️ To resolve type-casting problems

---

## 3. How to use Generics?

For example: to hold only the string type of object we can create a generic version of the `ArrayList` object as follows:

```java
ArrayList<String> al = new ArrayList<String>();
```

For this `ArrayList`, we can add only the `String` type of object. If we try to add any other type element then we will get compile time error.

```java
import java.util.*;
public class Test {
   public static void main(String[] args) {
      ArrayList<String> al = new ArrayList<String>();
      al.add("KnowProgram");
      al.add("Java");
      al.add(10); // compile time error
      al.add(new StringBuilder("Generic")); // error
   }
}
```

📤 **Output:**

```
Test.java:7: error: incompatible types: int cannot be converted to String
al.add(10);
^
Test.java:8: error: incompatible types: StringBuilder cannot be converted to String
al.add(new StringBuilder("Generic"));
^
```

Hence through generics, we are getting type safety. At the time of retrieval, we are not required to perform typecasting:

```java
String name1 = al.get(0); // type casting not required
```

Hence through generics, we can solve type-casting problems.

| Feature | Non-Generic `ArrayList al = new ArrayList();` ❌️ | Generic `ArrayList<String> al = new ArrayList<String>();` ✅ |
|---------|--------------------------------------------------|-----------------------------------------------------------|
| **Type** | Non-generic version | Generic version |
| **Type Safety** | ❌️ Can add any type of object, not type-safe | ✅ Can add only String type, type-safe |
| **Type Casting** | ❌️ Compulsory type casting at retrieval | ✅ No type casting required at retrieval |

### Important Points

🔑 **1. Polymorphism is applicable only for base type but not for parameter type.** (Polymorphism: Uses of parent reference to hold child object is the concept of polymorphism).

```java
ArrayList<String> al1 = new ArrayList<String>();
```

Here `ArrayList` is the base type and `String` is the parameter type.

```java
List<String> al2 = new ArrayList<String>(); // valid
Collection<String> al3 = new ArrayList<String>(); // valid
ArrayList<Object> al4 = new ArrayList<String>(); // invalid, compile time error
```

For the last line we get the compile time error: `incompatible types: ArrayList<String> cannot be converted to ArrayList<Object>`.

🔑 **2. For the type parameter, we can provide any class/interface name but not primitive data type.** If we are trying to provide the primitive data type then we will get compile time error.

```java
ArrayList<int> al = new ArrayList<int>(); // compile time error
```

📤 **Output:**

```
error: unexpected type
      ArrayList<int> al = new ArrayList<int>();
                ^
  required: reference
  found:    int
```

---

## 4. Generics Class

Until the 1.4 version, the non-generic version of the `ArrayList` class was given as follows:

```java
class ArrayList {
   add(Object o) { }
   Object get(int index) { }
   // other methods
}
```

In the non-generic version of the `ArrayList` class:

- ❌️ The argument to `add()` method is `Object`. Hence we can add any type of value to the ArrayList. Due to this we are missing type safety.
- ❌️ The return type of `get()` is `Object` hence at the time of retrieval we have to perform type casting.

But in the 1.5 version a generics version of the `ArrayList` class is declared as follows:

```java
class ArrayList<T> {
   add(T k) { }
   T get(int index) { }
   // other methods
}
```

Based on our runtime requirement `T` will be replaced with our provided type.

```java
ArrayList<String> al1 = new ArrayList<String>();
```

For example to hold only `String` type of objects a generic version of `ArrayList` can be created as follows:

```java
class ArrayList<String> {
   add(String k) { }
   String get(int index) { }
   // other methods
}
```

Here the argument to `add()` method is `String` type. Hence we can add only `String` type value to the `ArrayList`. If we try to add another type value then we will get a compile-time error.

```java
ArrayList<String> al = new ArrayList<String>();
al.add("KnowProgram");
al.add("Java");
al.add(10); // compile time error
al.add(new StringBuilder("Generic")); // error
```

Hence through generics, we are getting type safety. The Return type of the `get()` method is `String`, hence at the time of retrieval, we are not required to perform type casting.

```java
String str = al.get(0); // valid, type casting not required.
```

In C++, it is already there known as a template. In Generics we are associating a type parameter to the class. Such types of parameter-raised classes are nothing but generic classes or template classes. Based on our requirements we can define our generic classes also:

```java
class Account<T> {}

Account<Gold> acc1 = new Account<Gold>();
Account<Platinum> acc2 = new Account<Platinum>();
```

🛠️ **Custom generic class example:**

```java
public class Test {
   public static void main(String[] args) {
      Gen<String> g1 = new Gen<String>("KP");
      g1.show();
      System.out.println(g1.getOb());

      Gen<Integer> g2 = new Gen<Integer>(100);
      g2.show();
      System.out.println(g2.getOb());

      Gen<Double> g3 = new Gen<Double>(10.30);
      g3.show();
      System.out.println(g3.getOb());
   }
}

class Gen<T> {
   T ob;
   Gen(T ob) {
      this.ob = ob;
   }
   public void show() {
      System.out.println("The type of ob: "
       + ob.getClass().getName());
   }
   public T getOb() {
      return ob;
   }
}
```

📤 **Output:**

```
The type of ob: java.lang.String
KP
The type of ob: java.lang.Integer
100
The type of ob: java.lang.Double
10.3
```

---

## 5. Bounded Types

We can bound the type parameter into a particular range by using the `extends` keyword. Such types are called bounded types.

```java
class Test<T> {}
```

As the type parameter, we can pass any type and there are no restrictions. Hence it is an unbounded type.

```java
Test<Integer> t1 = new Test<Integer>();
Test<String> t2 = new Test<String>();
```

**Syntax for bounded types:**

```java
class Test<T extends X> {}
```

Here `X` can be either class or interface.

- 📖 If `X` is a class then as a type parameter we can pass either `X` type or its child class type.
- 📖 If `X` is an interface then as the type parameter we can pass either `X` type or its implementation classes.

The below are invalid declarations:

```java
class Test<T implements Runnable> { } // invalid
class Test<T super Runnable> { } // invalid
```

> ⚠️ **Caution:** We must use only the `extends` keyword. The `implements` and `super` are invalid declarations.

🛠️ **Example with Class:**

```java
class Test<T extends Number> { }

class Example {
   public static void main(String[] args) {
      Test<Integer> t1 = new Test<Integer>(); // valid
      Test<String> t2 = new Test<String>(); // invalid
   }
}
```

Compile time error: `type argument String is not within bounds of type-variable T`

Here we can pass only `Number`, `Integer`, etc child classes of `Number`, but we can't pass `String`.

🛠️ **Example with Interface:**

```java
class Test<T extends Runnable> { }

class Example {
   public static void main(String[] args) {
      Test<Runnable> t1 = new Test<Runnable>(); // valid
      Test<Thread> t2 = new Test<Thread>(); // valid
      Test<Integer> t3 = new Test<Integer>(); // invalid
   }
}
```

Compile time error: `type argument Integer is not within bounds of type-variable T`

🛠️ **Bounded types in Combination:**

We can define bounded types even in combination also.

```java
class Test<T extends Number & Runnable> { }
```

As the type parameter, we can take anything that should be a child class of `Number` and should implement the `Runnable` interface.

Another example:

- ✅ `class Test<T extends Runnable & Comparable> { }` - valid
- ✅ `class Test<T extends Number & Runnable & Comparable> { }` - valid
- ❌️ `class Test<T extends Runnable & Number> { }` - invalid because we have to take the class first followed by the interface next. The correct form is: `class Test<T extends Number & Runnable> { }`
- ❌️ `class Test<T extends Number & Thread> { }` - invalid because we can't extend more than one class simultaneously. `Number` and `Thread` both are classes.

---

## 6. Important Points

1. We can define bounded types only by using the **extends keyword** and we can't use `implements` and `super` keyword but we can replace the `implements` keyword purpose with the `extends` keyword.

```java
class Test<T extends Number> {} // valid
class Test<T extends Runnable> {} // valid
class Test<T implements Runnable> {} // invalid, we can't use implements keyword
class Test<T super String> {} // invalid, we can't use super keyword
```

2. As the type parameter `T`, we can take any valid Java identifier but it is conventional to use `T` ("T" used to represent "Type").

```java
class Test<T> {} // valid
class Test<A> {} // valid
class Test<Java> {} // valid
class Test<knowprogram> {} // valid
```

3. Based on our requirement we can declare any number of type parameters and all these type parameters should be separated with commas.

```java
class Test<A, B> {} // valid
class Test<X, Y, Z> {} // valid
class Test<K, V> {} // valid, K=> Key, V=> value
```

🛠️ **Example:**
`HashMap<Integer, String> hm = new HashMap<Integer, String>();`

---

## 7. Generic Methods & Wild Character (?)

**1. `m1(ArrayList<String> al)`**

- 📋 We can call this method by passing an `ArrayList` object of only `String` type.
- 🛡️ Within the `m1()` method, we can add only string-type objects to the list. By mistake, if we try to add any other type then we will get a compile-time error.

```java
import java.util.*;
public class Test {
   public static void main(String[] args) {
      ArrayList<String> al = new ArrayList<String>();
      m1(al);
      System.out.println(al);
   }
   public static void m1(ArrayList<String> al)  {
      al.add("A");
      al.add(null);
      al.add(10); // invalid
   }
}
```

**2. `m1(ArrayList<?> al)`**

- 📋 We can call this method by passing an `ArrayList` object of any type.
- 🔒 Within the `m1()` method, we can't add anything to the list except `null` because we don't know the type exactly. The `null` is allowed because it is a valid value for any type.

```java
public static void m1(ArrayList<?> al)  {
   al.add(null);
   al.add("A");
   al.add(10); // invalid
   al.add(10.5); // invalid
}
```

💡 **Tip:** This type of method is best suitable for read-only operations.

**3. `m1(ArrayList<? extends X> al)`**

- 📋 `X` can be either class or interface. If `X` is a class then we can call this method by passing `ArrayList` of either `X` type or its child class type. If `X` is an interface then we can call this method by passing `ArrayList` of either `X` type or its implementation classes.
- 🔒 Within this method, we can't add anything except `null` because we don't know the type exactly.
- 💡 This type of method is best suitable for read-only operations.

**4. `m1(ArrayList<? super X> al)`**

- 📋 `X` can be either class or interface. If `X` is a class then we can call this method by passing `ArrayList` of either `X` type or its superclasses. If `X` is an interface then we can call this method by passing `ArrayList` of either `X` type or superclass of implementation class of `X`.
- ✅ Within this method can add `X` type of object and `null` to the list.

🛠️ **Example:** `m1(ArrayList<? super Runnable> al)`
Object => Thread => Runnable.

The `Thread` class implements `Runnable`, and the `Object` class is the superclass of the `Thread` class. Hence we can call the `m1()` method by passing `Runnable` type or `Object` type.

```java
import java.util.*;
public class Test {
   public static void main(String[] args) {
      ArrayList<Runnable> alr = new ArrayList<Runnable>();
      m1(alr); // valid

      ArrayList<Object> alo = new ArrayList<Object>();
      m1(alo); // valid

      ArrayList<Thread> alt = new ArrayList<Thread>();
      m1(alt); // invalid
   }

   public static void m1(ArrayList<? super Runnable> al)  {
      al.add(null);
      // al.add("A");
      // al.add(10); // invalid
   }
}
```

Compile time error: `incompatible types: ArrayList<Thread> cannot be converted to ArrayList<? super Runnable>`

**Based on the above examples, find out the valid syntax:**

```java
import java.util.*;
public class Test {
   public static void main(String[] args) {
      ArrayList<String> al1 = new ArrayList<String>();
      ArrayList<?> al2 = new ArrayList<String>(); // valid
      ArrayList<?> al3 = new ArrayList<Integer>(); // valid

      ArrayList<? extends Number> al4 = new ArrayList<Number>(); // valid
      // Number is valid

      ArrayList<? extends Number> al5 = new ArrayList<Integer>(); // valid
      // Integer is child class of Number

      //ArrayList<? extends Number> al6 = new ArrayList<String>(); // invalid
      // String is not child class of Number

      ArrayList<? super String> al7 = new ArrayList<Object>(); // valid
      //ArrayList<?> al8 = new ArrayList<?>(); // invalid
      //ArrayList<?> al9 = new ArrayList<? extends Number>(); // invalid
   }
}
```

📝 **Note:** Wild card character `?` is applicable only on the declaration part (left side of `=`), hence in `al7` and `al8` we will get the compile time error.

```
Test.java:18: error: unexpected type
      ArrayList<?> al8 = new ArrayList<?>(); // invalid
                                      ^
  required: class or interface without bounds
  found:    ?
Test.java:19: error: unexpected type
      ArrayList<?> al9 = new ArrayList<? extends Number>(); // invalid
                                      ^
  required: class or interface without bounds
  found:    ? extends Number
```

---

## 8. Generic Methods

We can declare type parameters either at the class level or method level.

**Declaring type parameter at class level:**

```java
class Test<T> {}
```

We can use `T` within this class based on our requirements.

**Declaring type parameter at the method level:**

We can define bounded type even at the method level. We have to declare the type parameter just before the return type.

```java
class Test<T> {
   public <T>void m1(T ob) { }
}
```

In the `m1()` method, we can use `T` anywhere based on our requirements.

**Examples:**

- ✅ `public <T> void m1() {}`
- ✅ `public <T extends Number> void m1() {}`
- ✅ `public <T extends Runnable> void m1() {}`
- ✅ `public <T extends Number & Runnable> void m1() {}`
- ✅ `public <T extends Comparable & Runnable> void m1() {}`
- ✅ `public <T extends Number & Comparable & Runnable> void m1() {}`
- ❌️ `public <T extends Runnable & Number> void m1() {}` - CE: class should be taken first
- ❌️ `public <T extends Number & Thread> void m1() {}` - We can't extend more than one class.

---

## 9. Communication with Non-Generic Code

If we send the generic object to a non-generic area then it starts behaving like a non-generic object. Similarly, if we send the non-generic object to the generic area then it starts behaving like a generic object. That is the location in which an object is present based on that behavior will be defined.

```java
import java.util.ArrayList;
class Test<T> {
   public static void main(String[] args) {
      ArrayList<String> al = new ArrayList<String>();
      // generic area

      al.add("KnowProgram");
      al.add("Java");
      // al.add(10); // invalid
      // al.add(10.5); // invalid

      m1(al);
      System.out.println(al);
   }
   public static void m1(ArrayList al) {
      // non-generic area
      al.add(10);
      al.add(10.5);
      al.add(true);
   }
}
```

📤 **Output:**

```
[KnowProgram, Java, 10, 10.5, true]
```

📝 **Note:** In the `main()` method we can't add `10`, `10.5` to the list but in the `m1()` method we can add `10`, `10.5`. Because in the `main()` method `al` ArrayList object is a generic type and only `String` type objects can be added to the ArrayList, but in the `m1()` method `al` ArrayList object is the non-generic type and we can add any type of value to the ArrayList.

---

## 10. Conclusions

The main purpose of generics is to provide type safety and to resolve type casting problems.

🔑 **Key Point:** Type safety and type casting both are applicable at compile time hence generic concept is also applicable only at compile time but not at runtime. At the time of compilation as the last step generic syntax will be removed and hence for the JVM generic syntax won't be available.

Hence the following declarations are equal:

```java
ArrayList al = new ArrayList<String>();
ArrayList al2 = new ArrayList<Integer>();
ArrayList al3 = new ArrayList<Double>();
ArrayList al4 = new ArrayList();
```

**Example:**

```java
ArrayList al = new ArrayList<String>();
al.add(10);
al.add(10.5);
al.add(true);
System.out.println(al);
```

📤 **Output:**

```
[10, 10.5, true]
```

The following declarations are equal:

```java
ArrayList<String> al1 = new ArrayList<String>();
ArrayList<String> al2 = new ArrayList();
```

The reference is of `ArrayList<String>` type hence we can add only `String` type to the ArrayList.

```java
import java.util.ArrayList;
class Test<T> {
   public static void m1(ArrayList<String> al) { }
   public static void m1(ArrayList<Integer> al) { }
}
```

Compile time error: `name clash: m1(ArrayList) and m1(ArrayList) have the same erasure`

At compile time:

1. Compile code normally by considering generic syntax.
2. Remove generic syntax.
3. Compile once again.

After the 2nd step, the above class becomes:

```java
import java.util.ArrayList;
class Test<T> {
   public static void m1(ArrayList al) { }
   public static void m1(ArrayList al) { }
}
```

Hence it gives a Compile time error in the 3rd Step.
