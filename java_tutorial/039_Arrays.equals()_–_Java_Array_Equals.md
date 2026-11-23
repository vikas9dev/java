# Arrays.equals() - Java Array Equals

**Arrays.equals() - Java Array Equals** | The `Arrays.equals()` method in Java returns `true` if the two specified arrays are equal to one another.

- [Java Arrays.equals() Example](#java-arraysequals-example)
- [Additional forms of equals()](#additional-forms-of-equals)

---

## 1. Java Arrays.equals() Example

Two arrays are considered equal if both arrays contain the same number of elements, and all corresponding pairs of elements in the two arrays are equal. In other words, two arrays are equal if they contain the same elements in the same order. Also, two array references are considered equal if both are `null`.

📦 **There are 10 overloaded forms of `Arrays.equals()` method:**

- `public static boolean equals(byte[] a, byte[] b)`
- `public static boolean equals(short[] a, short[] b)`
- `public static boolean equals(int[] a, int[] b)`
- `public static boolean equals(long[] a, long[] b)`
- `public static boolean equals(float[] a, float[] b)`
- `public static boolean equals(double[] a, double[] b)`
- `public static boolean equals(char[] a, char[] b)`
- `public static boolean equals(boolean[] a, boolean[] b)`
- `public static boolean equals(Object[] a, Object[] b)`

📝 **Note:** In these methods the parameters are:

- **a** — array1 which is to be tested for equality.
- **b** — array2 that is to be tested for equality.

🔑 **Return value:** It returns `true` if both arrays are equal else it returns `false`.

Let us demonstrate some examples of the `Arrays.equals()` method in Java. Note that it is comparing two arrays based on its content, not based on its reference.

**Compare int arrays:**

```java
import java.util.Arrays;

public class CompareArray {

  // main method
  public static void main(String[] args) {

    // declare and initialize arrays
    int arr1[] = {10,20,30,40,50};
    int arr2[] = arr1;
    int arr3[] = {10,20,30,40,50};
    int arr4[] = {15,25,35,45,55};

    // compare arrays using Arrays.equals() method
    // compare arr1 and arr2
    if(Arrays.equals(arr1, arr2))
      System.out.println("arr1 & arr2 are same");
    else
      System.out.println("arr1 & arr2 are not same");

    // compare arr1 and arr3
    if(Arrays.equals(arr1, arr3))
      System.out.println("arr1 & arr3 are same");
    else
      System.out.println("arr1 & arr3 are not same");

    // compare arr1 and arr4
    if(Arrays.equals(arr1, arr4))
      System.out.println("arr1 & arr4 are same");
    else
      System.out.println("arr1 & arr4 are not same");
  }
}
```

📤 **Output:**

```
arr1 & arr2 are same
arr1 & arr3 are same
arr1 & arr4 are not same
```

**Compare char arrays:**

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

```
true
false
false
```

> 💡 **Tip:** The `Arrays.equals()` method performs case-sensitive comparison for `char` arrays. `'K'` and `'k'` are considered different.

---

## 2. Additional forms of equals()

In addition to the previously given forms, it also contains more forms to check equality of two arrays over the specified ranges. These forms were introduced in **Java 9** version.

- `public static boolean equals(int[] a, int aFromIndex, int aToIndex, int[] b, int bFromIndex, int bToIndex)`
- `public static boolean equals(long[] a, int aFromIndex, int aToIndex, long[] b, int bFromIndex, int bToIndex)`
- `public static boolean equals(byte[] a, int aFromIndex, int aToIndex, byte[] b, int bFromIndex, int bToIndex)`
- `public static boolean equals(short[] a, int aFromIndex, int aToIndex, short[] b, int bFromIndex, int bToIndex)`
- `public static boolean equals(float[] a, int aFromIndex, int aToIndex, float[] b, int bFromIndex, int bToIndex)`
- `public static boolean equals(double[] a, int aFromIndex, int aToIndex, double[] b, int bFromIndex, int bToIndex)`
- `public static boolean equals(char[] a, int aFromIndex, int aToIndex, char[] b, int bFromIndex, int bToIndex)`
- `public static boolean equals(boolean[] a, int aFromIndex, int aToIndex, boolean[] b, int bFromIndex, int bToIndex)`
- `public static boolean equals(Object[] a, int aFromIndex, int aToIndex, Object[] b, int bFromIndex, int bToIndex)`

📝 **Note:** In these forms, the parameters are:

- **a** — The first array to be tested for equality.
- **aFromIndex** — The index (inclusive) of the first element in the first array to be tested.
- **aToIndex** — The index (exclusive) of the last element in the first array to be tested.
- **b** — The second array to be tested for equality.
- **bFromIndex** — The index (inclusive) of the first element in the second array to be tested.
- **bToIndex** — The index (exclusive) of the last element in the second array to be tested.

**Range-based equality check example:**

```java
// Declare and initialize arrays
int arr1[] = {10,20,30,40,50};
int arr2[] = {10,20,33,44,55};
int arr3[] = {11,22,30,40,50};
int arr4[] = {15,25,10,20,30};

// Check Equality of arrays
// Check 1st and 2nd elements of arr1 & arr2
System.out.println(Arrays.equals(arr1, 0, 2, arr2, 0, 2));

// Check 3rd, 4th, and 5th elements of arr1 & arr3
System.out.println(Arrays.equals(
                      arr1, 2, arr1.length, arr3, 2, arr3.length));

// Check 1st and 2nd elements of arr1 & arr4
System.out.println(Arrays.equals(arr1, 0, 2, arr4, 0, 2));

// Check 1st, 2nd, 3rd element of arr1 and
// 3rd, 4th, 5th elements of arr4
System.out.println(Arrays.equals(arr1, 0, 3, arr4, 2, arr4.length));
```

📤 **Output:**

```
true
true
false
true
```

It also contains two more forms with a `Comparator`, also available from Java 9 onwards:

- `public static <T> boolean equals(T[] a, T[] a2, Comparator<? super T> cmp)`
- `public static <T> boolean equals(T[] a, int aFromIndex, int aToIndex, T[] b, int bFromIndex, int bToIndex, Comparator<? super T> cmp)`

> ⚠️ **Caution:** `Arrays.equals()` method is only capable of checking the equality of a single dimensional array. For multidimensional arrays, you need to use `Arrays.deepEquals()` method. It is discussed in detail here: How to compare two arrays in Java.

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!
