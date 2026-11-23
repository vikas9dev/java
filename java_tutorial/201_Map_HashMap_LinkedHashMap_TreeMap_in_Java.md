# Map HashMap LinkedHashMap TreeMap in Java

**Map HashMap LinkedHashMap TreeMap in Java** | We have seen the [Collection overview](192_Java_Collection_Framework_Overview.md), [List Interface](195_List_Interface_in_Java.md), and Set implementation classes. Here we will discuss the Map interface and its implementation classes with constructors, methods, and examples.

- [Map Interface Methods](#map-interface-methods)
- [Entry Interface](#entry-interface)
- [HashMap Interface in Java](#hashmap-interface-in-java)
- [LinkedHashMap Interface in Java](#linkedhashmap-interface-in-java)
- [IdentityHashMap Class In Java](#identityhashmap-class-in-java)
- [WeakHashMap Class In Java](#weakhashmap-class-in-java)
- [SortedMap Interface in Java](#sortedmap-interface-in-java)
- [TreeMap Class in Java](#treemap-class-in-java)
- [Hashtable Class in Java](#hashtable-class-in-java)
- [HashMap vs Hashtable](#hashmap-vs-hashtable)
- [Properties Class in Java](#properties-class-in-java)

---

## 1. Overview

- Map(I) _1.2v_
  - HashMap _1.2v_
    - LinkedHashMap _1.4v_
  - WeakHashMap _1.2v_
  - IdentityHashMap _1.4v_
  - Hashtable _1.0v_
    - Properties _1.0v_
  - SortedMap(I) _1.2v_
    - NavigableMap(I) _1.6v_
      - TreeMap _1.2v_

`Hashtable` implements `Map(I)` and extends the `Dictionary` abstract class. They were introduced in 1.0v therefore they are considered legacy classes.

- Dictionary(AC) 1.0v
  - Hashtable 1.0v
    - Properties 1.0v

🔑 **Key Points:**

- 🗺️ The Map interface is **not** a child of the `Collection` interface.
- 📦 If we want to represent a group of objects as a key-value pair then we should go for Map.

| Key 🔑 | Value 📋 |
|--------|---------|
| **101** | Java |
| **102** | C++ |
| **103** | Spring |
| **104** | Python |

Important Points about the Map:

- 🔑 Both keys & values can be any object.
- ❌️ Duplicate keys are not allowed but values can be duplicated.
- 📋 Each key-value pair is called an Entry. Hence Map is considered as a collection of Entry objects.

---

## 2. Map Interface Methods

1. `Object` **`put`**`(Object key, Object value)` - To add one key-value pair to the Map. If the key is already present then the old value will be replaced with a new value and return the old value.

🛠️ **put() example:**

```java
import java.util.HashMap;
import java.util.Map;

public class Test {
    public static void main(String[] args) {
        Map<Integer, String> hashMap = new HashMap<>();
        System.out.println(hashMap.put(1, "Go")); // null
        System.out.println(hashMap.put(2, "C++")); // null
        System.out.println(hashMap.put(1, "Python")); // Go
    }
}
```

In the first two lines keys are unique therefore Entries are stored to the Map and the `put()` method returns the `null` value, but in the third line key=1 already exists therefore its value will be replaced with a new passed value "Python", and existing value "Go" is returned.

2. `void putAll(Map m)`
3. `Object get(Object key)` - Returns the value associated with the specified key.
4. `Object remove(Object key)` - Removes the entry associated with the specified key.
5. `boolean containsKey(Object key)`
6. `boolean containsValue(Object value)`
7. `boolean isEmpty()`
8. `int size()`
9. `void clear()`

**Other methods (Collection views of Map):**

10. `Set keySet()` - To get all keys of the Map.
11. `Collection values()` - To get all values of the Map.
12. `Set entrySet()` - To get Entry as Set.

---

## 3. Entry Interface

The Map interface contains the inner interface `Entry`. It has several methods like `getKey()`, `getValue()`, etc.

A map is a group of key-value pairs and each key-value pair is called an Entry. Hence Map is considered as Collection of Entry objects. Without an existing Map object, there is no chance of existing `Entry(I)` hence `Entry(I)` is defined inside `Map(I)`.

```java
interface Map {
   interface Entry {
      Object getKey();
      Object getValue();
      Object setValue(Object newo);
      // other methods
   }
}
```

These methods are specific & we can apply only on the Entry object.

---

## 4. HashMap Interface in Java

- #️⃣ The underlying data structure is a hash table.
- 🔀 Insertion order is not preserved & it is based on the hashcode of keys.
- ❌️ Duplicate keys are not allowed but values can be duplicated.
- 📦 Heterogeneous objects are allowed for both keys & values.
- 🔓 Null is allowed for the key but only once. Null is allowed for values (any number of times).
- 🏷️ It implements `Serializable` & `Cloneable` but not `RandomAccess`.
- 🔍 HashMap is the best choice if our frequent operation is a search operation.

**Constructors in HashMap Class:**

1. **`HashMap map = new HashMap();`** It creates an empty HashMap object with a default initial capacity of 16 & default fill ratio of 0.75.
2. **`HashMap map = new HashMap(int initialCapacity);`** It creates an empty HashMap object with a specified initial capacity & default fill ratio of 0.75.
3. **`HashMap map = new HashMap(int initialCapacity, float fillRatio);`**
4. **`HashMap map = new HashMap(Map m);`**

🛠️ **HashMap example with Entry iteration:**

```java
import java.util.Collection;
import java.util.HashMap;
import java.util.Iterator;
import java.util.Map;
import java.util.Map.Entry;
import java.util.Set;

public class Test {
    public static void main(String[] args) {
        Map<Integer, String> hashMap = new HashMap<>();
        hashMap.put(101, "Java");
        hashMap.put(102, "C++");
        hashMap.put(103, "Python");
        hashMap.put(104, "JavaScript");
        System.out.println(hashMap); // {101=Java, 102=C++, 103=Python, 104=JavaScript}

        // display all keys
        Set<Integer> keys = hashMap.keySet();
        System.out.println(keys); // [101, 102, 103, 104]

        // display all values
        Collection<String> values = hashMap.values();
        System.out.println(values); // [Java, C++, Python, JavaScript]

        // display Entry
        Set<Entry<Integer, String>> entries = hashMap.entrySet();
        System.out.println(entries); // [101=Java, 102=C++, 103=Python, 104=JavaScript]

        Iterator<Entry<Integer, String>> iterator = entries.iterator();
        while (iterator.hasNext()) {
            Map.Entry<Integer, String> entry = iterator.next();
            System.out.println(entry.getKey() + ".." + entry.getValue());

            // update
            if (entry.getKey().equals(102)) {
                entry.setValue("C#");
            }
        }
        System.out.println(hashMap); // {101=Java, 102=C#, 103=Python, 104=JavaScript}
    }
}
```

💡 **How to get the synchronized version of the HashMap object?** By default HashMap object is non-synchronized but we can get its synchronized version using the `synchronizedMap()` method of the `Collections` class. Method signature: `public static Map synchronizedMap(Map m)`

```java
Map<Integer, String> hashMap = new HashMap<>();
Map<Integer, String> synchronizedMap = Collections.synchronizedMap(hashMap);
```

---

## 5. LinkedHashMap Interface in Java

- 🔗 It is the child class of HashMap.
- ⚙️ It is exactly the same as HashMap (including methods and constructor) except for the following differences:

| Feature | HashMap #️⃣ | LinkedHashMap 🔗 |
|---------|-----------|-----------------|
| **Data Structure** | Hash table | Combination of linked list and hash table |
| **Insertion Order** | ❌️ Not preserved (based on hashcode) | ✅ Preserved |
| **Version** | Introduced in 1.2 | Introduced in 1.4 |

💡 **Tip:** LinkedHashSet and LinkedHashMap are commonly used for developing cache-based applications.

🛠️ **LinkedHashMap example:**

```java
import java.util.LinkedHashMap;
import java.util.Map;

public class Test {
    public static void main(String[] args) {
        Map<Integer, String> hashMap = new LinkedHashMap<>();
        hashMap.put(101, "Java");
        hashMap.put(102, "C++");
        hashMap.put(103, "Python");
        hashMap.put(104, "JavaScript");
        System.out.println(hashMap);
        // {101=Java, 102=C++, 103=Python, 104=JavaScript}
    }
}
```

---

## 6. IdentityHashMap Class In Java

Before diving into the `IdentityHashMap` class, first let us see a quick difference between the `==` operator and the `equals()` method. In general, the `==` operator is meant for reference comparison (address comparison) whereas the `equals()` method is meant for content comparison. The default implementation of the `equals()` method in `Object` performs reference comparison but all wrapper classes (`Integer`, `Double`, `Long`, etc) and `String` class overridden the `equals()` method for content comparison.

```java
Integer i1 = new Integer(10);
Integer i2 = new Integer(10);
System.out.println(i1 == i2); // false
System.out.println(i1.equals(i2)); // true
```

`IdentityHashMap` is exactly the same as `HashMap` (including methods and constructors) except for the following differences:

- 🔍 In `HashMap`, JVM will use the `equals()` method to identify duplicate keys. The `equals()` method is meant for content comparison.
- 🔗 In `IdentityHashMap`, JVM will use the `==` operator to identify duplicate keys. The `==` operator is meant for reference comparison (address comparison).

🛠️ **Example Using HashMap:**

```java
import java.util.HashMap;
import java.util.Map;

public class Test {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<String, Integer>();
        String str1 = new String("Java");
        String str2 = new String("Java");
        map.put(str1, 100);
        map.put(str2, 250);
        System.out.println(map); // {Java=250}
    }
}
```

On calling `put(str2, 250)` internally JVM will call `str2.equals(str1)` which returns `true` hence key is duplicate.

🛠️ **Example Using IdentityHashMap:**

```java
import java.util.IdentityHashMap;
import java.util.Map;

public class Test {
    public static void main(String[] args) {
        Map<String, Integer> map = new IdentityHashMap<String, Integer>();
        String str1 = new String("Java");
        String str2 = new String("Java");
        map.put(str1, 100);
        map.put(str2, 250);
        System.out.println(map); // {Java=250, Java=100}
    }
}
```

If we replace `HashMap` with `IdentityHashMap` then `str1` and `str2` are not duplicate keys because `str1==str2` returns `false`.

---

## 7. WeakHashMap Class In Java

It is exactly the same as `HashMap` except for the following difference:

- 🏗️ In `HashMap` even though the object doesn't have any reference it is not eligible for garbage collection if it is associated with HashMap i.e. **HashMap dominates garbage collector**.
- 🗑️ But in the case of `WeakHashMap` if the object doesn't contain any reference then it is eligible for garbage collection even though the object is associated with WeakHashMap i.e. **garbage collector dominates WeakHashMap**.

**Temp class:**

```java
public class Temp {
    public String toString() {
        return "temp";
    }

    public void finalize() {
        System.out.println("finalize method called");
    }

}
```

🛠️ **While Using HashMap:**

```java
import java.util.HashMap;
import java.util.Map;

public class Test {
    public static void main(String[] args) throws InterruptedException {
        Map<Temp, String> map = new HashMap<>();
        Temp temp = new Temp();
        map.put(temp, "Java");
        System.out.println(map);

        temp = null;
        System.gc();
        Thread.sleep(1000);

        System.out.println(map);

    }
}
```

In the above example `Temp` object "temp" is not eligible for garbage collection because it is associated with `HashMap`.

📤 **Output:**

```
{temp=Java}
{temp=Java}
```

In the above program if we replace `HashMap` with `WeakHashMap` then `Temp` object "temp" is eligible for garbage collection. However, `System.gc();` does not guarantee that JVM will perform the garbage collection and call the `finalize()` method. It is only a suggestion.

🛠️ **Example using WeakHashMap:**

```java
import java.util.IdentityHashMap;
import java.util.Map;

public class Test {
    public static void main(String[] args) throws InterruptedException {
        Map<Temp, String> map = new IdentityHashMap<>();
        Temp temp = new Temp();
        map.put(temp, "Java");
        System.out.println(map);

        temp = null;
        System.gc();
        Thread.sleep(1000);

        System.out.println(map);

    }
}
```

📤 **Output:**

```
{temp=Java}
finalize method called
{ }
```

> 🔑 **Key Point:** An entry in a `WeakHashMap` will automatically be removed when its key is no longer in ordinary use, meaning that there is no single Reference that points to that key. When the garbage collection (GC) process discards a key, its entry is effectively removed from the map. In `HashMap`, even if the key does not have any reference, it is not eligible for garbage collection because it's associated with the entry object added in a bucket of HashMap.

---

## 8. SortedMap Interface in Java

- 🗺️ It is the child interface of `Map(I)`.
- ⚖️ If we want to represent a group of key values according to some sorting order of keys then we should go for SortedMap.
- 🔑 Sorting is based on the key but not based on value.

**SortedMap defines the following specific methods:**

- `Object firstKey()`
- `Object lastKey()`
- `SortedMap headMap(Object key)`
- `SortedMap tailMap(Object key)`
- `SortedMap subMap(Object key1, Object key2)`
- `Comparator comparator()`

🛠️ **SortedMap example:**

```java
import java.util.SortedMap;
import java.util.TreeMap;

public class Test {
    public static void main(String[] args) {
        SortedMap<Integer, String> map = new TreeMap<>();
        map.put(101, "A");
        map.put(103, "B");
        map.put(104, "C");
        map.put(107, "D");
        map.put(125, "E");
        map.put(136, "F");

        System.out.println(map);
        // {101=A, 103=B, 104=C, 107=D, 125=E, 136=F}

        System.out.println(map.firstKey()); // 101
        System.out.println(map.lastKey()); // 136
        System.out.println(map.headMap(107)); // {101=A, 103=B, 104=C}
        System.out.println(map.tailMap(107)); // {107=D, 125=E, 136=F}
        System.out.println(map.subMap(103, 125)); // {103=B, 104=C, 107=D}
        System.out.println(map.comparator()); // null
    }
}
```

---

## 9. TreeMap Class in Java

- 🌳 The underlying data structure is the RED-BLACK tree.
- 🔀 Insertion order is not preserved & it is based on some sorting order of keys.
- ❌️ Duplicate keys are not allowed but values can be duplicated.
- 🏷️ If we are depending upon the default sorting order then the keys should be homogeneous and comparable otherwise we will get a runtime exception saying `ClassCastException`. But if we are defining our sorting via `Comparator(I)` then keys need not be homogeneous and comparable.
- 📦 Whether we are depending on a default natural sorting order or a customized sorting order there are no restrictions for values.

**Null Acceptance in TreeMap Class:**

- 🚫 For non-empty TreeMap if we are trying to insert an entry with the null key then we will get the runtime exception: `NullPointerException`.
- 📜 For the empty TreeMap, till the 1.6 version the 1st entry with a null key was allowed. From the 1.7 version onwards null is not allowed for the key.
- ✅ For the value we can insert the `null` value any number of times.

**Constructors in TreeMap Class:**

- **`TreeMap m = new TreeMap();`** For default natural sorting order.
- **`TreeMap t = new TreeMap(Comparator c);`** For customized sorting orders.
- **`TreeMap t = new TreeMap(SortedMap m);`**
- **`TreeMap t = new TreeMap(Map m);`**

🛠️ **Example-1: Default natural sorting order:**

```java
import java.util.Map;
import java.util.TreeMap;

public class Test {
    public static void main(String[] args) {
        Map<Integer, String> treeMap = new TreeMap<>();
        treeMap.put(100, "ZZ");
        treeMap.put(103, "YY");
        treeMap.put(101, "XX");
        // treeMap.put(null, "ABCD"); // NullPointerException

        System.out.println(treeMap); // {100=ZZ, 101=XX, 103=YY}
    }
}
```

🛠️ **Example-2: Customized Sorting (descending order of keys):**

```java
import java.util.Comparator;
import java.util.Map;
import java.util.TreeMap;

public class Test {
    public static void main(String[] args) {
        Map<String, Integer> map = new TreeMap<>(new Comparator<String>() {

            @Override
            public int compare(String o1, String o2) {
                return o2.compareTo(o1);
            }
        });
        map.put("XX", 10);
        map.put("AA", 20);
        map.put("ZZ", 30);
        map.put("LL", 40);
        System.out.println(map); // {ZZ=30, XX=10, LL=40, AA=20}
    }
}
```

The same can be done as:
`Map map = new TreeMap<>(Comparator.reverseOrder());`

We have discussed many more examples of Comparable and Comparators in separate blogs.

---

## 10. Hashtable Class in Java

- #️⃣ The underlying data structure is hashtable.
- 🔀 Insertion order is not preserved and it is based on the hashcode of keys.
- ❌️ Duplicate keys are not allowed and values can be duplicated.
- 📦 Heterogeneous objects are allowed for keys and values.
- 🚫 Null is not allowed for both key and value otherwise we will get `NullPointerException`.
- 🏷️ It implements `Serializable` & `Cloneable` interface but not `RandomAccess`.
- 🔒 Every method present in Hashtable is synchronized and hence Hashtable object is thread-safe.
- 🔍 Hashtable is the best choice if our frequent operation is a search operation.

**Constructors of Hashtable Class in Java:**

1. **`Hashtable h = new Hashtable();`** It creates an empty hashtable object with a default capacity of 11 and a default fill ratio of 0.75.
2. **`Hashtable h = new Hashtable(int initialCapacity);`**
3. **`Hashtable h = new Hashtable(int initialCapacity, float fillRatio);`**
4. **`Hashtable h = new Hashtable(Map m);`**

🛠️ **Hashtable example:**

```java
import java.util.Hashtable;
import java.util.Map;

public class Test {
    public static void main(String[] args) {
        Map<Temp, String> hashtable = new Hashtable<>();
        hashtable.put(new Temp(5), "A");
        hashtable.put(new Temp(2), "B");
        hashtable.put(new Temp(6), "C");
        hashtable.put(new Temp(15), "D"); // 15 % 11 = 4
        hashtable.put(new Temp(23), "E"); // 23 % 11 = 1
        hashtable.put(new Temp(16), "F"); // 16 % 11 = 5

        System.out.println(hashtable);
    }
}
```

📤 **Output:**

```
{6=C, 16=F, 5=A, 15=D, 2=B, 23=E}
```

**Storing order (Top to Bottom, Right to Left):**

| Bucket 🪣 | Entry 📋 |
|-----------|---------|
| **6** | 6=C |
| **5** | 5=A, 16=F |
| **4** | 15=D |
| **2** | 2=B |
| **1** | 23=E |

In the above program, if we change `hashCode()` of the Temp class as:

```java
public int hashCode() {
   return i % 9;
}
```

```java
import java.util.Hashtable;
import java.util.Map;

public class Test {
    public static void main(String[] args) {
        Map<Temp, String> hashtable = new Hashtable<>();
        hashtable.put(new Temp(5), "A"); // 5 % 9 = 5
        hashtable.put(new Temp(2), "B"); // 2 % 9 = 2
        hashtable.put(new Temp(6), "C"); // 6 % 9 = 6
        hashtable.put(new Temp(15), "D"); // 15 % 9 = 6
        hashtable.put(new Temp(23), "E"); // 23 % 9 = 5
        hashtable.put(new Temp(16), "F"); // 16 % 9 = 7

        System.out.println(hashtable);
    }
}
```

📤 **Output:**

```
{16=F, 15=D, 6=C, 23=E, 5=A, 2=B}
```

| Bucket 🪣 | Entry 📋 |
|-----------|---------|
| **7** | 16=F |
| **6** | 6=C, 15=D |
| **5** | 5=A, 23=E |
| **2** | 2=B |

If we configure the initial capacity as 25: `Hashtable hashtable = new Hashtable(25);`

And the `hashCode()` method of the Temp class returns:

```java
public int hashCode() {
   return i;
}
```

```java
import java.util.Hashtable;
import java.util.Map;

public class Test {
    public static void main(String[] args) {
        Map<Temp, String> hashtable = new Hashtable<>(25);
        hashtable.put(new Temp(5), "A"); // 5 % 25 = 5
        hashtable.put(new Temp(2), "B"); // 2 % 25 = 2
        hashtable.put(new Temp(6), "C"); // 6 % 25 = 6
        hashtable.put(new Temp(15), "D"); // 15 % 25 = 15
        hashtable.put(new Temp(23), "E"); // 23 % 25 = 23
        hashtable.put(new Temp(16), "F"); // 16 % 25 = 16

        System.out.println(hashtable);
        // {23=E, 16=F, 15=D, 6=C, 5=A, 2=B}
    }
}
```

| Bucket 🪣 | Entry 📋 |
|-----------|---------|
| **23** | 23=E |
| **16** | 16=F |
| **15** | 15=D |
| **6** | 6=C |
| **5** | 5=A |
| **2** | 2=B |

---

## 11. HashMap vs Hashtable

| Feature | HashMap 🗺️ | Hashtable 🔒 |
|---------|-----------|-------------|
| **Synchronization** | ❌️ Non-synchronized | ✅ Synchronized |
| **Thread Safety** | ❌️ Not thread-safe | ✅ Thread-safe (only one thread at a time) |
| **Null Keys/Values** | ✅ Null allowed (key: once, values: any) | ❌️ Null not allowed (NullPointerException) |
| **Performance** | ⚡ High (threads don't wait) | 🐢 Low (threads wait) |
| **Version** | Introduced in 1.2 | Introduced in 1.0 |

---

## 12. Properties Class in Java

In our program if anything that changes frequently like username, password, mail ID, mobile number, and e.t.c. is not recommended to hardcode in the Java program because if there is any change then to reflect that change recompilation, rebuild, re-deploy of application is required. Overall it creates a big business impact on the client.

We can overcome this problem by using a properties file. Such type of variable things we have to configure into the properties file. From the properties file, we have to read those values into the Java program and we can use those properties.

> 💡 **Tip:** The main advantage of this approach is: if there is a change in the properties file, to reflect that change just re-deployment is required which won't create any business impact on the client.

We can use the Java properties object to hold properties that are coming from the properties file.

📝 **Note:** In a normal Map (like HashMap, Hashtable, TreeMap, etc.) the key value can be any type but in the case of properties **key and value should be a String type**.

**Constructor:** `Properties properties = new Properties();`

**Methods of Properties Class:**

- 🔍 `String` **`getProperty(String pname)`** - To get the value associated with the specified property. If the specified property is not available then this method returns `null`.
- ⚙️ `String` **`setProperty(String pname, String value)`** - Set a new property. If the specified property is already available then the old value will be replaced with the new value and return the old value.
- 📋 `Enumeration` **`propertyNames()`** - It returns all property names present in the Properties object.
- 📥 `void` **`load(InputStream is)`** - To load properties from the properties file into the Java properties object.
- 📤 `void` **`store(OutputStream os, String comment)`** - To store properties from Java properties object into the properties file.

🔧 **`test.properties` file:**

```properties
password=tiger
user=scott
```

🛠️ **Properties class example:**

```java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.util.Properties;

public class Test {
    public static void main(String[] args) throws IOException {
        Properties properties = new Properties();
        FileInputStream fis = new FileInputStream("test.properties");
        properties.load(fis);

        System.out.println(properties); // {password=tiger, user=scott}

        String username = properties.getProperty("user");
        System.out.println(username); // scott

        properties.setProperty("dept", "Computer Science");
        FileOutputStream fos = new FileOutputStream("test.properties");
        properties.store(fos, "Updated by KnowProgram - User");
    }
}
```

📤 **Now, in `test.properties` file:**

```properties
#Updated by KnowProgram - User
#Sun May 05 19:29:24 IST 2024
password=tiger
dept=Computer Science
user=scott
```
