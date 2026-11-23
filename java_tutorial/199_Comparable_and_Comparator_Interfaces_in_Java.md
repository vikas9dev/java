# Comparable and Comparator Interfaces in Java

**Comparable and Comparator Interfaces in Java** | Both Comparable and Comparator interfaces are used in the sorting of elements. Let us see them in detail.

- [Comparable Interface In Java](#comparable-interface-in-java)
- [Comparator Interface In Java](#comparator-interface-in-java)
- [Example Using Comparator Interface](#example-using-comparator-interface)
- [Comparable vs Comparator Interfaces](#comparable-vs-comparator-interfaces)

---

## 1. Comparable Interface In Java

It is present in `java.lang` package and it contains only one method `compareTo()`. Method Signature: `public int compareTo(T o);`

In most of the pre-defined classes including `String`, `StringBuffer`, `StringBuilder`, and all Wrapper classes `compareTo()` is implemented to return the following: `obj1.compareTo(obj2)`

- 🔽 It returns **-ve** if obj1 has to come before obj2. (obj1 < obj2)
- 🔼 It returns **+ve** if obj1 has to come after obj2. (obj1 > obj2)
- ⚖️ It returns **0** if obj1 & obj2 are equal. (obj1 == obj2)

In `obj1.compareTo(obj2)`, here:
1. **obj1** - The object which is to be inserted.
2. **obj2** - The object which is already inserted.

🛠️ **compareTo() example:**

```java
public class Test {
   public static void main(String[] args) {
      System.out.println("A".compareTo("Z")); // -25
      System.out.println("Z".compareTo("K")); // 15
      System.out.println("A".compareTo("A")); // 0
      System.out.println("A".compareTo(null)); // NullPointerException
   }
}
```

If we are depending on the default natural sorting order then while adding objects into the TreeSet JVM will call the `compareTo()` method.

🛠️ **TreeSet with default natural sorting:**

```java
import java.util.TreeSet;

public class Test {
    public static void main(String[] args) {
        TreeSet<String> ts = new TreeSet<>();
        ts.add("K"); // First element inserted without comparison
        ts.add("Z"); // "Z".compareTo("K") => +ve
        System.out.println(ts); // [K, Z]

        ts.add("A"); // "A".compareTo("K") => -ve
        System.out.println(ts); // [A, K, Z]

        ts.add("A");
        /*
         * "A".compareTo("K") => -ve; before adding this statement we already got -ve,
         * So compare with all other values where we got -ve. "A".compareTo("A") => 0;
         * Duplicate
         */
        System.out.println(ts); // [A, K, Z]

    }
}
```

🛠️ **ClassCastException without Comparable:**

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

> 💡 **Tip:** If the default natural sorting order is not available or if we are not satisfied with the default natural sorting order then we can go for a customized sorting order by using `Comparator(I)`.

---

## 2. Comparator Interface In Java

💡 **Difference between the Comparable and Comparator interface?** `Comparable` is meant for default natural sorting order whereas `Comparator` is meant for customized sorting order.

`Comparator` interface present in `java.util` package and it declares 2 methods `compare()` and `equals()`.

- `public int compare(Object obj1, Object obj2)`
  - 🔽 It returns -ve if obj1 has to come before obj2.
  - 🔼 It returns +ve if obj1 has to come after obj2.
  - ⚖️ It returns 0 if obj1 & obj2 are equal.
- `public boolean equals(Object obj)`

📝 **Note:** Whenever we are implementing the `Comparator` interface then we must provide implementation at least for the `compare()` method. It is not compulsory to provide the implementation for the `equals()` method i.e. implementing the `equals()` method is optional because it is already available in our class from `java.lang.Object` class through inheritance.

```java
class MyComparator implements Comparator {
   public int compare(Object obj1, Object obj2) {
      // ....
      return 0;
   }
}
```

---

## 3. Example Using Comparator Interface

### 1. Descending Order Integer Sorting

**Write a program to insert an integer object into the TreeSet where sorting order is in descending order.**

**MyComparator class:**

```java
import java.util.Comparator;

public class MyComparator implements Comparator<Integer> {

    @Override
    public int compare(Integer i1, Integer i2) {
        if (i1 < i2) {
            return +1;
        } else if (i1 > i2) {
            return -1;
        } else {
            return 0;
        }
    }

}
```

**Test class:**

```java
import java.util.Set;
import java.util.TreeSet;

public class Test {
    public static void main(String[] args) {
        Set<Integer> treeSet = new TreeSet<>(new MyComparator());
        treeSet.add(10);
        treeSet.add(0);
        treeSet.add(15);
        treeSet.add(5);
        treeSet.add(20);
        treeSet.add(20);
        System.out.println(treeSet); // [20, 15, 10, 5, 0]
    }
}
```

**In this program:**

```java
treeset.add(10); // For 1st element Comparison is not required
treeset.add(0); // compare(0, 10) => +ve
treeset.add(15); // compare(15, 10) => -ve
treeset.add(5); // compare(5, 10) => +ve; compare(5, 0) => -ve
treeset.add(20); // compare(20, 10) => -ve; compare(20, 15) => -ve
treeset.add(20); // compare(20, 10) => -ve; compare(20, 15) => -ve; compare(20, 20) => 0
```

If we are using the constructor `TreeSet()` i.e. not passing the `Comparator(I)` object to the constructor then internally JVM will call the `compareTo()` method which is meant for default natural sorting order.

🛠️ **Default natural sorting order:**

```java
import java.util.Set;
import java.util.TreeSet;

public class Test {
    public static void main(String[] args) {
        Set<Integer> treeSet = new TreeSet<>();
        treeSet.add(10);
        treeSet.add(0);
        treeSet.add(15);
        treeSet.add(5);
        treeSet.add(20);
        treeSet.add(20);
        System.out.println(treeSet); // [0, 5, 10, 15, 20]
    }
}
```

If we are using the constructor `TreeSet(Comparator c)` i.e. passing the `Comparator(I)` object to the constructor then internally JVM will call the `compare()` method which is meant for customized sorting order.

In the `MyComparator` class, we can directly call the `Integer` class `compareTo()` method which does the same as we are doing in the `compare()` method:

```java
import java.util.Comparator;

public class MyComparator implements Comparator<Integer> {

    @Override
    public int compare(Integer i1, Integer i2) {
        return i1.compareTo(i2);
    }

}
```

Creating a separate class provides reusability, but if we are not going to use it again then there is no point in creating a separate `MyComparator` class. Instead, we can provide code while creating the TreeSet object.

🛠️ **Anonymous Comparator with descending order:**

```java
import java.util.Comparator;
import java.util.Set;
import java.util.TreeSet;

public class Test {
    public static void main(String[] args) {
        Set<Integer> treeSet = new TreeSet<>(new Comparator<Integer>() {
            @Override
            public int compare(Integer o1, Integer o2) {
                return -o1.compareTo(o2);
            }
        });
        treeSet.add(10);
        treeSet.add(0);
        treeSet.add(15);
        treeSet.add(5);
        treeSet.add(20);
        treeSet.add(20);
        System.out.println(treeSet); // [20, 15, 10, 5, 0]
    }
}
```

**Various possible implementations in the `compare()` method:**

- ✅ **`return i1.compareTo(i2);`** => Default natural sorting order, [0, 5, 10, 15, 20]
- 🔄 **`return -i1.compareTo(i2);`** => Descending Order, [20, 15, 10, 5, 0]
- 🔄 **`return i2.compareTo(i1);`** => Descending Order, [20, 15, 10, 5, 0]
- ✅ **`return -i2.compareTo(i1);`** => Default natural sorting order, [0, 5, 10, 15, 20]
- 📋 **`return +1;`** => Insertion Order, [10, 0, 15, 5, 20, 20]
- 🔄 **`return -1;`** => Reverse of Insertion Order, [20, 20, 5, 15, 0, 10]
- ❌️ **`return 0;`** => [10], Only 1st element will be inserted & all remaining are considered as duplicate.

The `Comparator` class has also provided some static methods like `reverseOrder()`, `naturalOrder()`, `nullsFirst()`, `nullsLast()` which can be used while sorting.

🛠️ **Using `Comparator.reverseOrder()`:**

```java
import java.util.Comparator;
import java.util.Set;
import java.util.TreeSet;

public class Test {
    public static void main(String[] args) {
        Set<Integer> treeSet = new TreeSet<>(Comparator.reverseOrder());
        treeSet.add(10);
        treeSet.add(0);
        treeSet.add(15);
        treeSet.add(5);
        treeSet.add(20);
        treeSet.add(20);
        System.out.println(treeSet); // [20, 15, 10, 5, 0]
    }
}
```

### 2. Reverse Alphabetical Order String Sorting

**Write a program to insert the String object into the TreeSet where all elements should be inserted according to the reverse of alphabetical order.**

Before writing a program to sort according to the reverse of alphabetical order, first, let us see the default natural sorting order. The `String` class overrides the `compareTo()` method to sort elements in the ascending order of the alphabet.

🛠️ **Default alphabetical order:**

```java
import java.util.Set;
import java.util.TreeSet;

public class Test {
    public static void main(String[] args) {
        Set<String> treeSet = new TreeSet<>();
        treeSet.add("Pineapple");
        treeSet.add("Apple");
        treeSet.add("Orange");
        treeSet.add("Grapes");
        treeSet.add("Banana");
        System.out.println(treeSet);
        // [Apple, Banana, Grapes, Orange, Pineapple]
    }
}
```

🛠️ **Reverse alphabetical order using Comparator:**

```java
import java.util.Comparator;
import java.util.Set;
import java.util.TreeSet;

public class Test {
    public static void main(String[] args) {
        Set<String> treeSet = new TreeSet<>(new Comparator<String>() {
            @Override
            public int compare(String o1, String o2) {
                return -o1.compareTo(o2);
            }
        });
        treeSet.add("Pineapple");
        treeSet.add("Apple");
        treeSet.add("Orange");
        treeSet.add("Grapes");
        treeSet.add("Banana");
        System.out.println(treeSet);
        // [Pineapple, Orange, Grapes, Banana, Apple]
    }
}
```

The same program can be written using `Comparator.reverseOrder()` method as follows:

```java
import java.util.Comparator;
import java.util.Set;
import java.util.TreeSet;

public class Test {
    public static void main(String[] args) {
        Set<String> treeSet = new TreeSet<>(Comparator.reverseOrder());
        treeSet.add("Pineapple");
        treeSet.add("Apple");
        treeSet.add("Orange");
        treeSet.add("Grapes");
        treeSet.add("Banana");
        System.out.println(treeSet);
        // [Pineapple, Orange, Grapes, Banana, Apple]
    }
}
```

Write a program to insert a `StringBuffer` object into the TreeSet where the sorting order is alphabetical. This program is similar to `String` because `StringBuffer` also implements `Comparable(I)`.

### 3. Sort by String Length

**Write a program to insert String objects in TreeSet where the sorting order is increasing in length order. If two objects have the same length then consider their alphabetical order.**

```java
import java.util.Comparator;
import java.util.Set;
import java.util.TreeSet;

public class Test {
    public static void main(String[] args) {
        Set<String> treeSet = new TreeSet<>(new Comparator<String>() {
            @Override
            public int compare(String o1, String o2) {
                if (o1.length() > o2.length()) {
                    return 1;
                } else if (o1.length() < o2.length()) {
                    return -1;
                } else {
                    // natural sorting order
                    return o1.compareTo(o2);
                }
            }
        });
        treeSet.add("Apple");
        treeSet.add("Banana");
        treeSet.add("Orange");
        treeSet.add("Grapes");
        treeSet.add("Pineapple");
        treeSet.add("Pear");
        System.out.println(treeSet);
        // [Pear, Apple, Banana, Grapes, Orange, Pineapple]
    }
}
```

The same program can be written using `Integer.compare()`:

```java
import java.util.Comparator;
import java.util.Set;
import java.util.TreeSet;

public class Test {
    public static void main(String[] args) {
        Set<String> treeSet = new TreeSet<>(new Comparator<String>() {
            @Override
            public int compare(String s1, String s2) {
                Integer val = Integer.compare(s1.length(), s2.length());
                if (val != 0) {
                    return val;
                } else {
                    return s1.compareTo(s2); // natural sorting order
                }
            }
        });
        treeSet.add("Apple");
        treeSet.add("Banana");
        treeSet.add("Orange");
        treeSet.add("Grapes");
        treeSet.add("Pineapple");
        treeSet.add("Pear");
        System.out.println(treeSet);
        // [Pear, Apple, Banana, Grapes, Orange, Pineapple]
    }
}
```

The `compare()` method of the `Integer` wrapper class works as: `Integer.valueOf(x).compareTo(Integer.valueOf(y))`

---

## 4. Comparable vs Comparator Interfaces

**When we should use Comparable vs Comparator?**

- ✅ For pre-defined classes default natural sorting order is already available. If we are not satisfied with that default natural sorting order then we can define our sorting order by using the `Comparator` interface.
- ✅ For pre-defined non-comparable classes default natural sorting isn't available, for them, we can define our sorting by using `Comparator`.
- ✅ For our classes like `Employee`, `Product`, and `Student` classes, the programmer who is developing those classes is responsible for defining default natural sorting by implementing the `Comparable` interface. The person who is using those classes, if he is not satisfied with default natural sorting then he can define his sorting by using `Comparator`.

🛠️ **Employee class with Comparable:**

For example: we have an `Employee` class and by default, it should sort employees in ascending order based on the employee ID value. Later if we want to sort based on the name in alphabetic order then we can provide our implementation.

```java
public class Employee implements Comparable<Employee> {

    private Integer id;
    private String name;
    private Double salary;

    public Employee(Integer id, String name, Double salary) {
        this.id = id;
        this.name = name;
        this.salary = salary;
    }

     // getter and setter methods

    @Override
    public String toString() {
        return "Employee [id=" + id + ", name=" + name + ", salary=" + salary + "]";
    }

    @Override
    public int compareTo(Employee emp) {
        return this.getId().compareTo(emp.getId());
    }
}
```

🛠️ **Default sorting by ID:**

```java
import java.util.TreeSet;

public class Test {
    public static void main(String[] args) {
        TreeSet<Employee> treeSet = new TreeSet<>();
        treeSet.add(new Employee(101, "John", 50000.0));
        treeSet.add(new Employee(105, "David", 52000.0));
        treeSet.add(new Employee(102, "Alice", 60000.0));
        treeSet.add(new Employee(104, "Jane", 58000.0));
        treeSet.add(new Employee(103, "Bob", 55000.0));

        System.out.println(treeSet);
        // [Employee [id=101, name=John, salary=50000.0],
        // Employee [id=102, name=Alice, salary=60000.0],
        // Employee [id=103, name=Bob, salary=55000.0],
        // Employee [id=104, name=Jane, salary=58000.0],
        // Employee [id=105, name=David, salary=52000.0]]
    }
}
```

🛠️ **Sort employees based on ascending order of the name:**

```java
TreeSet<Employee> treeSet = new TreeSet<>(new Comparator<Employee>() {

    @Override
    public int compare(Employee o1, Employee o2) {
        return o1.getName().compareTo(o2.getName());
    }
});
```

🛠️ **Sort employees based on descending order of salary:**

```java
TreeSet<Employee> treeSet = new TreeSet<>(new Comparator<Employee>() {

    @Override
    public int compare(Employee o1, Employee o2) {
        // return o2.getSalary().compareTo(o1.getSalary());
        return Double.compare(o2.getSalary(), o1.getSalary());
    }
});
```

🛠️ **Multi-level sorting (salary desc, name asc, id asc):**

Sort employees based on the descending order of their salary, if the salary is the same then sort them based on the ascending order of the name, if they have the same name then sort them based on the employee id.

```java
import java.util.Comparator;
import java.util.TreeSet;

public class Test {
    public static void main(String[] args) {
        TreeSet<Employee> treeSet = new TreeSet<>(new Comparator<Employee>() {

            @Override
            public int compare(Employee o1, Employee o2) {
                // First, compare by salary in descending order
                Integer salaryComparison = Double.compare(o2.getSalary(), o1.getSalary());
                if (salaryComparison != 0) {
                    return salaryComparison;
                } else {
                    // If salary is the same, compare by name in ascending order
                    Integer nameComparison = o1.getName().compareTo(o2.getName());
                    if (nameComparison != 0) {
                        return nameComparison;
                    } else {
                        // If name is also the same, compare by ID in ascending order
                        return o1.getId().compareTo(o2.getId());
                    }
                }
            }
        });
        treeSet.add(new Employee(101, "John", 60000.0));
        treeSet.add(new Employee(102, "Alice", 55000.0));
        treeSet.add(new Employee(103, "Bob", 60000.0));
        treeSet.add(new Employee(104, "Alice", 55000.0));
        treeSet.add(new Employee(105, "David", 60000.0));
        System.out.println(treeSet);
    }
}
```

| Feature | Comparable ⚖️ | Comparator 🔧 |
|---------|-------------|--------------|
| **Purpose** | Default natural sorting order | Customized sorting order |
| **Package** | `java.lang` | `java.util` |
| **Abstract Methods** | 1: `compareTo()` | 2: `compare()`, `equals()` |
| **Pre-defined Implementations** | String, StringBuffer, StringBuilder, all wrapper classes | Collator, RuleBasedCollator (used in GUI-based applications) |
