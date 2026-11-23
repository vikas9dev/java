# How to Return an Array in Java

**How to Return an Array in Java** | [Array Programs in Java - 3](026_Java_Array_[With_Examples].md) | In the previous Java program, we have seen how to take array input in Java either from the end-user or a method. Now in this post, we will discuss how to return an array in Java.

- [Java Program to Return an array from a method](#java-program-to-return-an-array-from-a-method)
- [Return Array with User Input](#return-array-with-user-input)
- [Copy Array Through a Method](#copy-array-through-a-method)

---

To return an array from a method to another method in Java, first, we have to create an array and store array elements then simply return to the caller method.

Prerequisite: [Array in Java](026_Java_Array_[With_Examples].md)

To return an array we have to write the method such a way that:

- 🔢 **Return type** — It should be the data type and `[]`
- 📦 **Return value** — The method should return the array value with array-variable name.

**Method returning an array:**

```java
// method to return array elements
public static int[] readArray(){
  int[] arr = {10,20,30,40};
  return arr;
}
```

Let us assume we have an array of integer ([int data type](013_Data_Types_in_Java.md)) `arr = {10,20,30,40}` and we want to return it from the method. Then the return type should be `int[]`, because it is an array of `int` data types. Similarly, if it is an array of `double` then the return type should be `double[]`. For a single-dimensional array, only one square bracket `[]` is required, for a [two-dimensional array](043_2D_Array_in_Java.md), two square brackets `[][]` are required, and so on.

## 1. Java Program to Return an array from a method

**Return array with explicit values:**

```java
public class Test {

  // main method
  public static void main(String[] args) {

    // read array from a method
    int[] a = readArray();

    // display array elements
    for(int i=0; i < a.length; i++){
      System.out.print(a[i] + "\t");
    }
  }

  // method to return array elements
  public static int[] readArray(){
    int[] arr = {10,20,30,40};
    return arr;
  }

}
```

📤 **Output:**

```
10 20 30 40
```

---

## 2. Return Array with User Input

In the above program, we directly assigned array elements but we can also ask it from an end-user. See: how to take input for an array from end-user.

**Return array with user input:**

```java
import java.util.Scanner;
public class Test {

  // main method
  public static void main(String[] args) {

    // read array from a method
    int[] a = readArray();

    // display array elements
    System.out.println("Array elements are:");
    for(int i=0; i < a.length; i++){
      System.out.print(a[i]+"\t");
    }
  }

  // method to read array and
  // return array elements
  static int[] readArray(){

    // declare variables
    int n = 0;
    int[] arr = null;

    // Scanner class object to read input
    Scanner scan = new Scanner(System.in);

    // read number of elements
    System.out.print("Enter number of elements: ");
    n = scan.nextInt();

    // declare array
    arr = new int[n];

    // read array elements
    System.out.println("Enter elements:: ");
    for(int i=0; i < arr.length; i++)
    arr[i] = scan.nextInt();

    // close Scanner class object
    scan.close();

    // return array
    return arr;
  }
}
```

📤 **Output:**

```
Enter number of elements: 3
Enter elements::
15
85
56
Array elements are:
15 85 56
```

---

## 3. Copy Array Through a Method

**Program: Create `int[]` object with 5 values and copy elements of one array into the second array through a method (not directly). Display both array values.**

```java
public class ArrayOperation {
  int[] copyArray(int[] a){
    // returing array from method
    return a;
  }

  void displayArray(int[] a){
    for(int i=0; i < a.length; i++){
      System.out.print(a[i]+"\t");
    }
  }
}

class ArrayCopy{
  public static void main(String[] args) {
    ArrayOperation ao = new ArrayOperation();
    int[] arr1 = {10, 12, 15, 19, 25};

    // pass array to method
    int[] arr2 = ao.copyArray(arr1);

    //displaying first array elements
    System.out.println("First array elements:");
    // passing array to display method
    ao.displayArray(arr1);

    //displaying Second array elements
    System.out.println("\nSecond array elements:");
    // passing array to display method
    ao.displayArray(arr2);
  }
}
```

📤 **Output:**

```
First array elements:
10 12 15 19 25
Second array elements:
10 12 15 19 25
```

📝 **Note:** In the above program, we return an array to the method and also pass an array to the method. To make this program reusable we created a separate class with a method to copy the array elements.

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!
