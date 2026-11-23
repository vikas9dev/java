# Java Collection Interface

**Java Collection Interface** | If we want to represent a group of individual objects as a single entity then we should go for Collection(I). A collection represents a group of objects, known as its elements.

- [Implementation Classes of Java Collection Interface](#implementation-classes-of-java-collection-interface)
- [Java Collection Interface Methods](#java-collection-interface-methods)
- [Java Collection Interface Example](#java-collection-interface-example)

---

## 1. Implementation Classes of Java Collection Interface

It is part of the [Java Collection Framework](192_Java_Collection_Framework_Overview.md) (i.e. `java.util` package). Most of the interfaces/classes belonging to `java.util` package directly or indirectly implements `Collection(I)`, therefore the Collection interface is considered as the **root interface** of Java Collection Framework.

Java collection interface was introduced in **Java 1.2 version**. It implements an `Iterable` interface. The class declaration of `Collection(I)` is:

```java
public interface Collection<E> extends Iterable<E>
```

Collection interface is not directly implemented by any class but there are some interfaces that implement `Collection(I)`, and many classes implement those interfaces. Hence indirectly those classes and `Collection(I)` are in an inheritance relationship.

- Collection(I)
  - **List(I)**
    - ArrayList
    - LinkedList
    - Vector
      - Stack
  - **Set(I)**
    - HashSet
      - LinkedHashSet
    - SortedSet(I)
      - NavigableSet(I)
        - _TreeSet_
  - **Queue(I)**
    - PriorityQueue
    - BlockingQueue
      - PriorityBlockingQueue
      - LinkedBlockingQueue
    - _Other classes_

`List`, `Set`, and `Queue` interface implements Collection interface. Here `List`, `Set`, `SortedSet`, `NavigableSet`, and `Queue` are interfaces, and the remaining are classes.

📋 **1) List(I):** `ArrayList`, `LinkedList`, and `Vector` are child classes of `List(I)`. `Stack` is the child class of `Vector`. It is the child interface of `Collection(I)`. We should go for `List(I)` if we want to represent a group of individual objects as a single entity where:

- ✅ **Duplicates are allowed**
- ✅ **Insertion order must be preserved.** Similar to the array, the index of List also starts with 0.

📦 **2) Set(I):** It is the child interface of `Collection(I)`. `HashSet` and `SortedSet` are direct child classes of `Set(I)`. We should go for Set if we want to represent a group of individual objects as a single entity where:

- ❌️ **Duplicates are not allowed**
- ❌️ **Insertion order not preserved.**

📬 **3) Queue(I):** It is child interface of `Collection(I)`. If we want to represent a group of individual objects prior to processing then we should go for the queue. Usually, the queue follows **FIFO (first in first out) order** but based on our requirement we can implement our own priority order also.

All collection framework classes which indirectly implement `Collection(I)` provides at least two constructors: a void (no arguments) constructor, which creates an empty collection, and a constructor with a single argument of type Collection, which creates a new collection with the same elements as its argument. This 2nd constructor allows the user to copy any collection, producing an equivalent collection of the desired implementation type. Example:

- `ArrayList()`
- `ArrayList(Collection c)`
- `LinkedList()`
- `LinkedList(Collection c)`
- `HashSet()`
- `HashSet(Collection c)`

---

## 2. Java Collection Interface Methods

The collection interface defines the most common methods which are applicable for any collection object. It contains a total of 15 methods. Those methods will be also available in `ArrayList`, `LinkedList`, `Vector`, `HashSet`, `LinkedHashSet`, `TreeSet`, `PriorityQueue`, and e.t.c. classes.

| Method 🛠️ | Description 📋 |
|-----------|---------------|
| `boolean add(E e)` | Add specific element |
| `boolean addAll(Collection<? extends E> c)` | Add all elements of collection "c" |
| `boolean remove(Object o)` | Remove specific element from collection |
| `boolean removeAll(Collection<?> c)` | Remove all elements present in collection "c" |
| `boolean retainAll(Collection<?> c)` | Remove all elements except those in collection "c" |
| `boolean isEmpty()` | Check collection is empty? |
| `int size()` | Find number of elements in the collection |
| `void clear()` | Remove all elements from the collection |
| `boolean contains(Object o)` | Check specific element is available? |
| `boolean containsAll(Collection<?> c)` | Check all elements of collection "c" are available? |
| `Object[] toArray()` | Convert collection to object array type |
| `<T> T[] toArray(T[] a)` | Convert collection to specified array type |
| `Iterator iterator()` | Returns an iterator over the elements |
| `boolean equals(Object o)` | Compares the specified object for equality |
| `int hashCode()` | Returns the hash code value |

### Methods to Add Elements

1. `boolean` **`add(E e)`** - To add a specific element to the collection.
2. `boolean` **`addAll(Collection <? extends E> c)`** - To add all elements present in the collection "c".

### Methods to Remove Elements

3. `boolean` **`remove(Object o)`** - To remove the first occurrence of a specific element from the collection.
4. `boolean` **`removeAll(Collection <?> c)`** - To remove all elements present in collection "c".
5. `boolean` **`retainAll(Collection <?> c)`** - To remove all elements from the collection except those are present in collection "c".

📝 **Note:** The return type of these above methods is `boolean`. Some collection classes allow to add duplicates and some collection classes don't. On calling these methods if there is a change in collection size then they return `true` else they return `false`.

### Methods for Query Operations

6. `boolean` **`isEmpty()`** - To check whether collection is empty or not. It returns `true` if the collection doesn't contain any element.
7. `int` **`size()`** - To find the number of elements in the collection. If the collection contains more than `Integer.MAX_VALUE` elements, then it returns `Integer.MAX_VALUE`.
8. `void` **`clear()`** - To remove all elements from the collection. On calling this method the collection will be empty.

### Methods to Convert Collection to Array

9. `Object[]` **`toArray()`** - To convert collection to object array type.
10. `<T> T[]` **`toArray(T[] a)`** - To convert collection to specified array type.

### Methods to Check Elements

11. `boolean` **`contains(Object o)`** - To check whether a specific element is available or not. It returns `true` if this collection contains the specified element.
12. `boolean` **`containsAll(Collection <?> c)`** - To check whether all elements of collection "c" are available or not.

### Other Methods

13. `Iterator` **`iterator()`** - Returns an iterator over the elements in this collection.
14. `boolean` **`equals(Object o)`** - Compares the specified object with this collection for equality. It returns `true` if the specified object is equal to this collection.
15. `int` **`hashCode()`** - Returns the hash code value for this collection.

---

## 3. Java Collection Interface Example

🛠️ **Collection program to add and remove elements using ArrayList:**

```java
import java.util.ArrayList;
import java.util.Collection;

public class Test {
   public static void main(String[] args) {

      Collection<String> col1 = new ArrayList<String>();
      col1.add("A");
      col1.add("B");
      System.out.println(col1); // [A, B]

      Collection<String> col2 = new ArrayList<String>();
      col2.add("KP");
      col2.add("Java");
      System.out.println(col2); // [KP, Java]

      // Add all elements of col2 to col1
      col1.addAll(col2);
      System.out.println(col1); // [A, B, KP, Java]

      // remove element
      col1.remove("A");
      System.out.println(col1); // [B, KP, Java]

      // From col1, remove all elements present in col2
      col1.removeAll(col2);
      System.out.println(col1); // [B]
   }
}
```

📤 **Output:**

```
[A, B]
[KP, Java]
[A, B, KP, Java]
[B, KP, Java]
[B]
```

🛠️ **Java program to store objects in the Collection:**

Here we have a `Product` class with fields: PID (product id), name (product name), qty (product quantity), and price (the price of the product). We want to store those products in a collection.

```java
class Product {

   private int pid;
   private String name;
   private int qty; // quantity
   private double price;

   public Product(int pid, String name,
                  int qty, double price) {
      this.pid = pid;
      this.name = name;
      this.qty = qty;
      this.price = price;
   }

   @Override
   public String toString() {
      return "{" + pid + ", " + name
         + ", " + qty + ", " + price + "}";
   }
}
```

```java
import java.util.ArrayList;
import java.util.Collection;

public class Shop {
   public static void main(String[] args) {

      Collection<Product> col = new ArrayList<Product>();

      // Adding products to collection
      col.add(new Product(101, "Pen", 20, 5));
      col.add(new Product(205, "Book", 5, 100));
      col.add(new Product(101, "Pen", 20, 5)); // duplicate

      // display collection
      System.out.println(col);
   }
}
```

📤 **Output:**

```
[{101, Pen, 20, 5.0}, {205, Book, 5, 100.0}, {101, Pen, 20, 5.0}]
```

🛠️ **Collection program to demonstrate `isEmpty()`, `size()`, and `clear()` methods:**

```java
import java.util.ArrayList;
import java.util.Collection;

public class Test {
   public static void main(String[] args) {

      Collection<String> col = new ArrayList<String>();
      System.out.println(col.isEmpty()); // true
      System.out.println(col.size()); // 0

      col.add("A");
      col.add("B");
      System.out.println(col); // [A, B]

      System.out.println(col.isEmpty()); // false
      System.out.println(col.size()); // 2

      col.clear();
      System.out.println(col.isEmpty()); // true
      System.out.println(col.size()); // 0
   }
}
```

📤 **Output:**

```
true
0
[A, B]
false
2
true
0
```

🛠️ **Collection program to demonstrate `contains()`, `containsAll()`, `equals()`, and `hashCode()` methods:**

```java
import java.util.ArrayList;
import java.util.Collection;

public class Test {
   public static void main(String[] args) {

      Collection<String> col1 = new ArrayList<String>();
      col1.add("A");
      col1.add("B");
      System.out.println(col1); // [A, B]

      System.out.println(col1.contains("A")); // true
      System.out.println(col1.contains("Z")); // false

      Collection<String> col2 = new ArrayList<String>();
      col2.add("A");
      col2.add("Z");
      System.out.println(col2); // [A, Z]
      System.out.println(col1.containsAll(col2)); // false

      // equals()
      System.out.println(col1.equals(col2)); // false

      // hashcode()
      System.out.println(col1.hashCode()); // 3042
      System.out.println(col2.hashCode()); // 3066
   }
}
```

📤 **Output:**

```
[A, B]
true
false
[A, Z]
false
false
3042
3066
```

🛠️ **Java program to convert Collection to an array using `toArray()` method:**

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collection;

public class Test {
   public static void main(String[] args) {

      Collection<String> col = new ArrayList<String>();
      col.add("A");
      col.add("B");
      System.out.println(col); // [A, B]

      // Convert to an array of object
      Object[] obj = col.toArray();
      // display Array
      System.out.println("Object array: "
                   + Arrays.toString(obj));

      // convert to an array of String
      String[] str = new String[0];
      str = col.toArray(str);
      // display Array
      System.out.println("String array: "
                   + Arrays.toString(str));
   }
}
```

📤 **Output:**

```
[A, B]
Object array: [A, B]
String array: [A, B]
```

🛠️ **Collection program to demonstrate `iterator()` method:**

```java
import java.util.ArrayList;
import java.util.Collection;
import java.util.Iterator;

public class Test {
   public static void main(String[] args) {

      Collection<String> col = new ArrayList<String>();
      col.add("Know Program");
      col.add("Learn");
      col.add("Java Collection");

      Iterator<String> itr = col.iterator();
      while(itr.hasNext()) {
        String str = itr.next();
        System.out.println(str);
      }
   }
}
```

📤 **Output:**

```
Know Program
Learn
Java Collection
```
