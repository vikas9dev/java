# NavigableSet and NavigableMap Interface in Java

**NavigableSet and NavigableMap Interface in Java** | Java 1.6 Version Enhancement in [Collection Framework](192_Java_Collection_Framework_Overview.md) | As part of the 1.6 version the following 2 concepts were introduced in the collection framework: NavigableSet(I) and NavigableMap(I).

- [NavigableSet Interface in Java](#navigableset-interface-in-java)
- [NavigableMap Interface in Java](#navigablemap-interface-in-java)

---

## 1. NavigableSet Interface in Java

- Collection(I) 1.2v
  - Set(I) 1.2v
    - SortedSet(I) 1.2v
      - NavigableSet(I) 1.6v
        - TreeSet 1.2v

NavigableSet is the child interface of [SortedSet](198_HashSet_LinkedHashSet_TreeSet_in_Java.md) and it defines several methods for navigation purposes.

**NavigableSet defines the following methods:**

- 🔽 `floor(e)` - It returns the highest element which is <= e.
- ⬇️ `lower(e)` - It returns highest element which is < e.
- 🔼 `ceiling(e)` - It returns lowest element which is >= e.
- ⬆️ `higher(e)` - It returns lowest element which is > e.
- 📤 `pollFirst()` - It removes and returns the first element.
- 📤 `pollLast()` - It removes and returns the last element.
- 🔄 `descendingSet()` - It returns NavigableSet in reverse order.

🛠️ **NavigableSet example:**

```java
import java.util.TreeSet;

public class Test {
    public static void main(String[] args) {
        TreeSet<Integer> treeSet = new TreeSet<>();
        treeSet.add(1000);
        treeSet.add(1500);
        treeSet.add(2000);
        treeSet.add(2500);
        treeSet.add(3000);
        treeSet.add(4000);
        System.out.println(treeSet);
        // [1000, 1500, 2000, 2500, 3000, 4000]

        System.out.println(treeSet.ceiling(2000)); // 2000
        System.out.println(treeSet.higher(2000)); // 2500
        System.out.println(treeSet.floor(3000)); // 3000
        System.out.println(treeSet.lower(3000)); // 2500
        System.out.println(treeSet.pollFirst()); // 1000
        System.out.println(treeSet.pollLast()); // 4000

        System.out.println(treeSet); // [1500, 2000, 2500, 3000]
        System.out.println(treeSet.descendingSet()); // [3000, 2500, 2000, 1500]
    }
}
```

---

## 2. NavigableMap Interface in Java

- Map(I) 1.2v
  - SortedMap(I) 1.2v
    - NavigableMap(I) 1.6v
      - TreeMap 1.2v

NavigableMap is the child interface of [SortedMap](201_Map_HashMap_LinkedHashMap_TreeMap_in_Java.md). It defines several methods for navigation purposes.

**NavigableMap defines the following methods:**

- 🔽 `floorKey(e)` - Returns the greatest key less than or equal to e.
- ⬇️ `lowerKey(e)` - Returns the greatest key strictly less than e.
- 🔼 `ceilingKey(e)` - Returns the least key greater than or equal to e.
- ⬆️ `higherKey(e)` - Returns the least key strictly greater than e.
- 📤 `pollFirstEntry()` - Removes and returns the first entry.
- 📤 `pollLastEntry()` - Removes and returns the last entry.
- 🔄 `descendingMap()` - Returns a reverse order view.

🛠️ **NavigableMap example:**

```java
import java.util.TreeMap;

public class Test {
    public static void main(String[] args) {
        TreeMap<String, String> treeMap = new TreeMap<>();
        treeMap.put("B", "Banana");
        treeMap.put("C", "Cat");
        treeMap.put("A", "Apple");
        treeMap.put("D", "Dog");
        treeMap.put("G", "Good");
        System.out.println(treeMap);
        // {A=Apple, B=Banana, C=Cat, D=Dog, G=Good}

        System.out.println(treeMap.ceilingKey("C")); // C
        System.out.println(treeMap.higherKey("E")); // G
        System.out.println(treeMap.floorKey("E")); // D
        System.out.println(treeMap.lowerKey("E")); // D
        System.out.println(treeMap.pollFirstEntry()); // A=Apple
        System.out.println(treeMap.pollLastEntry()); // G=Good

        System.out.println(treeMap); // {B=Banana, C=Cat, D=Dog}
        System.out.println(treeMap.descendingMap()); // {D=Dog, C=Cat, B=Banana}
    }
}
```
