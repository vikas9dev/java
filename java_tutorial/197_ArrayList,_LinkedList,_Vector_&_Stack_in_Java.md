# ArrayList, LinkedList, Vector & Stack in Java

**ArrayList, LinkedList, Vector & Stack in Java** | The ArrayList, LinkedList, Vector, and Stack implement the [List interface](195_List_Interface_in_Java.md), and indirectly implement the [Collection interface](194_Java_Collection_Interface.md). This post will show examples of the List interface implementation classes with constructors and sample programs.

- [ArrayList Class in Java](#arraylist-class-in-java)
- [Array vs ArrayList in Java](#array-vs-arraylist-in-java)
- [LinkedList Class in Java](#linkedlist-class-in-java)
- [LinkedList vs ArrayList in Java](#linkedlist-vs-arraylist-in-java)
- [Vector Class in Java](#vector-class-in-java)
- [Stack Class in Java](#stack-class-in-java)
- [ArrayList vs Vector in Java](#arraylist-vs-vector-in-java)
- [synchronizedList() in Java](#synchronizedlist-in-java)
- [RandomAccess Interface](#randomaccess-interface)

---

## 1. ArrayList Class in Java

- ⚙️ It is non-synchronized & non-thread-safe.
- 🏗️ The underlying data structure is a resizable array or growable array.
- ✅ Duplicate objects are allowed.
- 📋 Insertion order is preserved.
- 📦 Heterogeneous objects are allowed.
- 🔓 Null insertion is possible. We can insert it any number of times.
- 📏 Default capacity = 10
- 🏷️ ArrayList implements the `Serializable`, `Cloneable`, and `RandomAccess` interfaces.

It has dynamic resizing - 50% of the original size. Whenever the ArrayList is full and we try to add more elements then it resizes to 50% of the original size.

### Constructors of ArrayList Class in Java

1. **`ArrayList list = new ArrayList();`** It creates an empty ArrayList object with a default initial capacity of 10. Once ArrayList reaches its max capacity then a new ArrayList object will be created with 50% of the original size.
2. **`ArrayList list = new ArrayList(int initialCapacity);`** It creates an empty ArrayList object with the specified initial capacity.
3. **`ArrayList list = new ArrayList(Collection c);`** It creates an equivalent ArrayList object for the given Collection. It is used to convert one Collection object type to an ArrayList type.

🛠️ **ArrayList example:**

```java
import java.util.ArrayList;
import java.util.List;

public class Test {
   public static void main(String[] args) {
      List<Object> list = new ArrayList<>();
      list.add("A");
      list.add(10);
      list.add("A");
      list.add(null);
      System.out.println(list); // [A, 10, A, null]

      list.remove(2);
      System.out.println(list); // [A, 10, null]

      list.add(2, "M");
      list.add("N");
      System.out.println(list); // [A, 10, M, null, N]
   }
}
```

> 💡 **Tip:** ArrayList is the best choice if our frequent operation is a retrieval operation because ArrayList implements the `RandomAccess` interface. ArrayList is the worst choice if our frequent operation is insertion/deletion in the middle. In that case, we should go for LinkedList.

---

## 2. Array vs ArrayList in Java

| Feature | Array 🅰️ | ArrayList 📋 |
|---------|----------|-------------|
| **Size** | Static, fixed-length | Variable length, growable |
| **Data Types** | Can store both objects and primitives | Cannot store primitives (auto-converts to wrapper) |
| **Performance** | Fast due to fixed size | `resize()` can slow down; `add()`/`get()` run in constant time |
| **Initialization** | Mandatory to provide size while initializing | Can create without specifying size (default 10) |
| **Iteration** | `for` loop or `for-each` loop | Can also use `Iterator` |
| **Size Check** | `length` variable | `size()` method |
| **Dimensions** | Can be multi-dimensional | Always single-dimensional |
| **Memory Layout** | Elements in adjacent memory locations | Objects not guaranteed in contiguous locations |
| **Element Storage** | Assignment operator (`=`) | `add()` method |
| **Generics** | ❌️ Not compatible | ✅ Supports Generics |

---

## 3. LinkedList Class in Java

- 🔗 The underlying data structure is a doubly linked list.
- 📋 Insertion order is preserved.
- ✅ Duplicate objects are allowed.
- 📦 Heterogeneous objects are allowed.
- 🔓 Null insertion is possible. We can insert a null value any number of times.
- ⚡ LinkedList is the best choice if our frequent operation is insertion/deletion in the middle.
- 🐢 LinkedList is the worst choice if our frequent operation is a retrieval operation because LinkedList doesn't implement the `RandomAccess` interface. In that case, we should go for ArrayList.
- 🏷️ LinkedList implements the `Serializable` & `Cloneable` interface but not the `RandomAccess` interface.

### Constructors of LinkedList Class in Java

Capacity is not applicable for LinkedList therefore it doesn't contain such constructor.

1. **`LinkedList list = new LinkedList();`** It creates an empty LinkedList object.
2. **`LinkedList list = new LinkedList(Collection c);`** It creates an equivalent LinkedList object for the given Collection.

**LinkedList Class-specific methods:**

Usually, we use LinkedList to develop Stack & Queue. To provide support for this requirement LinkedList class defines the following specific methods:

- `void` **`addFirst`**`(Object o)`
- `void` **`addLast`**`(Object o)`
- `Object` **`getFirst`**`()`
- `Object` **`getLast`**`()`
- `Object` **`removeFirst`**`()`
- `Object` **`removeLast`**`()`

🛠️ **LinkedList example:**

```java
import java.util.LinkedList;

public class Test {
    public static void main(String[] args) {
        LinkedList<Object> list = new LinkedList<>();
        list.add("Know"); // String
        list.add(30); // number
        list.add(null); // null value
        list.add("Know"); // duplicate value
        System.out.println(list); // [Know, 30, null, Know]

        list.set(0, "Program"); // [Program, 30, null, Know]
        System.out.println(list);

        list.add(0, "Hello");
        list.removeLast();
        list.addFirst("Java");
        System.out.println(list); // [Java, Hello, Program, 30, null]
    }
}
```

---

## 4. LinkedList vs ArrayList in Java

| Feature | ArrayList 📋 | LinkedList 🔗 |
|---------|-------------|--------------|
| **Data Structure** | Growable array (dynamic array) | Doubly linked list |
| **Memory Layout** | Elements in consecutive memory locations | Elements not in consecutive memory locations |
| **RandomAccess** | ✅ Implements `RandomAccess` | ❌️ Does not implement `RandomAccess` |
| **Interfaces** | Implements `List` | Implements `List` as well as `Queue` |
| **Manipulation** | 🐢 Slow (shifting required on remove) | ⚡ Fast (no bit shifting in memory) |
| **Access Speed** | ⚡ Faster (random access) | 🐢 Slower (node-by-node traversal) |
| **descendingIterator()** | ❌️ Not available | ✅ Available |
| **Default Capacity** | 10 | No default capacity |
| **Memory Overhead** | Less (only holds actual data) | More (maintains next and previous node addresses) |
| **Best For** | Retrieval operations | Insertion/deletion in the middle |
| **Worst For** | Insertion/deletion in the middle | Retrieval operations |

If our application has many retrievals/access compared to manipulation operations (insert/delete/update) in that case ArrayList is better else use LinkedList.

> 🔑 **Key Point:** LinkedList element deletion and addition is faster compared to ArrayList. LinkedList's every element maintains two pointers (addresses) which point to both neighbor elements in the list. Hence removal only requires a change in the pointer location in the two neighbor nodes of the node that is going to be removed. In ArrayList, all the elements need to be shifted to fill out the space created by the removed element.

---

## 5. Vector Class in Java

- 🔒 Every method present in the Vector class is synchronized and hence Vector is thread-safe.
- 🏗️ The underlying data structure is a resizable array or growable array.
- ✅ Duplicate objects are allowed.
- 📋 Insertion order is preserved.
- 📦 Heterogeneous objects are allowed.
- 🔓 Null insertion is possible, there is no restriction on the number of nulls.
- 📏 Default capacity = 10
- 🏷️ Like ArrayList, Vector also implements the `Serializable`, `Cloneable`, and `RandomAccess` interfaces.

It has dynamic resizing - 100% of the original size. Whenever the Vector is full and we try to add more elements then it resizes to 100% of the original size.

### Constructors of Vector Class in Java

1. **`Vector vector = new Vector();`** It creates an empty vector object with a default initial capacity of 10, once the vector reaches its maximum capacity then a new vector object will be created with 100% of the original size.
2. **`Vector vector = new Vector(int initialCapacity);`** It creates an empty vector object with a specified initial capacity.
3. **`Vector vector = new Vector(int initialCapacity, int incrementalCapacity);`** It creates an empty vector object with a specified initial capacity. Once the vector reaches its max capacity, it will increase "incremental capacity".
4. **`Vector vector = new Vector(Collection c);`** It creates an equivalent vector object for the given collection. This constructor is meant for interconversion between collection objects.

### Vector Specific Methods

**To add objects:**

1. `add(Object o)` => from Collection(I)
2. `add(int index, Object o)` => from List(I)
3. `addElement(Object o)` => from Vector

**To remove objects:**

1. `remove(Object o)` => from Collection(I)
2. `remove(int index)` => from List(I)
3. `removeElement(Object o)` => from Vector
4. `removeElementAt(int index)` => from Vector
5. `clear()` => from Collection
6. `removeAllElements()` => from Vector

**To get Objects:**

1. `Object get(int index)` => from List(I)
2. `Object elementAt(int index)` => from Vector
3. `Object firstElement()` => from Vector
4. `Object lastElement()` => from Vector

**Other Methods:**

1. `int size()`
2. `int capacity()`
3. `Enumeration elements()`

🛠️ **Vector example:**

```java
import java.util.Vector;

public class Test {
    public static void main(String[] args) {
        Vector<Object> vector = new Vector<>();
        System.out.println(vector.capacity()); // 10

        for (int i = 1; i <= 10; i++) {
            vector.addElement(i);
        }
        System.out.println(vector.capacity()); // 10

        vector.addElement("A");
        System.out.println(vector.capacity()); // 20

        System.out.println(vector); // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, A]
    }
}
```

---

## 6. Stack Class in Java

The stack class represents a last in first out (LIFO) stack of objects. It extends the `Vector` class with five operations that allow a vector to be treated as a stack. The usual push and pop operations are provided, as well as a method to peek at the top item on the stack. When a stack is first created, it contains no items.

- 📦 It is the child class of `Vector`.
- 🏗️ It is specially designed for LIFO (Last in first out) order.

**Constructor:** `Stack stack = new Stack();`

**Stack Class specific methods:**

- `Object` **`push`**`(Object o)` - To insert an object into the stack.
- `Object` **`pop`**`()` - To remove & return the top of the stack.
- `Object` **`peek`**`()` - To return the top of the stack without removal.
- `boolean` **`empty`**`()` - Returns `true` if the stack is empty.
- `int` **`search`**`(Object o)` - Returns offset if the element is available otherwise returns -1.

`public synchronized int search(Object o)` - It returns the 1-based position where an object is on this stack. If an object occurs as an item in this stack, this method returns the distance from the top of the stack. The topmost item on the stack is considered to be at distance 1. The `equals` method is used to compare `o` to the items in this stack. If they are not there in the stack it returns -1.

🛠️ **Stack example:**

```java
import java.util.Stack;

public class Test {
    public static void main(String[] args) {
        Stack<String> st = new Stack<String>();
        st.push("A");
        st.push("B");
        st.push("C");
        System.out.println(st); // [A, B, C]

        System.out.println(st.search("A")); // 3
        System.out.println(st.search("Z")); // -1

    }
}
```

| Offset 🔢 | Element 📋 | Index 🏷️ |
|-----------|-----------|----------|
| **1** | C | 2 |
| **2** | B | 1 |
| **3** | A | 0 |

---

## 7. ArrayList vs Vector in Java

| Feature | ArrayList 📋 | Vector 🔒 |
|---------|-------------|----------|
| **Synchronization** | ❌️ Non-synchronized | ✅ Synchronized |
| **Thread Safety** | ❌️ Not thread-safe (multiple threads can operate) | ✅ Thread-safe (only one thread at a time) |
| **Speed** | ⚡ Fast | 🐢 Slow |
| **Performance** | High (threads don't wait) | Low (threads wait) |
| **Legacy** | Not a legacy class (JDK 1.2) | Legacy class (1.0 version) |
| **Resize** | 50% of current array size | 100% (doubles) of current array size |
| **Traversal** | Uses `Iterator` | Uses `Iterator` or `Enumeration` |

---

## 8. synchronizedList() in Java

💡 **How to get the Synchronized version of the ArrayList object?** By default ArrayList is non-synchronized but we can get the synchronized version of the ArrayList object by using the `synchronizedList()` method of the `Collections` class. Method signature: **`public static List synchronizedList(List l)`**

```java
List<String> arrayList = new ArrayList<>();
List<String> synchronizedArrayList = Collections.synchronizedList(arrayList);
```

- 🔒 **How to get the synchronized version of the Set object?** Using **`Collections.synchronizedSet()`**. Method Signature: `public static List synchronizedSet(Set s)`
- 🔒 **How to get the synchronized version of the Map object?** Using **`Collections.synchronizedMap()`**. Method Signature: `public static List synchronizedMap(Map m)`

---

## 9. RandomAccess Interface

`RandomAccess` interface present in `java.util` package & it doesn't contain any methods. It is a marker interface where the required ability will be provided by the JVM. **ArrayList & Vector classes implement the RandomAccess interface** for any random element we can access with the same speed.

Usually, we use Collections to hold & transfer objects from one location to another location (container). To provide support for this requirement **every collection class by default implements Serializable and Cloneable interfaces.**

🛠️ **RandomAccess verification:**

```java
import java.io.Serializable;
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;
import java.util.RandomAccess;

public class Test {
    public static void main(String[] args) {
        List<String> arrayList = new ArrayList<>();
        List<String> linkedList = new LinkedList<>();

        System.out.println(arrayList instanceof Serializable); // true
        System.out.println(linkedList instanceof Cloneable); // true

        System.out.println(arrayList instanceof RandomAccess); // true
        System.out.println(linkedList instanceof RandomAccess); // false
    }
}
```
