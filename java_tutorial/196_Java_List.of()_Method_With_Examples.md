# Java List.of() Method With Examples

**Java List.of() Method With Examples** | The `of()` method of the List interface works very similarly to the Arrays.asList() method. Both `Arrays.asList()` and `List.of()` methods can be used to get a list representation of an array.

- [Examples of Java List.of() Method](#examples-of-java-listof-method)
- [UnsupportedOperationException By Java List.of() Method](#unsupportedoperationexception-by-java-listof-method)

---

## 1. Overview

`Arrays.asList()` method returns a fixed-size list backed by the specified array. The changes made to the array will be visible in the returned list. Whereas the `List.of()` method returns an unmodifiable list i.e. the modification done in the array will not be available to the list.

📋 **Following are the overloaded forms of the Java `List.of()` method:**

1. `static List of()`
2. `static List of(E e1)`
3. `static List of(E e1, E e2)`
4. `static List of(E e1, E e2, E e3)`
5. `static List of(E e1, E e2, E e3, E e4)`
6. `static List of(E e1, E e2, E e3, E e4, E e5)`
7. `static List of(E e1, E e2, E e3, E e4, E e5, E e6)`
8. `static List of(E e1, E e2, E e3, E e4, E e5, E e6, E e7)`
9. `static List of(E e1, E e2, E e3, E e4, E e5, E e6, E e7, E e8)`
10. `static List of(E e1, E e2, E e3, E e4, E e5, E e6, E e7, E e8, E e9)`
11. `static List of(E e1, E e2, E e3, E e4, E e5, E e6, E e7, E e8, E e9, E e10)`
12. `static List of(E... elements)`

📝 **Note:** The `of()` method in the List interface was introduced in **Java 9**. Therefore to use the `List.of()` method Java 9 or the later version is required.

---

## 2. Examples of Java List.of() Method

🛠️ **Creating a list from an array:**

```java
import java.util.Arrays;
import java.util.List;

public class Main {
   public static void main(String[] args) {
      Integer[] array = { 10, 15, 20, 25, 30 };
      List<Integer> numbers = List.of(array);

      System.out.println("Array: " + Arrays.toString(array));
      System.out.println(array.getClass().getName());

      System.out.println("List: " + numbers);
      System.out.println(numbers.getClass().getName());
   }
}
```

📤 **Output:**

```
Array: [10, 15, 20, 25, 30]
[Ljava.lang.Integer;
List: [10, 15, 20, 25, 30]
java.util.ImmutableCollections$ListN
```

If we have multiple values and want to create a list from them then there is not necessary to create the array. We can directly pass those values to the Java `List.of()` method and we will have a list representing those values.

🛠️ **Creating a list directly from values:**

```java
import java.util.List;

public class Main {
   public static void main(String[] args) {
      List<Integer> numbers = List.of(11, 22, 33, 44, 55);
      System.out.println("List: " + numbers);
   }
}
```

📤 **Output:**

```
List: [11, 22, 33, 44, 55]
```

🛠️ **Program to convert String Array to List of String using Java `List.of()` Method:**

```java
import java.util.List;

public class Main {
   public static void main(String[] args) {
      String[] arr = { "JavaScript", "HTML", "CSS" };
      List<String> list = List.of(arr);
      System.out.println("List = " + list);
   }
}
```

📤 **Output:**

```
List = [JavaScript, HTML, CSS]
```

Unlike the Arrays.asList() method, while using the `List.of()` method if we modify the array then the change will NOT be available to the list.

🛠️ **Demonstrating immutability of `List.of()`:**

```java
import java.util.Arrays;
import java.util.List;

public class Main {
   public static void main(String[] args) {
      String[] arr = { "JavaScript", "HTML", "CSS" };
      List<String> list = List.of(arr);

      arr[0] = "Java";
      System.out.println("Array: " + Arrays.toString(arr));
      System.out.println("List: " + list);
   }
}
```

📤 **Output:**

```
Array: [Java, HTML, CSS]
List: [JavaScript, HTML, CSS]
```

---

## 3. UnsupportedOperationException By Java List.of() Method

Even though `List.of()` method was introduced as an enhancement to the `Arrays.asList()` method, the `List.of()` method doesn't create an exact copy of the given array. It only prevents array modification from affecting the list representation.

The growable nature of the List and the fixed size of the array again got conflict with each other. In Java, the [array](026_Java_Array_[With_Examples].md) has a fixed size once it is initialized. We can't increase or decrease the size of the array after initialization. Whereas the [List](195_List_Interface_in_Java.md) is growable in nature and we can modify its size. Elements can be added or removed from the list.

> ⚠️ **Caution:** After using the Java `List.of()` method to convert the array to a list, if we try to modify the size of the list i.e. try to add an element or remove an element from the list then we will get `java.lang.UnsupportedOperationException`.

🛠️ **Attempting to add to an unmodifiable list:**

```java
String[] arr = { "JavaScript", "HTML", "CSS" };
List<String> list = List.of(arr);
list.add("Java");
```

📤 **Output:**

```
Exception in thread "main" java.lang.UnsupportedOperationException
```

🛠️ **Attempting to remove from an unmodifiable list:**

```java
String[] arr = { "JavaScript", "HTML", "CSS" };
List<String> list = List.of(arr);
list.remove(0);
```

📤 **Output:**

```
Exception in thread "main" java.lang.UnsupportedOperationException
```
