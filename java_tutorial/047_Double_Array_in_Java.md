# Double Array in Java

**Double Array in Java** | An array in Java used to store multiple `double` values in a single variable is called a double array. Double array example = {10.0, 15.9, 20.8, 45.5, 50.9}

- [Initialize Double Array in Java](#initialize-double-array-in-java)
- [Access and Modify](#access-and-modify)
- [Length or Size of double array](#length-or-size-of-double-array)
- [Print Double Array in Java](#print-double-array-in-java)
- [Double Array Example](#double-array-example)

---

## 1. Double Array Java Declaration

Before using any variable we must declare the variable. The syntax to declare the double array: `<Accessibility modifier><Execution-level Modifiers> double[] <variable>;`

In this syntax the accessibility-modifier and execution-level-modifiers are optional, but the remaining are mandatory.

**Declaration examples:**

```java
public static double[] arr1;
double[] arr2;
```

---

## 2. Initialize Double Array in Java

There are multiple ways to initialize the double array:

1. The double array initialization with explicit values
2. The double array initialization with default values (i.e. without explicit value)
3. Using [Anonymous Array](028_Anonymous_Array_in_Java_With_Example.md)

### 1) The double array initialization with explicit values

Full syntax: `<Accessibility modifier><Execution-level Modifiers> double[] <variable> = {<list-of-array-elements>};`

**Example:**

```java
double[] a1 = {10.0, 15.5, 20.9};
public static double[] a2 =
     {15.5, 25.5, 35.5, 45.5, 55.5};
```

In this way of double array initialization, the array is declared and initialized in the same line, because array constants can only be used in initializers. The accessibility modifier and execution level modifiers are optional.

> 📝 **Note:** We can use this approach only if the values are known at the time of double array declaration.

### 2) The double array initialization with default values

In this way, we can declare the array and initialize it later.

Syntax: `<array-variable> = new double[<size>];`

**Example:**

```java
// declare a double array
double[] arr = null;
// initialize double array with default values
arr = new double[5];
```

In this example, first, we had declared a double array then we had initialized it with the default value. Since it is an array of `double` data type and the default value for `double` type is 0.0, therefore this array is initialized with five 0.0 values. Later we can update the values by accessing the array elements.

Instead of two lines, we can declare and initialize within a single line:

```java
// declare and initilalize double array
double[] arr = new double[5];
```

### 3) Initialize double array using Anonymous Array

**Example:**

```java
// declare a double array
double[] arr1 = null;
// create array with explicit values
arr1 = new double[] {10.0, 15.5, 20.9};
```

✅ **Advantage of this approach:** In the first way of double array initialization i.e. while initializing the double array with explicit values, we must declare and initialize the array in a single line else we will get an error. But using this approach we can declare and initialize with explicit value at different lines.

---

## 3. Access and Modify

The double array can be accessed using `<array-variable>[index]`. Now, let us see it through an example.

**Declare double array of size 5 and initialize it with default value:**

```java
double[] a = new double[5];
```

**Currently:**

```java
a[0] = 0.0;
a[1] = 0.0;
a[2] = 0.0;
a[3] = 0.0;
a[4] = 0.0;
```

**Accessing and updating the array:**

```java
a[0] = 10.5;
a[1] = 20.5;
a[2] = 30.5;
a[3] = 40.5;
a[4] = 50.5;
```

It is similar to:

```java
double[] a = {10.5, 20.5, 30.5, 40.5, 50.5};
```

---

## 4. Length or Size of double array

The length or size of the double array can be found using the `length` property.

**Java program to find the length or size of double array:**

```java
public class DoubleArray {
   public static void main(String[] args) {
      double[] a = {10.5, 20.5, 30.5, 40.5, 50.5};
      System.out.println("Double Array Size = " + a.length);
   }
}
```

📤 **Output:**

```
Double Array Size = 5
```

---

## 5. Print Double Array in Java

To display a double array we can use loops or pre-defined methods. The loop can be for-loop, for-each loop, while loop, or do-while loop. While using loops we will use the `length` property.

**Print double array using for loop:**

```java
public class DoubleArray {
   public static void main(String[] args) {
      double[] a = {10.5, 20.5, 30.5, 40.5, 50.5};
      // display double array
      System.out.print("Double array = ");
      for (int i = 0; i < a.length; i++) {
         System.out.print(a[i]+" ");
      }
   }
}
```

📤 **Output:**

```
Double array = 10.5 20.5 30.5 40.5 50.5
```

**Print double array using for-each loop:**

```java
public class DoubleArray {
   public static void main(String[] args) {
      double[] a = {10.5, 20.5, 30.5, 40.5, 50.5};
      // display double array
      System.out.print("Double array = ");
      for (double d : a) {
         System.out.print(d+" ");
      }
   }
}
```

📤 **Output:**

```
Double array = 10.5 20.5 30.5 40.5 50.5
```

**Print double array using Arrays.toString() method:**

In addition to these ways, we have the [Arrays class](033_Arrays_Class_Java_With_Examples.md) defined in `java.util` package which contains lots of pre-defined methods related to the array. In this class `toString()` method is given to convert array to String.

```java
import java.util.Arrays;
public class DoubleArray {
   public static void main(String[] args) {
      double[] a = {10.5, 20.5, 30.5, 40.5, 50.5};
      // display double array
      System.out.print("Double array = " +
             Arrays.toString(a));
   }
}
```

📤 **Output:**

```
Double array = [10.5, 20.5, 30.5, 40.5, 50.5]
```

---

## 6. Double Array Example

Let us develop a **program to read input for a double array from the end-user and display it to the screen.** To read you can use command-line argument, `Scanner` class, `BufferedReader` class, or others. And to display you can use a loop or pre-defined method `Arrays.toString()`. In this program, we will use `Scanner` class and for-each loop.

**Read and display double array:**

```java
import java.util.Scanner;

public class DoubleArray {
   public static void main(String[] args) {

      // Scanner class object to read input
      Scanner scan = new Scanner(System.in);

      // declare double array
      double arr[] = null;

      // ask size of array
      System.out.print("Enter the size of the array: ");
      int size = scan.nextInt();

      // initialize double array with given size
      arr = new double[size];

      // display double array
      System.out.print("Double array = ");
      display(arr);

      // take input for the double array
      System.out.println("\nEnter elements for double array,");
      for (int i = 0; i < arr.length; i++) {
         arr[i] = scan.nextDouble();
      }

      // display double array
      System.out.print("Double array = ");
      display(arr);

      // close Scanner
      scan.close();
   }

   // method to display double array using for loop
   public static void display(double[] arr) {
      for (int i = 0; i < arr.length; i++) {
         System.out.print(arr[i]+" ");
      }
   }
}
```

📤 **Output:**

```
Enter the size of the array: 5
Double array = 0.0 0.0 0.0 0.0 0.0
Enter elements for double array,
10.5
20
30
55.9
453.96
Double array = 10.5 20.0 30.0 55.9 453.96
```

**Java program to add elements of double array:**

```java
public class DoubleArray {
   public static void main(String[] args) {
      // double array
      double[] arr = {10.5, 20.5, 30.5, 40.5, 50.5};
      double sum = 0.0;
      for (int i = 0; i < arr.length; i++) {
         sum += arr[i];
      }
      System.out.println("Sum = " + sum);
   }
}
```

📤 **Output:**

```
Sum = 152.5
```

### Java program to Sort double array

To sort an array we can use [Arrays.sort() method](035_Arrays.sort()_in_Java_With_Examples.md) given in [java.util.Arrays class](033_Arrays_Class_Java_With_Examples.md) which uses dual-pivot Quicksort. This algorithm offers O(n log(n)) performance on all data sets and is typically faster than traditional (one-pivot) Quicksort implementations.

> 💡 **Tip:** While working with [Java arrays](026_Java_Array_[With_Examples].md), no need to write your own logic to implement any sorting algorithm. Just import the `Arrays` class and use the `sort()` method which gives the best performance in most cases compared to other sorting algorithms.

```java
import java.util.Arrays;

public class DoubleArray {
   public static void main(String[] args) {

      // double array
      double[] arr = {50.5, 20.5, 40.5, 30.5, 10.5};

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

```
Before Sorting: [50.5, 20.5, 40.5, 30.5, 10.5]
After Sorting: [10.5, 20.5, 30.5, 40.5, 50.5]
```

### Copy double array in Java

To copy a double array we can use [System.arraycopy() method](031_System.arraycopy()_in_Java_with_Examples.md), [Arrays.copyOf()](036_Arrays.copyOf_in_Java_With_Example.md), or [Arrays.copyOfRange() method](037_Arrays.copyOfRange_in_Java_with_Example.md). The `Arrays.copyOf()` and `Arrays.copyOfRange()` methods internally use `System.arraycopy()` method therefore indirectly we will always use this method only. The `System.arraycopy()` method is a native method and performs copy operations on operating system level therefore it gives better performance compared to loops. For more see: Different ways to copy an array in Java.

```java
import java.util.Arrays;

public class DoubleArray {
   public static void main(String[] args) {

      // double array
      double[] arr = {50.5, 20.5, 40.5, 30.5, 10.5};

      // copy double array
      double[] copy = Arrays.copyOf(arr, arr.length);

      // display both array
      System.out.println("Original array: " + Arrays.toString(arr));
      System.out.println("Copied array: " + Arrays.toString(copy));
   }
}
```

📤 **Output:**

```
Original array: [50.5, 20.5, 40.5, 30.5, 10.5]
Copied array: [50.5, 20.5, 40.5, 30.5, 10.5]
```

### Convert int Array to double Array

**Java program to convert an int array to double array:**

```java
import java.util.Arrays;
public class DoubleArray {
   public static void main(String[] args) {

      // int array
      int arr[] = { 10, 40, 80, 20, 30 };

      // create new double array of similar size
      double newArr[] = new double[arr.length];

      // copy array elements
      for (int i = 0; i < arr.length; i++) {
         newArr[i] = arr[i];
      }

      // display both array
      System.out.println("The int array: " + Arrays.toString(arr));
      System.out.println("The double array: " +
                    Arrays.toString(newArr));
   }
}
```

📤 **Output:**

```
The int array: [10, 40, 80, 20, 30]
The double array: [10.0, 40.0, 80.0, 20.0, 30.0]
```

### double to byte Array

**Java program to convert double array to byte array.** The values of double array elements will be converted to the range of byte array.

```java
import java.util.Arrays;

public class DoubleArray {
   public static void main(String[] args) {

      // double array
      double arr[] = {50.5, 200.5, 40000.555, 3.5, 19000.5};

      // create new byte array of similar size
      byte newArr[] = new byte[arr.length];

      // copy array elements
      for (int i = 0; i < arr.length; i++) {
         // convert double to byte
         newArr[i] = (byte)arr[i];
      }

      // display both array
      System.out.println("The double array: " + Arrays.toString(arr));
      System.out.println("The byte array: " + Arrays.toString(newArr));
   }
}
```

📤 **Output:**

```
The double array: [50.5, 200.5, 40000.555, 3.5, 19000.5]
The byte array: [50, -56, 64, 3, 56]
```

### double array to float array

**Java program to convert double array to float array.** The values of double array elements will be converted to float type.

```java
import java.util.Arrays;
public class DoubleArray {
   public static void main(String[] args) {

      // double array
      double arr[] = {50.5, 40000.555, 999999999999999999.5};

      // create new float array of similar size
      float newArr[] = new float[arr.length];

      // copy array elements
      for (int i = 0; i < arr.length; i++) {
         // convert double to float
         newArr[i] = (float)arr[i];
      }

      // display both array
      System.out.println("The double array: " + Arrays.toString(arr));
      System.out.println("The float array: "
                         + Arrays.toString(newArr));
   }
}
```

📤 **Output:**

```
The double array: [50.5, 40000.555, 1.0E18]
The float array: [50.5, 40000.555, 9.9999998E17]
```

### double array to int array

**Java program to convert double array to int array:**

```java
import java.util.Arrays;
public class DoubleArray {
   public static void main(String[] args) {

      // double array
      double arr[] = {50.9, 40000.555, 999999999999999999.5};

      // create new int array of similar size
      int newArr[] = new int[arr.length];

      // copy array elements
      for (int i = 0; i < arr.length; i++) {
         // convert double to int
         newArr[i] = (int)arr[i];
      }

      // display both array
      System.out.println("The double array: " + Arrays.toString(arr));
      System.out.println("The int array: " + Arrays.toString(newArr));
   }
}
```

📤 **Output:**

```
The double array: [50.9, 40000.555, 1.0E18]
The int array: [50, 40000, 2147483647]
```

### double to char array

**Java program to convert double array to char array:**

```java
import java.util.Arrays;
public class DoubleArray {
   public static void main(String[] args) {

      // double array
      double arr[] = {50.9, 65.0, 98.0, 40000.555};

      // create new char array of similar size
      char newArr[] = new char[arr.length];

      // copy array elements
      for (char i = 0; i < arr.length; i++) {
         // convert double to char
         newArr[i] = (char)arr[i];
      }

      // display both array
      System.out.println("The double array: " + Arrays.toString(arr));
      System.out.println("The char array: " + Arrays.toString(newArr));
   }
}
```

📤 **Output:**

```
The double array: [50.9, 65.0, 98.0, 40000.555]
The char array: [2, A, b, 鱀]
```

### List to double Array

**Java program to convert list to double array:**

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class DoubleArray {
   public static void main(String[] args) {

      // list of double
      List<Double> list = new ArrayList<>();

      // create double array
      Double[] dblArray = new Double[list.size()];

      // add elements to the list
      list.add(343.34);
      list.add(432.34);

      // convert list to array
      dblArray = list.toArray(dblArray);

      // display both
      System.out.println("List: " + list);
      System.out.println("Array: " + Arrays.toString(dblArray));
   }
}
```

📤 **Output:**

```
List: [343.34, 432.34]
Array: [343.34, 432.34]
```

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!
