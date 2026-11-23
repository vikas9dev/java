# Enumeration Iterator ListIterator Cursor in Java

**Enumeration Iterator ListIterator Cursor in Java** | Three types of cursors to retrieve elements from all types of collection objects: Enumeration, Iterator, and ListIterator.

- [Enumeration Interface in Java](#enumeration-interface-in-java)
- [Iterator Interface in Java](#iterator-interface-in-java)
- [ListIterator Interface in Java](#listiterator-interface-in-java)
- [Comparison table of 3 Cursors](#comparison-table-of-3-cursors)

---

## 1. Overview

All these are interfaces. Their subclasses are created by SUN as inner classes inside collection classes. These subclass objects are returned via factory methods. These factory methods are also defined inside collection classes. So these factory methods must be called with the collection object from which we want to retrieve elements.

**The factory methods are:**

- 📜 `public Enumeration elements()` - To retrieve the Enumeration object. This method is defined inside both `Vector` and `Hashtable` classes.
- 🔄 `public Iterator iterator()` - To retrieve the Iterator object. It is defined in the `Collection` interface, and it is implemented in all subclasses. So it can be called on all Collection objects including `Vector`. We can't call it on `Hashtable` as it is not a subclass of Collection.
- 📋 `public ListIterator listIterator()`, `public ListIterator listIterator(int index)` - To retrieve ListIterator object. These methods are defined in the `List` interface. So these methods can be called only on List type collection objects.

**What are the operations we must perform using the above three cursor objects?**

- 🔍 Checking if elements are available in the underlying collection.
- 📥 If elements are available retrieve that element reference.

---

## 2. Enumeration Interface in Java

Enumeration is a legacy interface defined in Java 1.0 to retrieve elements from legacy collections `Vector` and `Hashtable`. It contains two methods:

- `public boolean hasMoreElements()`
- `public Object nextElement()`

💡 **Who implements the above two methods?** `Vector` and `Hashtable` classes implement them in inner classes.

**How can we obtain an Enumeration object on Vector and Hashtable?**

`Vector` class has below factory method: `public Enumeration elements()`

The `Hashtable` class has below two factory methods:

- `public Enumeration keys()` - It returns enumeration on all keys.
- `public Enumeration elements()` - It returns enumeration on all values.

🛠️ **Enumeration on Vector:**

```java
import java.util.Enumeration;
import java.util.Vector;

public class Test {
    public static void main(String[] args) {
        Vector<String> vector = new Vector<>();
        vector.add("A");
        vector.add("B");
        vector.add("C");
        vector.add("D");

        Enumeration<String> enumeration = vector.elements();
        while (enumeration.hasMoreElements()) {
            String string = enumeration.nextElement();
            System.out.print(string + " "); // A B C D
        }
    }
}
```

💡 **How can we obtain the Enumeration of collection framework classes?**
We can't obtain Enumeration on collection framework classes directly, we must use the `Collections` class static method `enumeration()`. Its prototype is: `public static Enumeration enumeration(Collection c)`

🛠️ **Enumeration on ArrayList:**

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Enumeration;
import java.util.List;

public class Test {
    public static void main(String[] args) {
        List<String> arrayList = new ArrayList<>();
        arrayList.add("A");
        arrayList.add("B");
        arrayList.add("C");
        arrayList.add("D");

        Enumeration<String> enumeration = Collections.enumeration(arrayList);
        while (enumeration.hasMoreElements()) {
            String string = enumeration.nextElement();
            System.out.print(string + " "); // A B C D
        }
    }
}
```

❌️ **Limitations of Enumeration:**

- We can apply the Enumeration concept only for legacy classes (`Vector`) & it is not a universal cursor available for all collection classes. To apply it to other classes we have to use the `enumeration()` method of the `Collections` class.
- By using Enumeration we can get only read access & we can't perform remove operation.
- To overcome the above limitations we should go for `Iterator`.

---

## 3. Iterator Interface in Java

Iterator is a collection framework interface defined in the Java 1.2 version. It is a cursor object used to retrieve elements from all collection type objects `List`, `Set`, `Queue` including `Vector`. It is an alternative to the Enumeration object and a replacement for the `for` loop on collection objects.

So from List objects, we can retrieve elements by using either Iterator or a for loop, but from Set objects, we can retrieve elements only by using Iterator.

- 🌐 We can apply the iterator concept for all collection objects & hence it is a **universal cursor**.
- 🔄 Using the iterator we can perform both **read and remove** operations.
- 📜 `Iterator(I)` was introduced in the 1.2 version.
- ⚙️ We can create an Iterator object by using the `iterator()` method of the `Collection` interface.

**The iterator interface provides below methods:**

1. `public boolean hasNext()`
2. `public Object next()`
3. `public void remove()`

💡 **Who implemented the above three methods?** All Collection subclasses in inner classes.

> ⚠️ **Iterator rules:**  
> - While retrieving elements, the collection object structure should not be modified by either adding elements or removing elements using collection object methods. After this modification if we call `itr.next()`, it leads to `java.util.ConcurrentModificationException`. This behavior is known as **fail-fast**.  
> - The `next()` method should not be called on an empty collection or empty location, it leads to runtime error: `java.util.NoSuchElementException`.  
> - The `remove()` method must be called only after the `next()` method call and only once, violation leads to `java.util.IllegalStateException`. We can't call the `remove()` method 2 times to remove only one element.

🛠️ **Iterator example:**

```java
import java.util.Iterator;
import java.util.LinkedHashSet;
import java.util.Set;

public class Test {
    public static void main(String[] args) {
        Set<String> lhs = new LinkedHashSet<String>();
        lhs.add("A");
        lhs.add("B");
        lhs.add("C");

        Iterator<String> itr = lhs.iterator();

        // itr.remove(); // java.lang.IllegalStateException
        String str1 = itr.next();
        System.out.println(str1); // A

        itr.remove();

        // lhs.add("Z"); // java.util.ConcurrentModificationException
        String str2 = itr.next();
        System.out.println(str2); // B

        String str3 = itr.next();
        System.out.println(str3); // C

        // String str4 = itr.next(); // java.util.NoSuchElementException
        itr.remove();

        lhs.add("KP");
        System.out.println(lhs); // [B, KP]

    }
}
```

📝 **Note:** Enumeration and Iterator both are fail-fast, so we can't modify the collection while iterating.

❌️ **Limitations of iterator:**

- By using Enumeration & Iterator we can always move only towards the **forward direction** and we can't move towards the backward direction. These are single-direction cursors but not bi-directional cursors.
- By using an iterator we can perform only **read & remove** operations. We can't perform the replacement & addition of new objects.
- To overcome the above limitations we should go for `ListIterator`.

---

## 4. ListIterator Interface in Java

- 🔄 Using ListIterator we can move either in the forward direction or the backward direction. Hence it is the **bi-directional cursor**.
- ⚙️ By using ListIterator we can perform **replacement & addition** operations of new objects in addition to read & remove operations.

We can create ListIterator by using the `listIterator()` method of the `List(I)` interface. Method prototype: `public ListIterator listIterator()`

ListIterator is the child interface of Iterator & hence all methods present in Iterator will be by default available to the ListIterator.

**ListIterator contains a total of 9 methods:**

- **Forward movement:**
  - `public boolean hasNext()`
  - `public Object next()`
  - `public int nextIndex()`
- **Backward movement:**
  - `public boolean hasPrevious()`
  - `public Object previous()`
  - `public int previousIndex()`
- **Extra Operations:**
  - `public void remove()`
  - `public void add(Object o)`
  - `public void set(Object o)`

🛠️ **ListIterator forward traversal with modifications:**

```java
import java.util.LinkedList;
import java.util.List;
import java.util.ListIterator;

public class Test {
    public static void main(String[] args) {
        List<String> linkedList = new LinkedList<String>();
        linkedList.add("A");
        linkedList.add("B");
        linkedList.add("C");
        linkedList.add("D");
        System.out.println(linkedList); // [A, B, C, D]

        ListIterator<String> litr = linkedList.listIterator();

        while (litr.hasNext()) {
            String str = litr.next();
            if (str.equals("A"))
                litr.remove();
            else if (str.equals("B"))
                litr.add("E");
            else if (str.equals("C"))
                litr.set("F");
        }
        System.out.println(linkedList); // [B, E, F, D]
    }
}
```

🛠️ **ListIterator retrieving in reverse order:**

```java
import java.util.LinkedList;
import java.util.List;
import java.util.ListIterator;

public class Test {
    public static void main(String[] args) {
        List<String> ll = new LinkedList<String>();
        ll.add("A");
        ll.add("B");
        ll.add("C");
        ll.add("D");

        ListIterator<String> litr = ll.listIterator();
        litr.next();
        litr.next();

        while (litr.hasPrevious()) {
            String str = litr.previous();
            System.out.print(str + " "); // B A
        }
    }
}
```

📝 **Note:** The most powerful cursor is ListIterator but its limitation is: it is applicable only for List objects.

---

## 5. Comparison table of 3 Cursors

| Property 📋 | Enumeration 📜 | Iterator 🔄 | ListIterator 📋 |
|------------|--------------|-----------|----------------|
| **Where to apply?** | Mainly for legacy classes | Any collection object | Only for List objects |
| **Introduced in** | 1.0v | 1.2v | 1.2v |
| **Movement** | Single direction (forward only) | Single direction (forward only) | Bi-directional |
| **Operations** | Read only | Read / Remove | Read / Remove / Replace / Add |
| **How to get it?** | `elements()` method of Vector/Hashtable or `enumeration()` of Collections class | `iterator()` method of Collection(I) | `listIterator()` method of List(I) |
| **Methods** | 2: `hasMoreElements()`, `nextElement()` | 3: `hasNext()`, `next()`, `remove()` | 9 methods |
| **Behavior** | Fail-Safe | Fail-Fast | Fail-Fast |

🛠️ **Verifying cursor implementation classes:**

```java
import java.util.Enumeration;
import java.util.Iterator;
import java.util.ListIterator;
import java.util.Vector;

public class Test {
    public static void main(String[] args) {
        Vector<String> vector = new Vector<>();
        Enumeration<String> enumeration = vector.elements();
        Iterator<String> iterator = vector.iterator();
        ListIterator<String> listIterator = vector.listIterator();
        System.out.println(enumeration.getClass().getName()); // java.util.Vector$1
        System.out.println(iterator.getClass().getName()); // java.util.Vector$Itr
        System.out.println(listIterator.getClass().getName()); // java.util.Vector$ListItr
    }
}
```
