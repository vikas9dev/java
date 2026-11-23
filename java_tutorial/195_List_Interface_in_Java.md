# List Interface in Java

**List Interface in Java** | What are the different List methods in Java? Program to demonstrate List and its methods.

- [List Interface Implementation Classes](#list-interface-implementation-classes)
- [List Methods in Java](#list-methods-in-java)
- [List in Java Example](#list-in-java-example)

---

## 1. List Interface Implementation Classes

List is the child interface of [Collection(I)](194_Java_Collection_Interface.md). If we want to represent a group of individual objects as a single entity where **duplicates are allowed & insertion order must be preserved** then we should go for List.

We can preserve insertion order with index & we can differentiate duplicate objects by using index hence index will play a very important role in List. Similar to the array its index starts from 0. We can use its index to iterate to the List.

| List 📋 | A | B | C | D | E | A |
|---------|---|---|---|---|---|---|
| **Index** | 0 | 1 | 2 | 3 | 4 | 5 |

**List interface declaration:**

```java
public interface List<E> extends Collection<E>
```

Implementation classes of List interface in Java:

- Collection(I)
  - List(I)
    - ArrayList
    - LinkedList
    - Vector
      - Stack

`ArrayList`, `LinkedList`, and `Vector` classes implement `List(I)`. `Stack` class extends from `Vector` class. The `Vector` and `Stack` classes are considered legacy classes because they were introduced in the 1.0 version. The remaining classes `ArrayList` & `LinkedList` were introduced in the 1.2 version.

| Class/Interface 🏷️ | Introduced in Version 📜 |
|--------------------|-------------------------|
| **Collection(I), List(I), ArrayList, LinkedList** | Java 1.2 |
| **Vector and Stack** | Java 1.0 |

---

## 2. List Methods in Java

List interface implements [Collection interface](194_Java_Collection_Interface.md), therefore all the 15 methods of Collection interface are also available to the List interface. The **15 methods given in Collection interface** are as follows: `add(E e)`, `addAll(Collection<? extends E> c)`, `remove(Object o)`, `removeAll(Collection<?> c)`, `retainAll(Collection<?> c)`, `isEmpty()`, `size()`, `clear()`, `contains(Object o)`, `containsAll(Collection<?> c)`, `Object[] toArray()`, `<T> T[] toArray(T[] a)`, `iterator()`, `equals(Object o)`, `hashCode()`

`List(I)` also defines the following **10 specific methods**: `add(int index, E element)`, `addAll(int index, Collection<? extends E> c)`, `get(int index)`, `remove(int index)`, `set(int index, E element)`, `indexOf(Object o)`, `lastIndexOf(Object o)`, `listIterator()`, `listIterator(int index)`, `subList(int fromIndex, int toIndex)`

Hence there is a total of 25 public methods in the List interface. Let us see these methods by arranging into some groups for easy understanding purposes.

### Methods to Add Elements

1. `boolean` **`add(E e)`** - Add a specific element to the list.
2. `void` **`add(int index, E element)`** - Insert an element at the given index.
3. `boolean` **`addAll(Collection <? extends E> c)`** - Add all elements present in the collection "c".
4. `boolean` **`addAll(int index, Collection <? extends E> c)`** - Insert a group of elements at given index.

### Methods to Remove Elements

5. `boolean` **`remove(Object o)`** - Remove the first occurrence of specific element from the list.
6. `E` **`remove(int index)`** - Remove/delete element at given index.
7. `boolean` **`removeAll(Collection <?> c)`** - Remove all elements present in collection "c".
8. `boolean` **`retainAll(Collection <?> c)`** - Remove all elements from the list except those present in collection "c".

### Methods to Get/Set or Find Elements

9. `E` **`get(int index)`** - Fetch element at given index.
10. `E` **`set(int index, E element)`** - Replace the element present at the specified index with the provided object and return the old object.
11. `int` **`indexOf(Object o)`** - Returns index of first occurrence of element "o".
12. `int` **`lastIndexOf(Object o)`** - Returns index of last occurrence of element "o".
13. `List<E>` **`subList(int fromIndex, int toIndex)`** - Returns a view of the portion of this list between the specified `fromIndex` (inclusive), and `toIndex` (exclusive).

### Methods to Check Elements

14. `boolean` **`contains(Object o)`** - Check whether a specific element is available or not.
15. `boolean` **`containsAll(Collection <?> c)`** - Check whether all elements of collection "c" are available or not.

### Methods to Iterate Over the List

16. `Iterator` **`iterator()`** - Returns an iterator over the elements in this list.
17. `ListIterator<E>` **`listIterator()`** - Returns a list iterator over the elements in this list (in proper sequence).
18. `ListIterator<E>` **`listIterator(int index)`** - Returns a list iterator over the elements in this list, starting at the specified position in the list.

### Methods for Query Operations

19. `boolean` **`isEmpty()`** - Check whether the list is empty or not.
20. `int` **`size()`** - Find the number of elements in the list.
21. `void` **`clear()`** - Remove all elements from the list.

### Methods to Convert List to Array

22. `Object[]` **`toArray()`** - To convert list to object array type.
23. `<T> T[]` **`toArray(T[] a)`** - To convert list to specified array type.

### Other Methods

24. `boolean` **`equals(Object o)`** - Compares the specified object with this list for equality. It returns `true` if the specified object is equal to this list.
25. `int` **`hashCode()`** - Returns the hash code value for this list.

---

## 3. List in Java Example

🛠️ **Java List example to demonstrate add and remove elements from the List:**

```java
import java.util.*;
public class ListTest1 {
   public static void main(String[] args) {

      List<String> l1 = new ArrayList<String>();
      l1.add("A");
      l1.add("B");
      l1.add("A");
      System.out.println("List 1: " + l1);

      // insert at 1 index
      l1.add(1, "Z");
      System.out.println("List 1: " + l1);

      List<String> l2 = new ArrayList<String>();
      l2.add("P");
      l2.add("Q");
      System.out.println("List 2: " + l2);

      // Add all element of l2 to l1
      l1.addAll(l2);
      System.out.println("List 1: " + l1);

      // remove from l1
      l1.remove("A");
      System.out.println("List 1: " + l1);
      l1.remove(3);
      System.out.println("List 1: " + l1);

      // remove all elements of l2 from l1
      l1.removeAll(l2);
      System.out.println("List 1: " + l1);
   }
}
```

📤 **Output:**

```
List 1: [A, B, A]
List 1: [A, Z, B, A]
List 2: [P, Q]
List 1: [A, Z, B, A, P, Q]
List 1: [Z, B, A, P, Q]
List 1: [Z, B, A, Q]
List 1: [Z, B, A]
```

🛠️ **List Example to Store Objects:**

List in Java Example with `Product` class: Here we have a product class with fields: PID (product id), name (product name), qty (product quantity), and price (product price). We have to store products into the List and display them.

**Product class:**

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
         + ", " + qty + ", " + price + "}\n";
   }
}
```

**Shop class:**

```java
import java.util.ArrayList;
import java.util.List;

public class Shop {
   public static void main(String[] args) {

      // ArrayList to store Products
      List<Product> al = new ArrayList<Product>();

      // Adding products to list
      al.add(new Product(123, "Laptop", 15, 2000));
      al.add(new Product(154, "Mobile", 30, 200));
      al.add(new Product(543, "Keyboard", 20, 30));
      // duplicate
      al.add(new Product(123, "Laptop", 15, 2000));

      // display list
      System.out.println(al);
   }
}
```

📤 **Output:**

```
[{123, Laptop, 15, 2000.0}
, {154, Mobile, 30, 200.0}
, {543, Keyboard, 20, 30.0}
, {123, Laptop, 15, 2000.0}
]
```

🛠️ **Java List example to get/set elements:**

```java
import java.util.ArrayList;
import java.util.List;

public class ListTest2 {
   public static void main(String[] args) {

      List<String> ls = new ArrayList<String>();
      ls.add("A");
      ls.add("B");
      ls.add("A");
      ls.add("C");
      ls.add("D");
      System.out.println(ls); // [A, B, A, C, D]

      // display list using get()
      for(int i=0; i<ls.size(); i++) {
         System.out.print(ls.get(i) + " ");
      }
      System.out.println(); // new line

      // get first occurrence of "A"
      System.out.println(ls.indexOf("A")); // 0
      // get last occurrence of "A"
      System.out.println(ls.lastIndexOf("A")); // 2

      // replace 3 index
      System.out.println(ls.set(3, "KP")); // C
      System.out.println(ls); // [A, B, A, KP, D]

      // sublist
      List<String> newlist = ls.subList(1, 3);
      System.out.println(newlist); // [B, A]
   }
}
```

📤 **Output:**

```
[A, B, A, C, D]
A B A C D
0
2
C
[A, B, A, KP, D]
[B, A]
```
