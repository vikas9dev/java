# Collections Class In Java

**Collections Class In Java** | The `Collections` class defines several utility methods for [collection objects](192_Java_Collection_Framework_Overview.md) like sorting, searching, reversing, etc.

- [Sorting Elements in the List](#sorting-elements-in-the-list)
- [Searching Elements in List](#searching-elements-in-list)
- [Reversing Elements in List](#reversing-elements-in-list)

---

## 1. Sorting Elements in the List

`Collections` class defines the following 2 `sort()` methods:

| Method 🏷️ | Description 📋 |
|-----------|----------------|
| **`sort(List list)`** | Sort based on default natural sorting order. List must contain homogenous and comparable objects |
| **`sort(List l, Comparator c)`** | Sort based on customized sorting order |

> ⚠️ **Caution:** For `sort(List list)`, the list should compulsorily contain homogenous and comparable objects otherwise we will get `RuntimeException: ClassCastException`. The list should not contain `null`, or else we get `NullPointerException`.

**Sort list using default natural sorting order:**

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class Test {
    public static void main(String[] args) {
        List<String> al = new ArrayList<String>();
        al.add("Z");
        al.add("A");
        al.add("K");
        al.add("N");
        // al.add(null);
        System.out.println("Before Sorting: " + al); // [Z, A, K, N]

        Collections.sort(al);
        System.out.println("After Sorting: " + al); // [A, K, N, Z]

    }
}
```

**Sort list using customized sorting order:**

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

public class Test {
    public static void main(String[] args) {
        List<String> al = new ArrayList<String>();
        al.add("Z");
        al.add("A");
        al.add("K");
        al.add("N");
        System.out.println("Before Sorting: " + al); // [Z, A, K, N]

        Collections.sort(al, new Comparator<String>() {
            @Override
            public int compare(String s1, String s2) {
                return s2.compareTo(s1);
            }
        });
        System.out.println("After Sorting: " + al); // [Z, N, K, A]
    }
}
```

---

## 2. Searching Elements in List

The `Collections` class defines the following binary search methods:

1. **`public static int binarySearch(List ls, Object target)`** — If the list is sorted according to the default natural sorting order then we have to use this method.
2. **`public static int binarySearch(List ls, Object target, Comparator c)`** — We have to use this method if the list is sorted according to customized sorting order.

🔑 **Key Points:**

- 🔍 The above search methods internally use a **binary search algorithm**
- ✅ Successful search returns: **index**
- ❌️ Unsuccessful search returns: **insertion point**
- 📍 The insertion point is the location where we can place the target element in the sorted list
- ⚠️ Before calling `binarySearch()`, the list **must be sorted** otherwise we will get unpredictable results
- 🔄 If the list is sorted according to the comparator then at the time of search operation also we have to pass the **same comparator object**

**Insertion point and index mapping (5 elements):**

| Insertion Point | -1 | -2 | -3 | -4 | -5 | -6 |
|----------------|----|----|----|----|----|----|
| **Element** | A | K | M | Z | a | |
| **Index** | 0 | 1 | 2 | 3 | 4 | |

**Search using default natural sorting order:**

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class Test {
    public static void main(String[] args) {
        List<String> al = new ArrayList<String>();
        al.add("A");
        al.add("K");
        al.add("M");
        al.add("Z");
        al.add("a");
        System.out.println(al); // [A, K, M, Z, a]

        Collections.sort(al);
        System.out.println(Collections.binarySearch(al, "Z")); // 3
        System.out.println(Collections.binarySearch(al, "J")); // -2
    }
}
```

**Search using customized sorting order:**

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;

public class Test {
    public static void main(String[] args) {
        ArrayList<Integer> al = new ArrayList<Integer>();
        al.add(15);
        al.add(0);
        al.add(20);
        al.add(10);
        al.add(5);
        System.out.println(al); // [15, 0, 20, 10, 5]

        Comparator<Integer> reverseOrder = new Comparator<Integer>() {

            @Override
            public int compare(Integer o1, Integer o2) {
                return o2.compareTo(o1);
            }
        };

        Collections.sort(al, reverseOrder);
        System.out.println(al); // [20, 15, 10, 5, 0]

        System.out.println(Collections.binarySearch(al, 10, reverseOrder)); // 2
        System.out.println(Collections.binarySearch(al, 13, reverseOrder)); // -3
        System.out.println(Collections.binarySearch(al, 17)); // unpredictable result

    }
}
```

**After sorting — insertion point and index mapping:**

| Insertion Point | -1 | -2 | -3 | -4 | -5 | -6 |
|----------------|----|----|----|----|----|----|
| **Element** | 20 | 15 | 10 | 5 | 0 | |
| **Index** | 0 | 1 | 2 | 3 | 4 | |

> ⚠️ **Caution:** Here the list is sorted based on customized sorting but when we call `Collections.binarySearch(al, 17)` **without passing the comparator object** then we will get unpredictable results.

📊 For the list of N elements in the case of `binarySearch` method:

- ✅ Successful search result range: `0` to `n-1`
- ❌️ Unsuccessful search result range: `-(n+1)` to `-1`
- 🔢 Total result range: `-(n+1)` to `n-1`

**Example with 3 elements:**

| Insertion Point | -1 | -2 | -3 | -4 |
|----------------|----|----|----|----|
| **Element** | A | K | Z | |
| **Index** | 0 | 1 | 2 | |

- ✅ Successful search result range: 0 to 2
- ❌️ Unsuccessful search result range: -4 to -1
- 🔢 Total result range: -4 to 2

---

## 3. Reversing Elements in List

The `Collections` class defines the following `reverse()` method to reverse elements in the list: **`public static void reverse(List list)`**

**Reverse list elements:**

```java
import java.util.Arrays;
import java.util.Collections;
import java.util.List;

public class Test {
    public static void main(String[] args) {
        List<Integer> al = Arrays.asList(15, 0, 20, 10, 5);
        System.out.println(al); // [15, 0, 20, 10, 5]

        // reverse the order of the elements
        Collections.reverse(al);
        System.out.println(al); // [5, 10, 20, 0, 15]

    }
}
```

### reverse() vs reverseOrder()

We can use the `reverse()` method to reverse the order of elements of the list whereas we can use the `reverseOrder()` method to get the reversed `Comparator`.

**`Comparator c1 = Collections.reverseOrder(Comparator c);`**

Here `c1` is for descending order whereas `c` is for ascending order.

**Using reverseOrder():**

```java
import java.util.Collections;
import java.util.Comparator;
import java.util.List;
import java.util.stream.Collectors;

public class Test {
    public static void main(String[] args) {
        List<Integer> al = List.of(15, 0, 20, 10, 5);
        System.out.println(al); // [15, 0, 20, 10, 5]

        Comparator<Integer> comparator = new Comparator<Integer>() {
            @Override
            public int compare(Integer o1, Integer o2) {
                return o2.compareTo(o1); // descending order
            }
        };

        // ascending order
        Comparator<Integer> reverseComparator = Collections.reverseOrder(comparator);

        List<Integer> defaultSorted = al.stream().sorted(comparator).collect(Collectors.toList());
        System.out.println(defaultSorted); // [20, 15, 10, 5, 0]

        List<Integer> reverseSorted = al.stream().sorted(reverseComparator).collect(Collectors.toList());
        System.out.println(reverseSorted); // [0, 5, 10, 15, 20]

    }
}
```

> 💡 **Tip:** `Collections.reverseOrder()` without arguments returns a comparator that imposes the reverse of the natural ordering. This is useful when you want to sort in descending order without writing a custom comparator.
