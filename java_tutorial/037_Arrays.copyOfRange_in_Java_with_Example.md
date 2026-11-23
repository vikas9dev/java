# Arrays.copyOfRange in Java with Example

**Arrays.copyOfRange in Java with Example** | The `copyOfRange()` method in [java.util.Arrays class](033_Arrays_Class_Java_With_Examples.md) is given to copy the specified range of the specified array into a new array.

- [Arrays.copyOfRange() Example in Java](#arrayscopyofrange-example-in-java)
- [How it is implemented?](#how-it-is-implemented)
- [Copy Multidimensional Array using copyOfRange() of Java Arrays](#copy-multidimensional-array-using-copyofrange-of-java-arrays)

---

## 1. Arrays.copyOfRange() Example in Java

There are many overloaded forms of `Arrays.copyOfRange()` method. All those forms were introduced in the **Java 1.6** version.

📦 **Overloaded forms of `Arrays.copyOfRange()` method:**

- `public static byte[] copyOfRange(byte[] original, int from, int to)`
- `public static short[] copyOfRange(short[] original, int from, int to)`
- `public static int[] copyOfRange(int[] original, int from, int to)`
- `public static long[] copyOfRange(long[] original, int from, int to)`
- `public static char[] copyOfRange(char[] original, int from, int to)`
- `public static float[] copyOfRange(float[] original, int from, int to)`
- `public static double[] copyOfRange(double[] original, int from, int to)`
- `public static boolean[] copyOfRange(boolean[] original, int from, int to)`
- `public static <T> T[] copyOfRange(T[] original, int from, int to)`
- `public static <T,U> T[] copyOfRange(U[] original, int from, int to, Class<? extends T[]> newType)`

📝 **Note:** In these methods the arguments are:

- **original** — The array from which a range is to be copied.
- **from** — The initial index of the range to be copied, it is inclusive.
- **to** — The final index of the range to be copied, exclusive. This index may lie outside the array.

The `copyOfRange()` method returns a new array containing the specified range from the original array, truncated or padded with zeros to obtain the required length.

🔑 **Important points about these arguments:**

- 🔢 The length of the returned array will be **to** - **from**.
- 🔢 The **from** must lie between zero and `original.length` (inclusive).
- 📦 The value at **original[from]** is placed into the initial element of the copy (unless `from == original.length` or `from == to`).
- 📦 Values from subsequent elements in the original array are placed into subsequent elements in the copy.
- 📦 The argument **to** must be greater than or equal to the argument **from**, or may be greater than `original.length`, in that case the default value is placed in all elements of the copy whose index is greater than or equal to `original.length - from`.

Let us demonstrate `Arrays.copyOfRange()` method with some examples.

**Basic copyOfRange() example:**

```java
import java.util.Arrays;

public class ArrayTest {
  public static void main(String[] args) {

    // original array
    int[] arr = {10, 20, 30, 40, 50};
    System.out.println("Original array = " +
                        Arrays.toString(arr));

    // Example1:- to copy first 3 elements to new array
    int[] newArray1 = Arrays.copyOfRange(arr, 0, 3);
    System.out.println("NewArray1 = " +
                        Arrays.toString(newArray1));

    // Example2:- to copy 30 and 40 to new array
    int[] newArray2 = Arrays.copyOfRange(arr, 2, 4);
    System.out.println("NewArray2 = " +
                        Arrays.toString(newArray2));

    // Example3:- to copy only one element 40
    int[] newArray3 = Arrays.copyOfRange(arr, 3, 4);
    System.out.println("NewArray3 = " +
                        Arrays.toString(newArray3));

    // Example4:- to copy complete array
    int[] newArray4 = Arrays.copyOfRange(arr, 0, arr.length);
    System.out.println("NewArray4 = " +
                        Arrays.toString(newArray4));

    // Example5:- to copy last element of array
    int[] newArray5=Arrays.copyOfRange(arr, arr.length-1, arr.length);
    System.out.println("NewArray5 = " +
                        Arrays.toString(newArray5));

    // Example6:- argument "to" can be greater than arr.length
    int[] newArray6 = Arrays.copyOfRange(arr, 0, 10);
    System.out.println("NewArray6 = " +
                        Arrays.toString(newArray6));

  }
}
```

📤 **Output:**

```
Original array = [10, 20, 30, 40, 50]
NewArray1 = [10, 20, 30]
NewArray2 = [30, 40]
NewArray3 = [40]
NewArray4 = [10, 20, 30, 40, 50]
NewArray5 = [50]
NewArray6 = [10, 20, 30, 40, 50, 0, 0, 0, 0, 0]
```

---

## 2. How it is implemented?

The `Arrays.copyOfRange()` method implementation is very similar to [Arrays.copyOf()](036_Arrays.copyOf_in_Java_With_Example.md). Similar to `Arrays.copyOf()` method, internally this method is also calling [System.arrayCopy() method](031_System.arraycopy()_in_Java_with_Examples.md) which is a native method that uses System resources to copy the array to give high performance.

⚙️ **How it works internally:**

1. First of all it calculates the number of elements that should be copied from the original array. `Length = to - from`.
2. If the calculated length is less than 0 then it gives `IllegalArgumentException`.
3. One local array variable is created with the size of the calculated length.
4. Then it internally calls `System.arraycopy()` method.
5. Return the copied array.

**Source code of `copyOfRange()` method to copy int array:**

```java
public static int[] copyOfRange(int[] original, int from, int to) {
    int newLength = to - from;
    if (newLength < 0)
        throw new IllegalArgumentException(from + " > " + to);
    int[] copy = new int[newLength];
    System.arraycopy(original, from, copy, 0,
                    Math.min(original.length - from, newLength));
    return copy;
}
```

Remaining overloaded forms of `copyOfRange()` method are implemented in a similar way, return types are changing based on the passed argument type.

⚠️ **Caution:** Exceptions thrown by `Arrays.copyOfRange()`:

| Exception 🚨 | Condition 📋 |
|--------------|-------------|
| **`ArrayIndexOutOfBoundsException`** | if `from < 0` or `from > original.length` |
| **`IllegalArgumentException`** | if `from > to` |
| **`NullPointerException`** | if original is `null` |

---

## 3. Copy Multidimensional Array using copyOfRange() of Java Arrays

The `Arrays.copyOfRange()` method also can be used to copy the [Java multidimensional array](027_Multidimensional_Array_in_Java.md) like [2D Java array](043_2D_Array_in_Java.md) and [3D Java array](044_3D_Array_in_Java.md).

**Copy two dimensional (2D) Java array using `Arrays.copyOfRange()`:**

```java
import java.util.Arrays;

public class Matrix1 {
  public static void main(String[] args) {

    // original 2D array 3x2
    int matrix[][] = { { 1, 2 }, { 4, 5 }, { 7, 8 } };
    System.out.println("Original = " +
               Arrays.deepToString(matrix));

    // Example1:- Copy 1st and 2nd 1D array
    int[][] newMatrix1 = Arrays.copyOfRange(matrix, 0, 2);
    System.out.println("newMatrix1 = " +
               Arrays.deepToString(newMatrix1));

    // Example2:- copy complete matrix
    int[][] newMatrix2 = Arrays.copyOfRange(matrix, 0, matrix.length);
    System.out.println("newMatrix2 = " +
               Arrays.deepToString(newMatrix2));

    // Example3
    int[][] newMatrix3 = Arrays.copyOfRange(matrix, 2, 6);
    System.out.println("newMatrix3 = " +
               Arrays.deepToString(newMatrix3));

  }
}
```

📤 **Output:**

```
Original = [[1, 2], [4, 5], [7, 8]]
newMatrix1 = [[1, 2], [4, 5]]
newMatrix2 = [[1, 2], [4, 5], [7, 8]]
newMatrix3 = [[7, 8], null, null, null]
```

> 💡 **Tip:** When the `to` index exceeds the original array length in a multidimensional copy, the extra positions are filled with `null` instead of zeros, since the inner arrays are objects.

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!
