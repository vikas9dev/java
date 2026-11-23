# HashSet LinkedHashSet TreeSet in Java

**HashSet, LinkedHashSet, and TreeSet in Java** | HashSet, LinkedHashSet, SortedSet, and TreeSet implement the Set interface and indirectly implement the [Collection interface](194_Java_Collection_Interface.md).

- [HashSet Class in Java](#hashset-class-in-java)
- [LinkedHashSet Class in Java](#linkedhashset-class-in-java)
- [HashSet vs LinkedHashSet](#hashset-vs-linkedhashset)
- [SortedSet Interface in Java](#sortedset-interface-in-java)
- [TreeSet Class In Java](#treeset-class-in-java)
- [Null Acceptance in TreeSet](#null-acceptance-in-treeset)
- [ClassCastException in TreeSet](#classcastexception-in-treeset)
- [Comparison Table of Set Interface Implemented Classes](#comparison-table-of-set-interface-implemented-classes)

---

## 1. Overview

Previously we have seen [List interface](195_List_Interface_in_Java.md) implementation classes [ArrayList, LinkedList, Vector, and Stack](197_ArrayList,_LinkedList,_Vector_&_Stack_in_Java.md). This post will show examples of the Set interface implementation classes with constructors, and sample programs.

- Set(I) 1.2v
  - HashSet 1.2v
    - LinkedHashSet 1.4v
  - SortedSet(I) 1.2v
    - NavigableSet(I) 1.6v
      - TreeSet 1.2v

The Set is a child interface of the Collection Interface. Suppose we want to represent a group of individual objects as a single entity **where duplicates are not allowed** in that case we can use Set. The Set interface doesn't contain any new methods & we have to use only [Collection interface](194_Java_Collection_Interface.md) methods.

---

## 2. HashSet Class in Java

- #️⃣ The underlying data structure is a hash table.
- ❌️ Duplicate objects are not allowed.
- 🔀 Insertion order is not preserved and is based on the object's hashcode.
- 🔓 Null insertion is possible but only once.
- 📦 Heterogeneous objects are allowed.
- 🏷️ It implements `Serializable` and `Cloneable` marker interfaces but not the `RandomAccess` interface.
- 🔍 HashSet is the best choice if our frequent operation is a search operation.

**Constructors in HashSet Class:**

1. **`HashSet hashset = new HashSet();`** It creates an empty HashSet object with a default initial capacity of 16 and a default fill ratio of 0.75.
2. **`HashSet hashset = new HashSet(int initialCapacity);`** It creates an empty HashSet object with a specified initial capacity and default fill ratio of 0.75.
3. **`HashSet hashset = new HashSet(int initialCapacity, float fillRatio);`**
4. **`HashSet hashset = new HashSet(Collection c);`** It creates an equivalent HashSet for the given Collection. This constructor is meant for interconversion between Collection objects.

📝 **Note:** The other collection classes whose underlying data structure is a hash table also contain these 4 constructors.

💡 **What is the fill ratio or load factor?** After filling how much ratio a new HashSet object will be created, this ratio is called fill ratio or load factor. For example: fill ratio of 0.75 means after filling the 75% ratio a new HashSet object will be created.

🛠️ **HashSet example:**

```java
import java.util.HashSet;
import java.util.Set;
public class Test {
    public static void main(String[] args) {
        Set<Object> hashSet = new HashSet<>();
        hashSet.add("A");
        hashSet.add("B");
        hashSet.add("C");
        hashSet.add("Z");
        hashSet.add(null);
        hashSet.add(10);
        System.out.println(hashSet); // [null, A, B, C, Z, 10]
    }
}
```

🛠️ **What will happen if we try to insert duplicate values?** In HashSet, duplicates are not allowed. If we are trying to insert a duplicate then we won't get any compile time or run time error and the `add()` method simply returns a `false` value & the value won't be inserted.

```java
import java.util.HashSet;
import java.util.Set;
public class Test {
    public static void main(String[] args) {
        Set<String> set = new HashSet<>();
        System.out.println(set.add("Java")); // true
        System.out.println(set.add("Java")); // false
        System.out.println(set); // [Java]
    }
}
```

---

## 3. LinkedHashSet Class in Java

LinkedHashSet is the child class of the HashSet class. It contains the same constructors and methods as HashSet. The most important difference between HashSet and LinkedHashSet is: **LinkedHashSet preserves the insertion order**. It is an ordered version of HashSet that maintains a **doubly linked List** across all elements.

🛠️ **LinkedHashSet example:**

```java
import java.util.LinkedHashSet;
import java.util.Set;
public class Test {
    public static void main(String[] args) {
        Set<Object> linkedHashSet = new LinkedHashSet<>();
        linkedHashSet.add("A");
        linkedHashSet.add("B");
        linkedHashSet.add("C");
        linkedHashSet.add("Z");
        linkedHashSet.add(null);
        linkedHashSet.add(10);
        System.out.println(linkedHashSet); // [A, B, C, Z, null, 10]
    }
}
```

💡 **Tip:** In general we can use LinkedHashSet to develop cache-based applications where duplicates are not allowed & insertion order is preserved.

---

## 4. HashSet vs LinkedHashSet

| Feature | HashSet #️⃣ | LinkedHashSet 🔗 |
|---------|-----------|-----------------|
| **Data Structure** | Hash table | Combination of linked list and hash table |
| **Insertion Order** | ❌️ Not preserved | ✅ Preserved |
| **Version** | Introduced in 1.2 | Introduced in 1.4 |

---

## 5. SortedSet Interface in Java

SortedSet is the child interface of the Set interface. If we want to represent a group of individual objects according to some sorting order without duplicates then we should go for SortedSet.

**SortedSet(I) defines the following specific methods:**

- `Object first()` - It returns the first element of the SortedSet.
- `Object last()` - It returns the last element of the SortedSet.
- `SortedSet headSet(Object obj)` - It returns SortedSet whose elements are < obj.
- `SortedSet tailSet(Object obj)` - It returns SortedSet whose elements are >= obj.
- `SortedSet subSet(Object obj1, Object obj2)` - Returns SortedSet whose elements are >= obj1 & < obj2 (obj1 is inclusive, obj2 is exclusive).
- `Comparator comparator()` - It returns a comparator object that describes the underlying sorting technique. If we are using the default natural sorting order then we will get `null`.

The default natural order for:

- 🔢 **Number:** Ascending order
- 🔤 **String:** Alphabetical order

🛠️ **Example:** `[100, 101, 104, 106, 110, 115, 120]`

- `first()` => 100
- `last()` => 120
- `headSet(106)` => [100, 101, 104]
- `tailSet(106)` => [110, 115, 120]
- `subSet(101, 115)` => [101, 104, 106, 110]

---

## 6. TreeSet Class In Java

- 🌳 The underlying data structure is a balanced tree.
- ❌️ Duplicate objects are not allowed.
- 🔀 Insertion order is not preserved.
- 🚨 **Heterogeneous objects are not allowed** otherwise we will get the runtime exception: `ClassCastException`
- 🚫 Null insertion is not possible. (Before the 1.7 version, null insertion was possible but only once & at the beginning.)
- 🏷️ TreeSet implements `Serializable` and `Cloneable` marker interfaces but not the `RandomAccess` interface.
- ⚖️ All objects will be inserted based on some sorting order. It may be a default natural sorting order or a customized sorting order.

> 📝 **Note:** In all Collection classes, `TreeSet` and `TreeMap` are the only classes which don't allow the storing of heterogeneous objects because they require comparison of each object therefore objects must be the same type.

**Constructors of the TreeSet class:**

Similar constructors exist for `TreeMap` and `SortedMap`.

- **`TreeSet treeSet = new TreeSet();`** It creates an empty TreeSet object where the elements will be inserted according to the default natural sorting order.
- **`TreeSet treeSet = new TreeSet(Comparator c);`** It creates an empty TreeSet object where the elements will be inserted according to the customized sorting order specified by the comparator object.
- **`TreeSet treeSet = new TreeSet(Collection c);`**
- **`TreeSet treeSet = new TreeSet(SortedSet s);`**

🛠️ **TreeSet example:**

```java
import java.util.TreeSet;
public class Test {
    public static void main(String[] args) {
        TreeSet<String> treeSet = new TreeSet<>();
        treeSet.add("A");
        treeSet.add("a");
        treeSet.add("B");
        treeSet.add("Z");
        treeSet.add("L");
        System.out.println(treeSet); // [A, B, L, Z, a]
    }
}
```

The ASCII value of "a" is 97, ASCII value of "A" to "Z" is less than 97 therefore "a" will be inserted at last. Here elements are inserted based on ASCII value.

---

## 7. Null Acceptance in TreeSet

1. For a non-empty TreeSet, if we are trying to insert a null value then we will get `NullPointerException`.

```java
import java.util.TreeSet;

public class Test {
    public static void main(String[] args) {
        TreeSet<String> treeSet = new TreeSet<>();
        treeSet.add("A");
        treeSet.add(null); // java.lang.NullPointerException
        System.out.println(treeSet);
    }
}
```

2. From the 1.7 version onwards null insertion is not possible.
3. Before the 1.7 version, for empty TreeSet, null insertion was allowed as 1st element. But after inserting the null value if we try to insert any other value then we get the `NullPointerException`.

> ⚠️ **Caution:** The previously inserted value & newly inserted value (null) will be compared with each other. Hence it gives `NullPointerException`. Until the 1.6 version null was allowed as the 1st element to the empty TreeSet but from 1.7v onwards null is not allowed even as the 1st element.

---

## 8. ClassCastException in TreeSet

```java
import java.util.TreeSet;

public class Test {
    public static void main(String[] args) {
        TreeSet<A> treeSet = new TreeSet<>();
        treeSet.add(new A("Java")); // java.lang.ClassCastException
        treeSet.add(new A("Know"));
        treeSet.add(new A("Program"));
        System.out.println(treeSet);
    }
}

public class A {
    String a;

    A(String a) {
        this.a = a;
    }
}
```

It gives: `Exception in thread "main" java.lang.ClassCastException: class A cannot be cast to class java.lang.Comparable`

If we are depending on the default natural sorting order then the **object must be homogeneous & comparable** otherwise it gives runtime exception: `ClassCastException`.

An object is said to be comparable if & only if the corresponding class **implements a Comparable interface**. For example: `String`, `StringBuffer`, `StringBuilder`, and all Wrapper classes already implement the `Comparable` interface. See more: Comparable and Comparator Interface in Java.

---

## 9. Comparison Table of Set Interface Implemented Classes

| Properties 📋 | HashSet #️⃣ | LinkedHashSet 🔗 | TreeSet 🌳 |
|--------------|-----------|-----------------|-----------|
| **Data Structure** | Hash table | Linked list + hash table | Balanced tree |
| **Duplicates** | ❌️ Not allowed | ❌️ Not allowed | ❌️ Not allowed |
| **Insertion Order** | ❌️ Not preserved | ✅ Preserved | ❌️ Not preserved |
| **Sorting Order** | ❌️ Not applicable | ❌️ Not applicable | ✅ Applicable |
| **Heterogeneous Objects** | ✅ Allowed | ✅ Allowed | ❌️ Not allowed |
| **Null Acceptance** | ✅ Allowed (only once) | ✅ Allowed (only once) | ❌️ Not allowed (after 1.7v) |
