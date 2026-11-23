# Arrays Class Java With Examples

**Arrays Class Java With Examples** | The arrays class was introduced in JDK 1.2 version. This class contains various methods for manipulating arrays such as sorting, searching, copying, converting an array to a string and etc. Java Arrays class also contains a static factory that allows arrays to be viewed as lists. It belongs to java.util package.

📋 **Arrays Class Declaration:**  
`public class Arrays extends Object`

🔧 **Arrays Class Constructors:**  
It doesn’t contain any public constructors therefore we can’t create objects of the java.util.Arrays class through constructors. It contains:- `private Arrays() {}`

- [Methods of Java Arrays Class](#methods-of-java-arrays-class)
- [Arrays.toString() Method](#arraystostring-method)
- [Arrays.deepToString() Method](#arraysdeeptostring-method)
- [Arrays.sort() Method](#arrayssort-method)
- [Arrays.parallelSort() Method](#arraysparallelsort-method)
- [Arrays.copyOf() Method](#arrayscopyof-method)
- [Arrays.copyOfRange() Method](#arrayscopyofrange-method)
- [Arrays.equals() Method](#arraysequals-method)
- [Arrays.deepEquals() Method](#arraysdeepequals-method)
- [Arrays.hashCode() Method](#arrayshashcode-method)
- [Arrays.deepHashCode() Method](#arraysdeephashcode-method)
- [Arrays.compare() & compareUnsigned()](#arrayscompare--compareunsigned)
- [Arrays.setAll() & parallelSetAll()](#arrayssetall--parallelsetall)
- [Arrays.fill() Method](#arraysfill-method)
- [Arrays.stream() Method](#arraysstream-method)
- [Arrays.asList() Method](#arraysaslist-method)
- [Arrays.binarySearch() Method](#arraysbinarysearch-method)
- [Arrays.mismatch() Method](#arraysmismatch-method)
- [Arrays.spliterator() Method](#arraysspliterator-method)
- [Arrays.parallelPrefix() Method](#arraysparallelprefix-method)

---

## 1. Methods of Java Arrays Class

| Method 🏷️ | Purpose 📋 |
|---|---|
| `Arrays.toString()` | To convert single dimensional array to string |
| `Arrays.deepToString()` | To convert multi-dimensional array to string |
| [`Arrays.sort()`](035_Arrays.sort()_in_Java_With_Examples.md) | To sort array in ascending order |
| [`Arrays.parallelSort()`](035_Arrays.sort()_in_Java_With_Examples.md) | Similar to `Arrays.sort()` (mainly for multiple threads) |
| [`Arrays.copyOf()`](036_Arrays.copyOf_in_Java_With_Example.md) | To copy the complete array to another array |
| [`Arrays.copyOfRange()`](037_Arrays.copyOfRange_in_Java_with_Example.md) | Similar to `Arrays.copyOf()` but copy only within the given range |
| `Arrays.equals()` | For equality testing of two arrays |
| `Arrays.deepEquals()` | For equality testing given two arrays deeply |
| `Arrays.hashCode()` | To give hash code based on the contents of the specified array |
| `Arrays.deepHashCode()` | To give hash code based on the "deep contents" of given array |
| `Arrays.compare()` | Compares two specified arrays lexicographically |
| `Arrays.compareUnsigned()` | Compares two arrays lexicographically, numerically treating elements as unsigned |
| `Arrays.setAll()` | It set all elements of the specified array |
| `Arrays.parallelSetAll()` | Set all elements of the specified array, in parallel |
| [`Arrays.fill()`](038_Arrays.fill()_–_Fill_Java_Arrays.md) | To fill array elements with the given value |
| `Arrays.stream()` | To return stream for the specified array |
| `Arrays.asList()` | To return array as List |
| `Arrays.binarySearch()` | Find the index of the array element |
| `Arrays.mismatch()` | To return the index of the first mismatch between the two arrays |
| `Arrays.spliterator()` | It returns a Spliterator covering all of the specified arrays |
| `Arrays.parallelPrefix()` | It performs a given mathematical function on the elements of the array cumulatively, and then modifies the array concurrently |
---

## 2. Arrays.toString() Method

In Java to convert a single-dimensional array to a string, we can use **Arrays.toString() method**. The Arrays.toString() with all forms were introduced in the **Java 1.5** version. They are listed here:-

- public static String toString(byte[ ] a)
- public static String toString(short[ ] a)
- public static String toString(int[ ] a)
- public static String toString(long[ ] a)
- public static String toString(float[ ] a)
- public static String toString(double[ ] a)
- public static String toString(char[ ] a)
- public static String toString(boolean[ ] a)
- public static String toString(Object[ ] a)

The Arrays.toString() method returns a string representation of the contents of the specified array. The string representation consists of a list of the array’s elements, enclosed in square brackets “`[]`” and the adjacent elements are separated by the characters “, ” (a comma followed by a space). It Returns “null” if the passed array is null.

**Arrays to String in Java Examples**  
Let us see a Java program to demonstrate the Arrays.toString() method.
```java
import java.util.Arrays;

public class ArrayTest {
    public static void main(String[] args) {
        // int array
        int[] arr = { 10, 20, 30, 40, 50 };
        System.out.println("Array = " + Arrays.toString(arr));
    }
}
```

📤 **Output:**

Array = [10, 20, 30, 40, 50]

🛠️ **Example with**[**Java Object Array**](029_Array_of_Objects_in_Java_With_Example.md),

Let us see a complete Java program with an object array and display it through the Arrays.toString() method.

Student class,
```java
class Student {
    private int idNum;
    private String name;

    // constructor
    public Student(int idNum, String name) {
        this.idNum = idNum;
        this.name = name;
    }

    @Override
    public String toString() {
        return "[" + idNum + ", " + name + "]";
    }
}
```

User class or test class,
```java
import java.util.Arrays;

public class Collage {
    public static void main(String[] args) {

        // array of Student objects
        Student[] st = new Student[3];

        // initialize Student object
        st[0] = new Student(100, "Emma");
        st[1] = new Student(110, "Noah");
        st[2] = new Student(235, "Amelia");

        // display Student details
        System.out.println("Student Array = " + Arrays.toString(st));
    }
}
```

📤 **Output:**

Student Array = `[[`100, Emma`], [`110, Noah`], [`235, Amelia`]]`

To demonstrate more examples of converting an array to a string using Arrays.toString(), how Arrays.toString() is implemented? See here:- Arrays.toString() method in Java

---

## 3. Arrays.deepToString() Method

The Arrays.toString() method is capable of converting single dimension array to string, but it can’t convert [multidimensional Java array](027_Multidimensional_Array_in_Java.md) to string. For **converting the multidimensional Java array to a string** we can use the deepToString() method given in the Arrays class.

It returns a string representation of the “deep contents” of the specified array. If the array contains other arrays as elements, the string representation contains their contents, and so on. This method is designed for converting multidimensional arrays to strings.

Similar to the Arrays.toString() method, the Arrays.deepToString() was also introduced later in the **Java1.5** version onwards. The syntax of deepToString() method:-

- public static String deepToString(Object[ ] a)

**Java Program to Print[2D Java Array](043_2D_Array_in_Java.md) using Arrays.deepToString() method**
```java
import java.util.Arrays;

public class TwoDArray {

    public static void main(String[] args) {
        // declare a 2D array
        // and initialize with explicit values
        int[][] arr = { { 50, 60 }, { 70, 80 }, { 90, 10 } };

        // display 2D array using Arrays.toString()
        System.out.println(Arrays.deepToString(arr));
    }
}
```

📤 **Output:**

`[[`50, 60`], [`70, 80`], [`90, 10`]]`

**Java Program to display[three-dimensional Java array](044_3D_Array_in_Java.md) using Arrays.deepToString() method**
```java
import java.util.Arrays;

public class ThreeDArray {

    public static void main(String[] args) {
        // 3D array 2x3x2
        int[][][] arr = { { { 1, 2 }, { 3, 4 }, { 5, 6 } }, 
                          { { 7, 8 }, { 9, 1 }, { 2, 3 } } };

        // displaying three dimensional array in Java using
        // Arrays.deepToString()
        System.out.println(Arrays.deepToString(arr));
    }
}
```

📤 **Output:**

`[[[`1, 2`], [`3, 4`], [`5, 6`]], [[`7, 8`], [`9, 1]`, [`2, 3`]]]`

---

## 4. Arrays.sort() Method

The [Arrays.sort() method](035_Arrays.sort()_in_Java_With_Examples.md) sorts the specified array into ascending numerical order. While working with the [concept of the array in Java](026_Java_Array_[With_Examples].md), no need to write your own logic to implement any sorting algorithm. Just import the Arrays class and use the sort() method which gives the best performance in most cases compared to other sorting algorithms.

There are many sorting algorithms are available to solve only one problem i.e. sort an array. They have different time complexity and space complexity. But among all sorting algorithms Quick Sort gives the best performance.

The time complexity of Quicksort is **O(n log (n))** in the best case, O(n log (n)) in the average case, and O(n^2) in the worst case. But because it has the best performance in the average case for most inputs, therefore Quicksort is generally considered the “fastest” sorting algorithm.

In the java.util.Arrays class there are several overloaded forms of sort() methods available. All of them use dual-pivot Quicksort. The **Dual-Pivot Quicksort** is given by Vladimir Yaroslavskiy, Jon Bentley, and Josh Bloch. This algorithm offers **O(n log(n)) performance** on all data sets and is typically faster than traditional (one-pivot) Quicksort implementations.

Dual pivot quicksort is a little bit faster than the original single-pivot quicksort. But still, the **worst case** will remain **O(n^2)** when the array is already sorted in an increasing or decreasing order.

### Overloaded Forms of Arrays.sort() Method

- public static void sort(byte[ ] a)
- public static void sort(short[ ] a)
- public static void sort(int[ ] a)
- public static void sort(long[ ] a)
- public static void sort(float[ ] a)
- public static void sort(double[ ] a)
- public static void sort(char[ ] a)
- public static void sort(Object[ ] a)
- public static void sort(byte[ ] a, int fromIndex, int toIndex)
- public static void sort(short[ ] a, int fromIndex, int toIndex)
- public static void sort(int[ ] a, int fromIndex, int toIndex)
- public static void sort(long[ ] a, int fromIndex, int toIndex)
- public static void sort(float[ ] a, int fromIndex, int toIndex)
- public static void sort(double[ ] a, int fromIndex, int toIndex)
- public static void sort(char[ ] a, int fromIndex, int toIndex)
- public static void sort(Object[ ] a, int fromIndex, int toIndex)
- public static void sort(T[ ] a, Comparator c)
- public static void sort(T[ ] a, int fromIndex, int toIndex, Comparator c)

Here the parameters are,

- _**a**_ :- the array to be sorted.
- _**FromIndex**_ :- the index of the first element, inclusive, to be sorted.
- _**toIndex**_ :- the index of the last element, exclusive, to be sorted.

**_Arrays.sort(array)_** :- It sorts the full array into ascending order.  
**_Arrays.sort(array, fromIndex, toIndex)_** :- It sorts only the elements from fromIndex to toIndex.

### Java Example to Sort an Array using Array.sort()

**Let us demonstrate an example to sort an array in Java using the Arrays.sort() method:-**
```java
import java.util.Arrays;

public class SortArray {

    // main method
    public static void main(String[] args) {
        // declare and initialize arrays
        int arr[] = { 50, 25, 30, 55, 15 };

        // display array before sorting
        System.out.println("Before Sorting: " + Arrays.toString(arr));

        // sort array
        Arrays.sort(arr);

        // display array after sorting
        System.out.println("After Sorting: " + Arrays.toString(arr));
    }
}
```

📤 **Output:**

Before Sorting: [50, 25, 30, 55, 15]  
After Sorting: [15, 25, 30, 50, 55]

Another example,
```java
// double array
double[] doubleArr = {10.5, 15.9, 500, -88888, 0.9};
Arrays.sort(doubleArr);
System.out.println("Double Array = " + Arrays.toString(doubleArr));
```

📤 **Output:**

Double Array = [-88888.0, 0.9, 10.5, 15.9, 500.0]

Using _**Arrays.sort(array, fromIndex, toIndex)**_ we can sort only the elements between a particular range. Here _**fromIndex**_ is the index of the first element, inclusive, to be sorted, and _**toIndex**_ is the index of the last element, exclusive, to be sorted. In the below program, since we are calling Arrays.sort(arr, 0, 3); therefore only the first three elements of the given array are sorted.
```java
import java.util.Arrays;

public class SortArray {

    // main method
    public static void main(String[] args) {
        // declare and initialize arrays
        int arr[] = { 50, 25, 30, 55, 15 };

        // display array before sorting
        System.out.println("Before Sorting: " + Arrays.toString(arr));

        // sort array
        Arrays.sort(arr, 0, 3);

        // display array after sorting
        System.out.println("After Sorting: " + Arrays.toString(arr));
    }
}
```

📤 **Output:**

Before Sorting: [50, 25, 30, 55, 15]  
After Sorting: [25, 30, 50, 55, 15]

Exceptions thrown by Arrays.sort(array, fromIndex, toIndex)

- **IllegalArgumentException** :- if fromIndex > toIndex
- **ArrayIndexOutOfBoundsException** :- if fromIndex < 0 or toIndex > a.length

The sorting operation is not applicable to the boolean array. See more examples of the [Arrays.sort() method](035_Arrays.sort()_in_Java_With_Examples.md).

---

## 5. Arrays.parallelSort() Method

The parallelSort() method of the Java Arrays class is given to sort an array. It also sorts the specified array into ascending numerical order. This method is added in **Java 1.8** version.

Unlike Arrays.sort() (which is based on a single thread), It uses multiple threads, and for executing parallel tasks it uses the ForkJoin pool. It uses a sort-merge technique that divides the specified array into chunks of some size and sorts each chunk individually. Finally, the sorted chunks are merged using the merge logic from the Merge-sort algorithm.

**Similarity with Java Arrays.sort() and Arrays.parallelSort():-**

- Both can be used to sort objects and primitive arrays.
- By default, both sort an array into ascending order.

The implementation in JDK 8 uses this approach:-  
1) Divide the array into 4 parts.  
2) Sort the first two parts and then merge them.  
3) Sort the next two parts and then merge them.  
The above steps are repeated recursively with each part until the size of the part to sort is not lesser than the threshold value calculated above.

Note:- Arrays.parallelSort() uses parallelism only when certain conditions are met. If the array size is less than or equal to 8192 or the processor has only one core, then it internally uses the Arrays.sort() method.

**Overloaded Forms of Arrays.parallelSort() method**  
Similar to sort() it also has two variants to sort a full array and partial array,

- public static void parallelSort(byte[ ] a)
- public static void parallelSort(short[ ] a)
- public static void parallelSort(int[ ] a)
- public static void parallelSort(long[ ] a)
- public static void parallelSort(float[ ] a)
- public static void parallelSort(double[ ] a)
- public static void parallelSort(char[ ] a)
- public static void parallelSort(byte[ ] a, int fromIndex, int toIndex)
- public static void parallelSort(short[ ] a, int fromIndex, int toIndex)
- public static void parallelSort(int[ ] a, int fromIndex, int toIndex)
- public static void parallelSort(long[ ] a, int fromIndex, int toIndex)
- public static void parallelSort(float[ ] a, int fromIndex, int toIndex)
- public static void parallelSort(double[ ] a, int fromIndex, int toIndex)
- public static void parallelSort(char[ ] a, int fromIndex, int toIndex)
- public static void parallelSort(T[ ] a, Comparator cmp)
- public static void parallelSort(T[ ] a, int fromIndex, int toIndex, Comparator cmp)
- public static > void parallelSort(T[ ] a, int fromIndex, int toIndex)

**_Arrays.parallelSort(array)_** :- It sorts the full array into ascending order.  
**_Arrays.parallelSort(array, fromIndex, toIndex)_** :- It sorts only the elements from fromIndex to toIndex.

### Examples Using parallelSort() Method of Java Arrays Class
```java
import java.util.Arrays;

public class CompareArray {
    public static void main(String[] args) {
        // declare and initialize arrays
        int arr[] = { 50, 30, 25, 55, 15 };

        // sort array
        Arrays.parallelSort(arr);

        // display array after sorting
        System.out.println(Arrays.toString(arr));
    }
}
```

📤 **Output:**

[15, 25, 30, 50, 55]

Another example to sort fromIndex to toIndex in the given array,
```java
// declare and initialize arrays
int arr[] = {50, 30, 25, 55, 15};
    
// sort array using parallelSort()
Arrays.parallelSort(arr, 1, 3);
    
// display array after sorting
System.out.println(Arrays.toString(arr));
```

📤 **Output:**

[50, 25, 30, 55, 15]

See more about Arrays.parallelSort() and the differences between Arrays.sort() vs Arrays.parallelSort():- [How to sort an array in Java](035_Arrays.sort()_in_Java_With_Examples.md)

---

## 6. Arrays.copyOf() Method

The [copyof() method](036_Arrays.copyOf_in_Java_With_Example.md) of java.util.Arrays class in Java copies the specified array, truncating or padding with zeros/nulls (if necessary). Internally, this method calls the System.arraycopy() method of Java. The copyof() method with all its overloaded forms was introduced in **Java 1.6** version.

There is a total of 10 overloaded forms of Arrays.copyof() method. Those methods are listed here,

- public static byte[ ] copyOf(byte[ ] original, int newLength)
- public static short[ ] copyOf(short[ ] original, int newLength)
- public static int[ ] copyOf(int[ ] original, int newLength)
- public static long[ ] copyOf(long[ ] original, int newLength)
- public static char[ ] copyOf(char[ ] original, int newLength)
- public static float[ ] copyOf(float[ ] original, int newLength)
- public static double[ ] copyOf(double[ ] original, int newLength)
- public static boolean[ ] copyOf(boolean[ ] original, int newLength)
- public static T[ ] copyOf(T[ ] original, int newLength)
- public static T[ ] copyOf(U[ ] original, int newLength, Class newType)

In these methods the parameters are,

- original:- The array to be copied.
- newLength:- The length of the copy to be returned.

If newLength is minimum compared to the length of the original array then, only that portion of array elements will be copied from the original array. But if the original array length is minimum compared to the newLength then the remaining elements will be filled by default values.

### Java Example to Copy Array using copyOf() Method of Arrays Class

Let us see demonstration of the copyof() method of the Arrays class.
```java
import java.util.Arrays;

public class ArrayTest {
    public static void main(String[] args) {
        // original array
        int[] arr = { 10, 20, 30, 40, 50 };
        System.out.println("Original array = "
                + Arrays.toString(arr));

        // Example1
        int[] newArray1 = Arrays.copyOf(arr, 3);
        System.out.println("NewArray1 = "
                + Arrays.toString(newArray1));

        // Example2
        int[] newArray2 = Arrays.copyOf(arr, 5);
        System.out.println("NewArray2 = "
                + Arrays.toString(newArray2));

        // Example3
        int[] newArray3 = Arrays.copyOf(arr, 7);
        System.out.println("NewArray3 = "
                + Arrays.toString(newArray3));
    }
}
```

📤 **Output:**

Original array = [10, 20, 30, 40, 50]  
NewArray1 = [10, 20, 30]  
NewArray2 = [10, 20, 30, 40, 50]  
NewArray3 = [10, 20, 30, 40, 50, 0, 0]

Exceptions thrown by Arrays.copyof() Method,

- NullPointerException:- if the passed original array is null.
- NegativeArraySizeException:- if the passed length (i.e. newLength) is negative.

How to use Arrays.copyof() method to copy [array of objects](029_Array_of_Objects_in_Java_With_Example.md)? How Arrays.copyof() method is implemented? How to copy [multidimensional array](027_Multidimensional_Array_in_Java.md) using the Arrays.copyof() method? These are discussed in detailed here:- [Arrays.copyof() in Java](036_Arrays.copyOf_in_Java_With_Example.md)

---

## 7. Arrays.copyOfRange() Method

The copyOfRange() method in java.util.Arrays class is given to copy the specified range of the specified array into a new array. There is many overloaded forms of Arrays.copyOfRange() method. All those forms were introduced in the **Java1.6 version**. The overloaded forms of Arrays.copyOfRange() method are,

- public static byte[ ] copyOfRange(byte[ ] original, int from, int to)
- public static short[ ] copyOfRange(short[ ] original, int from, int to)
- public static int[ ] copyOfRange(int[ ] original, int from, int to)
- public static long[ ] copyOfRange(long[ ] original, int from, int to)
- public static char[ ] copyOfRange(char[ ] original, int from, int to)
- public static float[ ] copyOfRange(float[ ] original, int from, int to)
- public static double[ ] copyOfRange(double[ ] original, int from, int to)
- public static boolean[ ] copyOfRange(boolean[ ] original, int from, int to)
- public static T[ ] copyOfRange(T[ ] original, int from, int to)
- public static T[ ] copyOfRange(U[ ] original, int from, int to, Class newType)

In these methods the parameters are,

- original:- The array from which a range is to be copied.
- from:- The initial index of the range to be copied, it is inclusive.
- to:- the final index of the range to be copied, exclusive. This index may lie outside the array.

Important points about these parameters:-

- The length of the returned array will be to – from.
- The from must lie between zero and original.length (inclusive).
- The value at original[from] is placed into the initial element of the copy (unless from == original.length or from == to).
- Values from subsequent elements in the original array are placed into subsequent elements in the copy.
- The argument to, must be greater than or equal to the argument from, or may be greater than original.length, in that case default value is placed in all elements of the copy whose index is greater than or equal to original.length – from.

### copyOfRange() Example of Java Arrays Class

Let us demonstrate Arrays.copyOfRange() method with some examples.
```java
import java.util.Arrays;

public class ArrayTest {
    public static void main(String[] args) {
        // original array
        int[] arr = { 10, 20, 30, 40, 50 };
        System.out.println("Original array = "
                 + Arrays.toString(arr));

        // Example1:- to copy first 3 elements to new array
        int[] newArray1 = Arrays.copyOfRange(arr, 0, 3);
        System.out.println("NewArray1 = "
                 + Arrays.toString(newArray1));

        // Example2:- to copy 30 and 40 to new array
        int[] newArray2 = Arrays.copyOfRange(arr, 2, 4);
        System.out.println("NewArray2 = "
                 + Arrays.toString(newArray2));

        // Example3:- to copy only one element 40
        int[] newArray3 = Arrays.copyOfRange(arr, 3, 4);
        System.out.println("NewArray3 = "
                 + Arrays.toString(newArray3));

        // Example4:- to copy complete array
        int[] newArray4 = Arrays.copyOfRange(arr, 0, arr.length);
        System.out.println("NewArray4 = "
                 + Arrays.toString(newArray4));

        // Example5:- to copy last element of array
        int[] newArray5 = Arrays.copyOfRange(arr, arr.length - 1, arr.length);
        System.out.println("NewArray5 = "
                 + Arrays.toString(newArray5));

        // Example6:- argument "to" can be greater than arr.length
        int[] newArray6 = Arrays.copyOfRange(arr, 0, 10);
        System.out.println("NewArray6 = "
                 + Arrays.toString(newArray6));
    }
}
```

📤 **Output:**

Original array = [10, 20, 30, 40, 50]  
NewArray1 = [10, 20, 30]  
NewArray2 = [30, 40]  
NewArray3 = [40]  
NewArray4 = [10, 20, 30, 40, 50]  
NewArray5 = [50]  
NewArray6 = [10, 20, 30, 40, 50, 0, 0, 0, 0, 0]

The Arrays.copyOfRange() method implementation is very similar to [Arrays.copyof()](036_Arrays.copyOf_in_Java_With_Example.md). Similar to Arrays.copyof() method, internally this method is also calling [System.arrayCopy() method](031_System.arraycopy()_in_Java_with_Examples.md) which is a native method that uses System resources to copy the array to give high performance. To learn more about copyOfRange() method, see:- [Arrays.copyOfRange() method in Java](037_Arrays.copyOfRange_in_Java_with_Example.md)

---

## 8. Arrays.equals() Method

In Java, the Arrays.equals() method can be used to check whether the two given arrays are equal or not. It returns true if the given arrays are equal else it returns false.

Two arrays are considered equal if both arrays contain the same number of elements, and all corresponding pairs of elements in the two arrays are equal. In other words, two arrays are equal if they contain the same elements in the same order. Also, two array references are considered equal if both are null.

There are 10 overloaded forms of Arrays.equals() method and they are listed here,

- public static boolean equals(byte[ ] a, byte[ ] b)
- public static boolean equals(short[ ] a, short[ ] b)
- public static boolean equals(int[ ] a, int[ ] b)
- public static boolean equals(long[ ] a, long[ ] b)
- public static boolean equals(float[ ] a, float[ ] b)
- public static boolean equals(double[ ] a, double[ ] b)
- public static boolean equals(char[ ] a, char[ ] b)
- public static boolean equals(boolean[ ] a, boolean[ ] b)
- public static boolean equals(Object[ ] a, Object[ ] b)

In these methods the parameter,

- a:- array1 which to be tested for equality.
- b:- array2 that to be tested for equality.

Let us demonstrate some examples of the Arrays.equals() method in Java. Note that it is comparing two arrays based on its content, not based on its reference.
```java
import java.util.Arrays;

public class CompareArray {
    public static void main(String[] args) {
        // declare and initialize arrays
        int arr1[] = { 10, 20, 30, 40, 50 };
        int arr2[] = arr1;
        int arr3[] = { 10, 20, 30, 40, 50 };
        int arr4[] = { 15, 25, 35, 45, 55 };

        // compare arrays using Arrays.equals() method
        // compare arr1 and arr2
        if (Arrays.equals(arr1, arr2))
            System.out.println("arr1 & arr2 are same");
        else
            System.out.println("arr1 & arr2 are not same");

        // compare arr1 and arr3
        if (Arrays.equals(arr1, arr3))
            System.out.println("arr1 & arr3 are same");
        else
            System.out.println("arr1 & arr3 are not same");

        // compare arr1 and arr4
        if (Arrays.equals(arr1, arr4))
            System.out.println("arr1 & arr4 are same");
        else
            System.out.println("arr1 & arr4 are not same");
    }
}
```

📤 **Output:**

arr1 & arr2 are same  
arr1 & arr3 are same  
arr1 & arr4 are not same

Let us see more Java examples with another array and equals().
```java
// declare and initialize arrays
char arr1[] = {'K','N','O','W'};
char arr2[] = {'K','N','O','W'};
char arr3[] = {'k','n','o','w'};
char arr4[] = {'P','R','O','G','R','A','M'};

// compare arrays using Arrays.equals() method
System.out.println(Arrays.equals(arr1, arr2));
System.out.println(Arrays.equals(arr1, arr3));
System.out.println(Arrays.equals(arr1, arr4));
```

📤 **Output:**

true  
false  
false

Addition to the previously given forms, it also contains more forms to check equality of two arrays over the specified ranges. These forms were introduced in Java 9 version.

- public static boolean equals(int[] a, int aFromIndex, int aToIndex, int[] b, int bFromIndex, int bToIndex)
- and more

---

## 9. Arrays.deepEquals() Method

Arrays.equals() method is only capable of checking the equality of a single dimensional array. For [multidimensional array](027_Multidimensional_Array_in_Java.md), we need to use Arrays.deepEquals() method. The syntax of Arrays.deepEquals() method,

- public static boolean deepEquals(Object[ ] a1, Object[ ] a2)

This method is appropriate for use with nested arrays of arbitrary depth. Two array references are considered deeply equal,

- If both are null, or
- If they refer to arrays that contain the same number of elements and all corresponding pairs of elements in the two arrays are deeply equal.

```java
import java.util.Arrays;

public class CompareArray {
    public static void main(String[] args) {
        // declare and initialize 2D arrays
        int arr1[][] = { { 50, 60 }, { 70, 80 }, { 90, 100 } };
        int arr2[][] = arr1;
        int arr3[][] = { { 50, 60 }, { 70, 80 }, { 90, 100 } };
        int arr4[][] = { { 55, 66 }, { 77, 88 }, { 99, 100 } };

        // compare arr1 and arr2
        if (Arrays.deepEquals(arr1, arr2))
            System.out.println("arr1 & arr2 are same");
        else
            System.out.println("arr1 & arr2 are not same");

        // compare arr1 and arr3
        if (Arrays.deepEquals(arr1, arr3))
            System.out.println("arr1 & arr3 are same");
        else
            System.out.println("arr1 & arr3 are not same");

        // compare arr1 and arr4
        if (Arrays.deepEquals(arr1, arr4))
            System.out.println("arr1 & arr4 are same");
        else
            System.out.println("arr1 & arr4 are not same");
    }
}
```

📤 **Output:**

arr1 & arr2 are same  
arr1 & arr3 are same  
arr1 & arr4 are not same

The Arrays.deepEquals() method can compare only [multidimensional array](027_Multidimensional_Array_in_Java.md), not the single-dimensional array. We can also compare the [3D Java array](044_3D_Array_in_Java.md) using the Arrays.deepEquals() method. See:- How to compare two arrays in Java.

---

## 10. Arrays.hashCode() Method

The Arrays.hashCode() method is given to return the hashcode value based on the contents of given array. For two given arrays a and b such that Arrays.equals(a,b), it is also the case that Arrays.hashCode(a) = Arrays.hashCode(b).

It contains several overloaded forms of hashCode() method, and all of them were given in **Java 1.5** version onwards. They are:-

- public static int hashCode(byte a[ ])
- public static int hashCode(short a[ ])
- public static int hashCode(int a[ ])
- public static int hashCode(long a[ ])
- public static int hashCode(float a[ ])
- public static int hashCode(double a[ ])
- public static int hashCode(char a[ ])
- public static int hashCode(boolean a[ ])
- public static int hashCode(Object a[ ])

**Return value** :- content-based hash code for a given array. If the array referenced to null then it returns 0.

### Java Example Using hashCode() of Java Arrays Class

Let us demonstrate Arrays.hashCode() method with different types of arrays.
```java
import java.util.Arrays;

public class ArrayTest {
    public static void main(String[] args) {
        int[] arr = { 10, 20, 30, 40, 50 };
        System.out.println("Hascode value = " + Arrays.hashCode(arr));
    }
}
```

📤 **Output:**

Hascode value = 38490301

Arrays.hashCode() method returns the same for the byte, short, and int array with the same content. But it returns different results for other data types because it is using a different algorithms for calculating hash code value. Now, let us demonstrate with the byte, long, float, double, char, boolean array.
```java
byte[] arr1 = {10, 20, 30, 40, 50};
System.out.println("Hascode value = " + Arrays.hashCode(arr1));
```

Hascode value = 38490301
```java
long[] arr2 = {10, 20, 30, 40, 50};
System.out.println("Hascode value = " + Arrays.hashCode(arr2));
```

Hascode value = 38490301
```java
float[] arr3 = {10, 20, 30, 40, 50};
System.out.println("Hascode value = " + Arrays.hashCode(arr3));
```

Hascode value = 1464653983
```java
double[] arr4 = {10, 20, 30, 40, 50};
System.out.println("Hascode value = " + Arrays.hashCode(arr4));
```

Hascode value = 610785439
```java
char[] arr5 = {'K','n','o','w','P','r','o','g','r','a','m'};
System.out.println("Hascode value = " + Arrays.hashCode(arr5));
```

Hascode value = -2107616584
```java
boolean[] arr6 = {true, false, true, true, false};
System.out.println("Hascode value = " + Arrays.hashCode(arr6));
```

Hascode value = 1203557358

---

## 11. Arrays.deepHashCode() Method

The Arrays.deepHashCode() method returns a hash code based on the “deep contents” of the given array. If the array contains other arrays as elements, the hash code is based on their contents and so on, ad infinitum. If the array referenced to null then it returns 0.

The signature of Arrays.deepHashCode() method is:- `public static int deepHashCode(Object a[])`

**Result using Arrays.hashCode() method** ,
```java
int arr1[][] = {{50,60},{70,80},{90,100}};
System.out.println("Hascode value = " + Arrays.hashCode(arr1));
```

Hascode value = 1016072584

**Result using Arrays.deepHashCode() method** ,
```java
int arr2[][] = {{50,60},{70,80},{90,100}};
System.out.println("Hascode value = " + Arrays.deepHashCode(arr2));
```

Hascode value = 2603914

The previous example was using [two dimensional Java array](043_2D_Array_in_Java.md). Let us see an example using [three dimensional Java array](044_3D_Array_in_Java.md).
```java
// 3D array 2x3x2
int[][][] arr3 = {{{1,2},{3,4},{5,6}},{{7,8},{9,1},{2,3}}};
System.out.println("Result using hashcode() = " 
                   + Arrays.hashCode(arr3));
System.out.println("Result using deepHashcode() = " 
                   + Arrays.deepHashCode(arr3));
```

📤 **Output:**

Result using hashcode() = 279892533  
Result using deepHashcode() = 32797290

---

## 12. Arrays.compare() & compareUnsigned()

The compare method of the Java Arrays class compares two arrays lexicographically. Similarly, Arrays.compareUnsigned() method is comparing two arrays lexicographically, but numerically treating elements as unsigned. Both methods are given in **Java 9** version onwards.

A null array reference is considered lexicographically less than a non-null array reference. Two null array references are considered equal.**Return Value**| **Condition**|  0| If both array are equal and contain the same elements in the same order.| Less than 0| If the first array is lexicographically less than the second array.| Greater than 0| If the first array is lexicographically greater than the second array.  
---|---  
  
There are many overloaded forms are available either with and without range. Note:- The compareUnsigned() method with and without range is available only for byte, short, int, and long data types. For remaining only compare() method is available with or without range. Here are some example:-

- public static int compare(int[ ] a, int[ ] b)
- public static int compare(int[ ] a, int aFromIndex, int aToIndex, int[ ] b, int bFromIndex, int bToIndex)
- public static int compareUnsigned(int[ ] a, int[ ] b)
- public static int compareUnsigned(int[ ] a, int aFromIndex, int aToIndex, int[ ] b, int bFromIndex, int bToIndex)

For float, double, char, boolean, T[ ] only compare method is available like below,

- public static int compare(boolean[ ] a, boolean[ ] b)
- public static int compare(boolean[ ] a, int aFromIndex, int aToIndex, boolean[ ] b, int bFromIndex, int bToIndex)

### Examples Using compare() & compareUnsigned() of Java Arrays Class

Java program to demonstrate Arrays.compare() method using int array,
```java
import java.util.Arrays;

public class ArrayTest {
    public static void main(String[] args) {
        int arr1[] = { 10, 20, 30, 40, 50 };
        int arr2[] = { 10, 20, 30, 40, 50 };
        int arr3[] = { 15, 25, 35, 45, 55 };
        System.out.println(Arrays.compare(arr1, arr2));
        System.out.println(Arrays.compare(arr1, arr3));
        System.out.println(Arrays.compare(arr3, arr1));
    }
}
```

📤 **Output:**

0  
-1  
1

Java program to demonstrate Arrays.compareUnsigned() method using int array,
```java
import java.util.Arrays;

public class ArrayTest {
    public static void main(String[] args) {
        int arr1[] = { 10, 20, 30, 40, 50 };
        int arr2[] = { 10, 20, 30, 40, 50 };
        int arr3[] = { -10, 20, -30, 40, -50 };
        int arr4[] = { 15, 25, 35, 45, 55 };
        System.out.println(Arrays.compareUnsigned(arr1, arr2));
        System.out.println(Arrays.compareUnsigned(arr1, arr3));
        System.out.println(Arrays.compareUnsigned(arr1, arr4));
        System.out.println(Arrays.compareUnsigned(arr4, arr1));
        System.out.println(Arrays.compareUnsigned(arr3, arr4));
    }
}
```

📤 **Output:**

0  
-1  
-1  
1  
1

### equals() vs compare() of Java Arrays Class

Just by looking at the name, they may look the same but there is a huge difference between them. Let us see the difference between equals() and compare() methods in the Arrays class.**Arrays.equals()**| **Arrays.compare()**|  Return either true or false.| Return 0, -1 or 1.| It check whether the two given arrays are equal or not.| It compares two arrays lexicographically. Thr first array can be equal/lesser/greater than second array.  
---|---  
  
---

## 13. Arrays.setAll() & parallelSetAll()

The set() method set all elements of the specified array, using the provided generator function to compute each element. The setAll() method set all elements of the specified array, in parallel, using the provided generator function to compute each element. The Arrays.set() and Arrays.setAll() both methods were introduced in **Java 1.8** version.

Note:- The set() and setAll() methods are given only for the int, long, double, T[ ] array. Total 8 methods are there. For int array they are:-

- public static void setAll(int[ ] array, IntUnaryOperator generator)
- public static void parallelSetAll(int[ ] array, IntUnaryOperator generator)

The parameters are:-

- **_array_** :- Array to which the elements to be set.
- **_generator_** :- It is a function that accepts the index of an array and returns the computed value to that index.

Comparision between Arrays.setAll() and Arrays.parallelSetAll():-

- Both methods produce the same output.
- The setAll() runs faster on the smaller sized array.
- The parallelSetAll() runs faster on larger sized array.
- But parallelSetAll() is considered faster as it performs the changes on the array parallel(i.e. at once) while setAll() updates each index of the array(i.e. one after another).

### Examples using setAll() & parallelSetAll() of Java Arrays Class

Below Java program check array elements, if it is an odd number then it will be replaced by its square value.
```java
import java.util.Arrays;

public class ArrayTest {
    public static void main(String[] args) {

        // declare and initialize arrays
        int[] arr = { 11, 12, 13, 14, 15 };

        // Apply setAll() on given Array
        /*
         * Modify the odd numbers in given array and store square of it
         */
        Arrays.setAll(arr, e -> {
            if (arr[e] % 2 != 0)
                return arr[e] * arr[e];
            else
                return arr[e];
        });

        // display array
        System.out.println(Arrays.toString(arr));
    }
}
```

📤 **Output:**

[121, 12, 169, 14, 225]

The parallelSetAll() method also gives the same result. Example:-
```java
import java.util.Arrays;

public class ArrayTest {
    public static void main(String[] args) {

        // declare and initialize arrays
        int[] arr = { 11, 12, 13, 14, 15 };

        // Apply parallelSetAll() on given Array
        Arrays.parallelSetAll(arr, e -> {
            if (arr[e] % 2 != 0)
                return arr[e] * arr[e];
            else
                return arr[e];
        });

        // display array
        System.out.println(Arrays.toString(arr));
    }
}
```

📤 **Output:**

[121, 12, 169, 14, 225]

Let us see some more examples using parallelSetAll() method. Java program to set 0 at even index and 2*index at odd index in the given array using parallelSetAll() method.
```java
import java.util.Arrays;

public class ArrayTest {
    public static void main(String[] args) {
        int[] arr = { 11, 12, 13, 14, 15 };

        /*
         * Set 0 at even index and 2*index at odd index
         */
        Arrays.parallelSetAll(arr, e -> {
            if (e % 2 == 0)
                return 0;
            else
                return 2 * e;
        });

        System.out.println(Arrays.toString(arr));
    }
}
```

📤 **Output:**

[0, 2, 0, 6, 0]

---

## 14. Arrays.fill() Method

In Java to fill the arrays, the [Arrays.fill() method](038_Arrays.fill()_–_Fill_Java_Arrays.md) is available. The Arrays.fill() method Assigns the specified value to each element of the specified range of the specified array. There are many overloaded forms of fill() method are given, they are listed here:-

- public static void fill(byte[ ] a, byte val)
- public static void fill(short[ ] a, short val)
- public static void fill(int[ ] a, int val)
- public static void fill(long[ ] a, long val)
- public static void fill(char[ ] a, char val)
- public static void fill(float[ ] a, float val)
- public static void fill(double[ ] a, double val)
- public static void fill(boolean[ ] a, boolean val)
- public static void fill(Object[ ] a, Object val)
- public static void fill(byte[ ] a, int fromIndex, int toIndex, byte val)
- public static void fill(short[ ] a, int fromIndex, int toIndex, short val)
- public static void fill(int[ ] a, int fromIndex, int toIndex, int val)
- public static void fill(long[ ] a, int fromIndex, int toIndex, long val)
- public static void fill(char[ ] a, int fromIndex, int toIndex, char val)
- public static void fill(float[ ] a, int fromIndex, int toIndex, float val)
- public static void fill(double[ ] a, int fromIndex, int toIndex,double val)
- public static void fill(boolean[ ] a, int fromIndex, int toIndex, boolean val)
- public static void fill(Object[ ] a, int fromIndex, int toIndex, Object val)

In these methods the parameters represents,

- _**a**_ :- the array to be filled.
- _**val**_ :- the value to be stored in all elements of the array.
- _**fromIndex**_ :- the index of the first element (inclusive) to be filled with the specified value.
- _**toIndex**_ :- the index of the last element (exclusive) to be filled with the specified value.

Let us first discuss and demonstrate the fill() method with two parameters.
```java
import java.util.Arrays;

public class ArrayTest {
    public static void main(String[] args) {
        // int array example
        int arr[] = { 10, 20, 30, 40, 50 };
        System.out.println("Original = " + Arrays.toString(arr));
        Arrays.fill(arr, 99);
        System.out.println("After filling = " + Arrays.toString(arr));
    }
}
```

📤 **Output:**

Original = [10, 20, 30, 40, 50]  
After filling = [99, 99, 99, 99, 99]

**Example using Arrays.fill(array, fromIndex, toIndex, value)**
```java
// int array example
int arr1[] = {10, 20, 30, 40, 50};
// Example1:- filling first 3 elements
Arrays.fill(arr1, 0, 3, 99);
System.out.println("After filling first 3 elements = " 
                  + Arrays.toString(arr1));
```

After filling first 3 elements = [99, 99, 99, 40, 50]

**Exceptions thrown by Arrays.fill(-,-,-,-) method** ,

- IllegalArgumentException:- if fromIndex > toIndex
- ArrayIndexOutOfBoundsException:- if fromIndex < 0 or toIndex > a.length

---

## 15. Arrays.stream() Method

The stream method of the Java Array class returns a sequential Stream with the specified array as its source. It is used to **convert array to stream**. This method was introduced in **Java 1.8** version. Its variations are:-

- public static IntStream stream(int[ ] array)
- public static LongStream stream(long[ ] array)
- public static DoubleStream stream(double[ ] array)
- public static Stream stream(T[ ] array)
- public static IntStream stream(int[ ] array, int startInclusive, int endExclusive)
- public static LongStream stream(long[ ] array, int startInclusive, int endExclusive)
- public static DoubleStream stream(double[ ] array, int startInclusive, int endExclusive)
- public static Stream stream(T[ ] array, int startInclusive, int endExclusive)

The parameters are:-

- _**array**_ :- the array, assumed to be unmodified during use.
- _**startInclusive**_ :- the first index to cover, inclusive.
- _**endExclusive**_ :- index immediately past the last index to cover.

**Java program to convert int array to stream using Arrays.stream() Method**
```java
import java.util.Arrays;
import java.util.stream.IntStream;

public class ArrayTest {
    public static void main(String[] args) {
        // int array
        int[] arr = { 10, 20, 30, 40, 50 };

        // Using Arrays.stream() to convert
        // int array into Stream
        IntStream stream = Arrays.stream(arr);

        // Displaying elements in Stream
        stream.forEach(str -> System.out.print(str + " "));
    }
}
```

📤 **Output:**

10 20 30 40 50

**Java program to convert String array to stream using Arrays.stream()****Method**
```java
import java.util.Arrays;
import java.util.stream.Stream;

public class ArrayTest {
    public static void main(String[] args) {
        // String array
        String[] arr = { "Java", "Python", "C++" };

        // Using Arrays.stream() to convert
        // int array into Stream
        Stream<String> stream = Arrays.stream(arr);

        // Displaying elements in Stream
        stream.forEach(str -> System.out.print(str + " "));
    }
}
```

📤 **Output:**

Java Python C++

**Java program to convert int array to stream using Arrays.stream() Method within a given range,**
```java
import java.util.Arrays;
import java.util.stream.IntStream;

public class ArrayTest {
    public static void main(String[] args) {
        // int array
        int[] arr = { 10, 20, 30, 40, 50 };

        // Using Arrays.stream() to convert
        // int array into Stream
        IntStream stream = Arrays.stream(arr, 2, 4);

        // Displaying elements in Stream
        stream.forEach(str -> System.out.print(str + " "));
    }
}
```

📤 **Output:**

30 40

---

## 16. Arrays.asList() Method

The asList() method of the Java Arrays class returns a fixed-size list backed by the specified array. Changes made to the array will be visible in the returned list, and changes made to the list will be visible in the array. The returned list is Serializable and it implements RandomAccess. This method acts as the bridge between array-based and collection-based APIs, in combination with Collection.toArray(). This runs in O(1) time.

Sytax:- `public static <T> List<T> asList(T... a)`

In the case of primitive data types, the type of the specified array must be a Wrapper Class(Integer, Double, and etc). If we pass int a`[]` to Arrays.asList() method, then it will return a List <int a`[]`> and not List <Integer>, as “autoboxing” doesn’t happen in this case and int a`[]` is itself identified as an object, and a List of int array is returned, instead of the list of integers, which will give an error in various Collection functions.

**Java program to convert Integer array to List using Arrays.asList() method** ,
```java
import java.util.Arrays;
import java.util.List;

public class ArrayTest {
    public static void main(String[] args) {
        // Integer array
        Integer[] arr = { 11, 12, 13, 14, 15 };
        // convert Integer array to list
        List<Integer> list = Arrays.asList(arr);
        // display list
        System.out.println("List = " + list);
    }
}
```

📤 **Output:**

List = [11, 12, 13, 14, 15]

Example to convert String array to List using Arrays.asList() method,
```java
// String array
String[] arr = {"Java", "Python", "C++"};
// convert Integer array to list
List<String> list = Arrays.asList(arr);
// display list
System.out.println("List = " + list);
```

List = [Java, Python, C++]

Example to convert Character array to List using Arrays.asList() method,
```java
// Character array
Character[] arr = {'K','n','o','w','P','r','o','g','r','a','m'};
// convert Integer array to list
List<Character> list = Arrays.asList(arr);
// display list
System.out.println("List = " + list);
```

List = [K, n, o, w, P, r, o, g, r, a, m]

---

## 17. Arrays.binarySearch() Method

The Arrays.binarySearch() method searches the specified array for the specified value using the **binary search algorithm**.

To use the Arrays.binarySearch() method:- The array must be sorted. If the array is not sorted, the results will be undefined.

If the array is not sorted then we can Arrays.sort() or Arrays.parallelSort() to sort the given array in ascending order. If the array contains multiple elements with the specified value, there is no guarantee which one will be found.

There are several overloaded forms of binarySearch() method either with range or without range.

- public static int binarySearch(byte[ ] a, byte key)
- public static int binarySearch(short[ ] a, short key)
- public static int binarySearch(int[ ] a, int key)
- public static int binarySearch(long[ ] a, long key)
- public static int binarySearch(float[ ] a, float key)
- public static int binarySearch(double[ ] a, double key)
- public static int binarySearch(char[ ] a, char key)
- public static int binarySearch(Object[ ] a, Object key)
- public static int binarySearch(T[ ] a, T key, Comparator c)
- public static int binarySearch(byte[ ] a, int fromIndex, int toIndex, byte key)
- public static int binarySearch(short[ ] a, int fromIndex, int toIndex, short key)
- public static int binarySearch(int[ ] a, int fromIndex, int toIndex, int key)
- public static int binarySearch(long[ ] a, int fromIndex, int toIndex, long key)
- public static int binarySearch(float[ ] a, int fromIndex, int toIndex, float key)
- public static int binarySearch(double[ ] a, int fromIndex, int toIndex, double key)
- public static int binarySearch(char[ ] a, int fromIndex, int toIndex, char key)
- public static int binarySearch(Object[ ] a, int fromIndex, int toIndex, Object key)
- public static int binarySearch(T[ ] a, int fromIndex, int toIndex, T key, Comparator c)

Parameters in binarySearch() method:-

- _**a**_ :- the array to be searched
-  _**fromIndex**_ :- the index of the first element (inclusive) to be searched
-  _**toIndex**_ :- the index of the last element (exclusive) to be searched
-  _**key**_ :- the value to be searched for

Retrun value:- it return the index of the search key. If array doesn’t contain key then it returns -1.

### Example Using Arrays.binarySearch() of Java Arrays class
```java
import java.util.Arrays;

public class ArrayTest {
    public static void main(String[] args) {
        int[] arr = { 11, 12, 13, 14, 15 };

        // search 13
        System.out.println("13 found at index = "
                 + Arrays.binarySearch(arr, 13));

        // search 10
        if (Arrays.binarySearch(arr, 10) != -1) {
            System.out.println("10 Found");
        } else {
            System.out.println("10 not Found");
        }
    }
}
```

📤 **Output:**

13 found at index = 2  
10 not Found.

If the array is not sorted then we may get wrong result.
```java
int[] arr = { 15, 12, 14, 11, 13 };
// search 13
System.out.println("13 found at index = " 
            + Arrays.binarySearch(arr, 13));
```

13 found at index = -1

Similarly, if the array is sorted but in descending order then also we may get the wrong result.
```java
int[] arr = { 15, 14, 13, 12, 11 };

// search 14
System.out.println("14 found at index = " 
   + Arrays.binarySearch(arr, 14));

// search 12
System.out.println("12 found at index = " 
   + Arrays.binarySearch(arr, 12));
```

14 found at index = -6  
12 found at index = -1

Therefore, if array is not sorted then before calling Arrays.binarySearch() method sort the given array with the help of Arrays.sort() or Arrays.parallelSort().

---

## 18. Arrays.mismatch() Method

The mismatch method of the Arrays class in Java finds and returns the index of the first mismatch between two arrays. If no mismatch is found then it returns -1. The mismatch() method of the Arrays class in Java was introduced in **Java 9 version**.

Like other methods of Arrays class, it also contains many overloaded forms either with range or without range. For int array, these are two overloaded methods given below. These forms are available for byte`[]`, short`[]`, long`[]`, float`[]`, double`[]`, char`[]`, boolean`[]`, Object`[]`, and T`[]`.

- public static int mismatch(int[ ] a, int[ ] b)
- public static int mismatch(int[ ] a, int aFromIndex, int aToIndex, int[ ] b, int bFromIndex, int bToIndex)

Here the parameters are:-

- _**a**_ :- the first array to compare.
- _**aFromIndex**_ :- the index (inclusive) of the first element in the first array to be compared.
- _**aToIndex**_ :- the index (exclusive) of the last element in the first array to be compared.
- _**b**_ :- the second array to compare.
- _**bFromIndex**_ :- the index (inclusive) of the first element in the second array to be compared.
- _**bToIndex**_ :- the index (exclusive) of the last element in the second array to be compared.

Exceptions thrown by Arrays.mismatch() method,

- IllegalArgumentException:- if aFromIndex > aToIndex or if bFromIndex > bToIndex.
- ArrayIndexOutOfBoundsException:- if aFromIndex < 0 or aToIndex > a.length or if bFromIndex < 0 or bToIndex > b.length.
- NullPointerException:- if either array is null.

```java
import java.util.Arrays;

public class ArrayTest {
    public static void main(String[] args) {
        int[] arr1 = { 10, 11, 12, 13, 14 };
        int[] arr2 = { 10, 11, 12, 13, 14 };
        int[] arr3 = { 10, 11, 13, 12, 14 };
        int[] arr4 = { 14, 11, 13, 12, 15 };

        // match arrays
        System.out.println(Arrays.mismatch(arr1, arr2));
        System.out.println(Arrays.mismatch(arr1, arr3));
        System.out.println(Arrays.mismatch(arr1, arr4));
    }
}
```

📤 **Output:**

-1  
2  
0

---

## 19. Arrays.spliterator() Method

The spliterator() method of Arrays class in Java returns a Spliterator covering all of the specified array. In was given in **Java 1.8 version**. They are:-

- public static Spliterator.OfInt spliterator(int[ ] array)
- public static Spliterator.OfLong spliterator(long[ ] array)
- public static Spliterator.OfDouble spliterator(double[ ] array)
- public static Spliterator spliterator(T[ ] array)
- public static Spliterator spliterator(T[ ] array, int startInclusive, int endExclusive)
- public static Spliterator.OfInt spliterator(int[ ] array, int startInclusive, int endExclusive)
- public static Spliterator.OfLong spliterator(long[ ] array, int startInclusive, int endExclusive)
- public static Spliterator.OfDouble spliterator(double[ ] array, int startInclusive, int endExclusive)

**Java Example using Arrays.spliterator() Method**
```java
import java.util.Arrays;
import java.util.Spliterator;

public class ArrayTest {
    public static void main(String[] args) {
        int[] arr = { 10, 11, 12, 13, 14 };

        Spliterator<Integer> s1 = Arrays.spliterator(arr);
        Spliterator<Integer> s2 = s1.trySplit();

        System.out.println("Spliterator 1");
        s1.forEachRemaining(System.out::println);
        
        System.out.println("Spliterator 2");
        s2.forEachRemaining(System.out::println);
    }
}
```

📤 **Output:**

Spliterator 1  
12  
13  
14  
Spliterator 2  
10  
11

---

## 20. Arrays.parallelPrefix() Method

The parallelPrefix method in the Java Arrays class performs a given mathematical function on the elements of the array cumulatively and then modifies the array concurrently. It was given in **Java 1.8** version. Its variations are:-

- public static void parallelPrefix(int[ ] array, IntBinaryOperator op)
- public static void parallelPrefix(long[ ] array, LongBinaryOperator op)
- public static void parallelPrefix(double[ ] array, DoubleBinaryOperator op)
- public static void parallelPrefix(T[ ] array, BinaryOperator op)
- public static void parallelPrefix(int[ ] array, int fromIndex, int toIndex, IntBinaryOperator op)
- public static void parallelPrefix(long[ ] array, int fromIndex, int toIndex, LongBinaryOperator op)
- public static void parallelPrefix(double[ ] array, int fromIndex, int toIndex, DoubleBinaryOperator op)
- public static void parallelPrefix(T[ ] array, int fromIndex, int toIndex, BinaryOperator op)

**Java Example of Arrays.parallelPrefix() Method** ,
```java
import java.util.Arrays;

public class ArrayTest {
    static int add(int x, int y) {
        return x + y;
    }

    public static void main(String[] args) {
        int[] arr = { 11, 12, 13, 14, 15 };
        Arrays.parallelPrefix(arr, (x, y) -> add(x, y));
        System.out.println(Arrays.toString(arr));
    }
}
```

📤 **Output:**

[11, 23, 36, 50, 65]

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

# **Java Tutorial**  
# **Java Programs**  
➤ [Array in Java](026_Java_Array_[With_Examples].md)  
➤ [Multidimensional Array](027_Multidimensional_Array_in_Java.md)  
➤ [Anonymous Array](028_Anonymous_Array_in_Java_With_Example.md)  
➤ [Array of Objects](029_Array_of_Objects_in_Java_With_Example.md)  
➤ [Jagged Array](030_Jagged_Array_in_Java_with_Example.md)  
➤ [System.arraycopy()](031_System.arraycopy()_in_Java_with_Examples.md)  
# [**Java Array Programs**](026_Java_Array_[With_Examples].md)  
  
Java Arrays Class  
➤ Arrays Class & Methods  
➤ Arrays.toString()  
➤ [Arrays.sort() Method](035_Arrays.sort()_in_Java_With_Examples.md)  
➤ [Arrays.copyof()](036_Arrays.copyOf_in_Java_With_Example.md)  
➤ [Arrays.copyOfRange()](037_Arrays.copyOfRange_in_Java_with_Example.md)  
➤ [Arrays.fill()](038_Arrays.fill()_–_Fill_Java_Arrays.md)  
➤ Arrays.equals() Method  
  
Others  
➤ Get Array Input in Java  
➤ [Return Array From Method](042_How_to_Return_an_Array_in_Java.md)  
➤ [2D Array in Java](043_2D_Array_in_Java.md)  
➤ [3D Array in Java](044_3D_Array_in_Java.md)  
➤ [Matrix Tutorial in Java](045_Matrix_in_Java.md)  
➤ [Array of String in Java](046_String_Array_in_Java.md)  
➤ [Array of double in Java](047_Double_Array_in_Java.md)