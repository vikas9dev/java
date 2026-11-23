# Arrays.fill() - Fill Java Arrays

**Arrays.fill() - Fill Java Arrays** | The `Arrays.fill()` method assigns the specified value to each element of the specified range of the specified array.

- [Fill Java Arrays Using Arrays.fill(array, value)](#fill-java-arrays-using-arraysfillarray-value)
- [Arrays.fill(array, fromIndex, toIndex, value)](#arraysfillarray-fromindex-toindex-value)
- [Filling multidimensional array in Java](#filling-multidimensional-array-in-java)

---

## 1. Fill Java Arrays Using Arrays.fill(array, value)

There are many overloaded forms of `fill()` method available in the `java.util.Arrays` class.

📦 **Overloaded forms with two arguments (array, value):**

- `public static void fill(byte[] a, byte val)`
- `public static void fill(short[] a, short val)`
- `public static void fill(int[] a, int val)`
- `public static void fill(long[] a, long val)`
- `public static void fill(char[] a, char val)`
- `public static void fill(float[] a, float val)`
- `public static void fill(double[] a, double val)`
- `public static void fill(boolean[] a, boolean val)`
- `public static void fill(Object[] a, Object val)`

📦 **Overloaded forms with four arguments (array, fromIndex, toIndex, value):**

- `public static void fill(byte[] a, int fromIndex, int toIndex, byte val)`
- `public static void fill(short[] a, int fromIndex, int toIndex, short val)`
- `public static void fill(int[] a, int fromIndex, int toIndex, int val)`
- `public static void fill(long[] a, int fromIndex, int toIndex, long val)`
- `public static void fill(char[] a, int fromIndex, int toIndex, char val)`
- `public static void fill(float[] a, int fromIndex, int toIndex, float val)`
- `public static void fill(double[] a, int fromIndex, int toIndex, double val)`
- `public static void fill(boolean[] a, int fromIndex, int toIndex, boolean val)`
- `public static void fill(Object[] a, int fromIndex, int toIndex, Object val)`

📝 **Note:** In these methods the arguments represent:

- **a** — The array to be filled.
- **val** — The value to be stored in all elements of the array.
- **fromIndex** — The index of the first element (inclusive) to be filled with the specified value.
- **toIndex** — The index of the last element (exclusive) to be filled with the specified value.

Let us first discuss and demonstrate the `fill()` method with two arguments.

`Arrays.fill(array, value)` assigns the specified value to each element of the specified array. Here the given value will be stored in all elements of the given array.

**Fill int array example:**

```java
import java.util.Arrays;

public class ArrayTest {
   public static void main(String[] args) {

      // int array example
      int arr[] = {10, 20, 30, 40, 50};
      System.out.println("Original = " + Arrays.toString(arr));
      Arrays.fill(arr, 99);
      System.out.println("After filling = " + Arrays.toString(arr));
   }
}
```

📤 **Output:**

```
Original = [10, 20, 30, 40, 50]
After filling = [99, 99, 99, 99, 99]
```

Let us demonstrate some other examples with `double`, `char`, and `boolean` arrays.

**Fill double array example:**

```java
// double array example
double doubelArr[] = {15.9, 20.5, 30.5, 40.5, 55.9};
System.out.println("Original = " + Arrays.toString(doubelArr));
Arrays.fill(doubelArr, 18.9);
System.out.println("After filling = " + Arrays.toString(doubelArr));
```

📤 **Output:**

```
Original = [15.9, 20.5, 30.5, 40.5, 55.9]
After filling = [18.9, 18.9, 18.9, 18.9, 18.9]
```

**Fill char array example:**

```java
// char array example
char charArr[]={'K', 'n', 'o', 'w', 'P', 'r', 'o', 'g', 'r', 'a', 'm'};
System.out.println("Original = " + Arrays.toString(charArr));
Arrays.fill(charArr, 'A');
System.out.println("After filling = " + Arrays.toString(charArr));
```

📤 **Output:**

```
Original = [K, n, o, w, P, r, o, g, r, a, m]
After filling = [A, A, A, A, A, A, A, A, A, A, A]
```

**Fill boolean array example:**

```java
// boolean array example
boolean boolArr[] = {true, false, true, false, false};
System.out.println("Original = " + Arrays.toString(boolArr));
Arrays.fill(boolArr, true);
System.out.println("After filling = " + Arrays.toString(boolArr));
```

📤 **Output:**

```
Original = [true, false, true, false, false]
After filling = [true, true, true, true, true]
```

🧠 **In Simple Words:** The `Arrays.fill()` method uses a normal `for` loop to iterate through the array and update each element with the given value.

**Internal implementation of `Arrays.fill(int[] a, int val)`:**

```java
public static void fill(int[] a, int val) {
    for (int i = 0, len = a.length; i < len; i++)
        a[i] = val;
}
```

The remaining `fill(array, value)` methods are also implemented in a very similar way.

---

## 2. Arrays.fill(array, fromIndex, toIndex, value)

The another form of `fill()` method takes four arguments, where:

- **a** — The array to be filled.
- **val** — The value to be stored in all elements of the array.
- **fromIndex** — The index of the first element (inclusive) to be filled with the specified value.
- **toIndex** — The index of the last element (exclusive) to be filled with the specified value.

Let us demonstrate it through some examples.

**Fill first 3 elements:**

```java
// int array example
int arr1[] = {10, 20, 30, 40, 50};
// Example1:- filling first 3 elements
Arrays.fill(arr1, 0, 3, 99);
System.out.println("After filling first 3 elements = "
                  + Arrays.toString(arr1));
```

📤 **Output:**

```
After filling first 3 elements = [99, 99, 99, 40, 50]
```

**Fill last 3 elements:**

```java
int arr2[] = {10, 20, 30, 40, 50};
// Example2:- filling last 3 elements in given array
Arrays.fill(arr2, 2, arr2.length, 99);
System.out.println("After filling last 3 elements = "
                  + Arrays.toString(arr2));
```

📤 **Output:**

```
After filling last 3 elements = [10, 20, 99, 99, 99]
```

**Fill all elements:**

```java
int arr3[] = {10, 20, 30, 40, 50};
// Example3:- filling all elements in given array
Arrays.fill(arr3, 0, arr3.length, 99);
System.out.println("After filling all elements = "
                  + Arrays.toString(arr3));
```

📤 **Output:**

```
After filling all elements = [99, 99, 99, 99, 99]
```

⚠️ **Caution:** Exceptions thrown by `Arrays.fill(a, fromIndex, toIndex, val)`:

| Exception 🚨 | Condition 📋 |
|--------------|-------------|
| **`IllegalArgumentException`** | if `fromIndex > toIndex` |
| **`ArrayIndexOutOfBoundsException`** | if `fromIndex < 0` or `toIndex > a.length` |

**Internal implementation of `Arrays.fill(int[] a, int fromIndex, int toIndex, int val)`:**

```java
public static void fill(int[] a, int fromIndex, int toIndex, int val) {
    rangeCheck(a.length, fromIndex, toIndex);
    for (int i = fromIndex; i < toIndex; i++)
        a[i] = val;
}
static void rangeCheck(int arrayLength, int fromIndex, int toIndex) {
    if (fromIndex > toIndex) {
        throw new IllegalArgumentException(
           "fromIndex(" + fromIndex + ") > toIndex(" + toIndex + ")");
    }
    if (fromIndex < 0) {
        throw new ArrayIndexOutOfBoundsException(fromIndex);
    }
    if (toIndex > arrayLength) {
        throw new ArrayIndexOutOfBoundsException(toIndex);
    }
}
```

---

## 3. Filling multidimensional array in Java

The `Arrays.fill()` method directly can be used only for the single-dimensional array. It doesn't perform deep operations. To fill a [multi-dimensional array](027_Multidimensional_Array_in_Java.md), we need to take the help of loops and `Arrays.fill()` method.

**Java Program to fill [2D Java array](043_2D_Array_in_Java.md):**

```java
import java.util.Arrays;

public class ArrayTest {
   public static void main(String[] args) {
      // 2D array
      int matrix[][] = { { 1, 2 }, { 4, 5 }, { 7, 8 } };
      // filling all elements with 9 in given 2D array
      // using for loop
      for(int i=0; i<matrix.length; i++) {
         Arrays.fill(matrix[i], 9);
      }
      System.out.println("After filling all elements = "
               + Arrays.deepToString(matrix));
   }
}
```

📤 **Output:**

```
After filling all elements = [[9, 9], [9, 9], [9, 9]]
```

**Using for-each loop:**

```java
// using for each loop
for (int[] row : matrix) {
   Arrays.fill(row, 9);
}
```

**Java Program to fill [3D Java array](044_3D_Array_in_Java.md):**

```java
// 3D array 2x3x2
int[][][] arr = {{{1,2},{3,4},{5,6}},{{7,8},{9,1},{2,3}}};
// filling all elements with 5 in given 3D array
// using for loop
for (int i = 0; i < arr.length; i++) {
   for (int j = 0; j < arr[i].length; j++) {
      Arrays.fill(arr[i][j], 5);
   }
}
System.out.println("After filling all elements = "
                  + Arrays.deepToString(arr));
```

📤 **Output:**

```
After filling all elements = [[[5, 5], [5, 5], [5, 5]], [[5, 5], [5, 5], [5, 5]]]
```

**Using for-each loop:**

```java
// using for-each loop
for (int[][] row : arr) {
   for (int[] column : row) {
      Arrays.fill(column, 5);
   }
}
```

> 💡 **Tip:** For multidimensional arrays, always iterate through the outer dimensions and call `Arrays.fill()` on the innermost 1D arrays.

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!
