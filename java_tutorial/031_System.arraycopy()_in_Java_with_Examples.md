# System.arraycopy() in Java with Examples

**System.arraycopy() in Java with Examples** | Copying arrays from source to destination using the native `System.arraycopy()` method.

- [Java Program to Copy Complete Array using System.arraycopy()](#java-program-to-copy-complete-array-using-systemarraycopy)
- [Copy Only Particular Elements](#copy-only-particular-elements)
- [Copy Array Elements to the Same Array](#copy-array-elements-to-the-same-array)
- [Exceptions thrown by the System.arrayCopy() Method in Java](#exceptions-thrown-by-the-systemarraycopy-method-in-java)
- [Copy Multidimensional Array using System.arraycopy() in Java](#copy-multidimensional-array-using-systemarraycopy-in-java)
- [Copy Object Array Using System.arraycopy() Method](#copy-object-array-using-systemarraycopy-method)
- [System.arraycopy() Performs Shallow or Deep Copy?](#systemarraycopy-performs-shallow-or-deep-copy)
- [Questions on System.arraycopy() in Java](#questions-on-systemarraycopy-in-java)

The `System.arraycopy()` method in Java is given to copy an array to another array. It copies an array from the specified source array, beginning at the specified position, to the specified position of the destination array.

📋 **Syntax of the `arraycopy()` method in `java.lang.System` class:**

```java
public static native void arraycopy(Object src,
    int srcPos, Object dest, int destPos, int length);
```

📝 **Arguments:**

- 📦 **src** - The source array.
- 🔢 **srcPos** - Starting position in the source array.
- 📋 **dest** - The destination array.
- 🔢 **destPos** - Starting position in the destination array.
- 🔢 **length** - The number of array elements to be copied.

> 💡 **Tip:** Since `java.lang.System` class is imported by default in all Java classes therefore to use `arraycopy()` method no need to explicitly import the System class.

---

## 1. Java Program to Copy Complete Array using System.arraycopy()

📋 **To copy the complete array using `System.arraycopy()` method:**

1. Take an array (source array)
2. Declare a new array with the same length. See: How to find the length of different arrays in Java?
3. Call `System.arraycopy(src, 0, dest, 0, src.length);`

```java
System.arraycopy(src, 0, dest, 0, src.length);
```

It will copy from the beginning of the source array to the beginning of the destination array until the length of the original array.

**Complete array copy example:**

```java
import java.util.Arrays;

public class ArrayTest {

  public static void main(String[] args) {

    // source array
    int src[] = {10, 15, 20, 25, 30};

    // destination array
    int dest[] = new int[src.length];

    // copy array using System.arraycopy
    System.arraycopy(src, 0, dest, 0, src.length);

    // display arrays
    System.out.println("Source array = " +
                        Arrays.toString(src));
    System.out.println("Destination array = " +
                        Arrays.toString(dest));

  }

}
```

📤 **Output:**

```
Source array = [10, 15, 20, 25, 30]
Destination array = [10, 15, 20, 25, 30]
```

---

## 2. Copy Only Particular Elements

Now let us see other examples of copying only some particular elements.

Assume we have an array of five integers:
`src = {10, 20, 30, 40, 50};`
And we have another array of integers with five zeros:
`dest = {0, 0, 0, 0, 0};`

Now, to copy 20, 30, 40 from the src array, we must pass `srcPos=0` and `length=3`. If we pass `destPos=1` then the destination array will fill up from the 1st index of the array to 1+3 = 4th position. No changes to the 0th and 5th index elements of the destination array.

```java
System.arraycopy(src, 0, dest, 1, 3);
```

Then: `Dest = {0,10,20,30,0};`

**Partial copy example:**

```java
import java.util.Arrays;

public class ArrayTest {

  public static void main(String[] args) {

    // source array
    int src[] = {10, 15, 20, 25, 30};

    // destination array
    int dest[] = new int[src.length];

    // copy array using System.arraycopy
    System.arraycopy(src, 0, dest, 1, 3);

    // display reverse of the array
    System.out.println("Source array = " +
                     Arrays.toString(src));
    System.out.println("Destination array = " +
                      Arrays.toString(dest));

  }

}
```

📤 **Output:**

```
Source array = [10, 15, 20, 25, 30]
Destination array = [0, 10, 15, 20, 0]
```

**Another example to copy particular elements using `arraycopy()` method:**

```java
// source array
int src[] = {10, 15, 20, 25, 30};

// destination array
int dest[] = new int[src.length];
// dest = {0, 0, 0, 0, 0};

// copy array using System.arraycopy
System.arraycopy(src, 0, dest, 0, 3);

// display the array
System.out.println("Destination Array = " +
                  Arrays.toString(src));
```

📤 **Output:**

```
Destination Array = [10, 15, 20, 0, 0]
```

---

## 3. Copy Array Elements to the Same Array

If the arguments for the source array and the destination refer to the same array object, then the copying is performed as if the components at positions `srcPos` through `srcPos+length-1` were first copied to a temporary array with length components and then the contents of the temporary array were copied into positions `destPos` through `destPos+length-1` of the destination array.

**Same array copy example:**

```java
int src[] = {10, 15, 20, 25, 30};
System.arraycopy(src, 0, src, 2, 3);

// display the array
System.out.println("Array = " +  Arrays.toString(src));
```

📤 **Output:**

```
Array = [10, 15, 10, 15, 20]
```

---

## 4. Exceptions thrown by the System.arrayCopy() Method in Java

The `java.lang.System.arraycopy()` method throws `NullPointerException`, `IndexOutOfBoundsException`, and `ArrayStoreException`.

🚨 **When it throws `NullPointerException`:**

- If the destination array is null.
- If the source array is null. In this case, the destination array won't be modified.

🚨 **When it throws `IndexOutOfBoundsException`** (In this case, the destination array won't be modified):

- Value for `srcPos`/`destPos`/`length` is negative.
- The `srcPos+length` is greater than the length of the source array.
- The `destPos+length` is greater than the length of the destination array.

🚨 **When it throws `ArrayStoreException`** (In this case, the destination array won't be modified):

- The src/dest refers to an object that is not an array.
- Both arrays component types are different primitive types.
- The src argument refers to an array with a primitive component type and the dest argument refers to an array with a reference component type.

---

## 5. Copy Multidimensional Array using System.arraycopy() in Java

We can also copy [multidimensional array](027_Multidimensional_Array_in_Java.md) like [2D array](043_2D_Array_in_Java.md) and [3D array](044_3D_Array_in_Java.md) using `System.arraycopy()` method. Let us demonstrate it through an example with the 2D array.

**Copy 2D array:**

```java
import java.util.Arrays;

public class ArrayTest {

   public static void main(String[] args) {

      // original 2D array 3x2
      int src[][] = { { 1, 2 }, { 4, 5 }, { 7, 8 } };

      // destination array
      int dest[][] = new int[3][2];

      // copy array using System.arraycopy
       System.arraycopy(src, 0, dest, 0, src.length);

      // display both array
      System.out.println("Source array = " +
                         Arrays.deepToString(src));
      System.out.println("Destination array = " +
                         Arrays.deepToString(dest) );

   }
}
```

📤 **Output:**

```
Source array = [[1, 2], [4, 5], [7, 8]]
Destination array = [[1, 2], [4, 5], [7, 8]]
```

---

## 6. Copy Object Array Using System.arraycopy() Method

Let us demonstrate an example to copy an [array of objects in Java](029_Array_of_Objects_in_Java_With_Example.md) using `System.arraycopy()` method.

**Student class:**

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

In Student class, we are overriding the toString() method to display the Student content. See: Example of Arrays.toString() with Object Array

**Copy object array:**

```java
import java.util.Arrays;
public class Collage {
   public static void main(String[] args) {
      // array of Student objects
      Student[] st = new Student[3];

      // initialize Student object
      st[0] = new Student(100, "Emma");
      st[1] = new Student(115, "Alex");
      st[2] = new Student(225, "Amelia");

      // display Student details (Original)
      System.out.println("Original Array= " +
                          Arrays.toString(st));

      // create new Student array
      Student[] newSt = new Student[st.length];
      // copy all Student objects
      System.arraycopy(st, 0, newSt, 0, st.length);
      // display new array
      System.out.println("Copied Array= " +
                          Arrays.toString(newSt));
   }
}
```

📤 **Output:**

```
Original Array= [[100, Emma], [115, Alex], [225, Amelia]]
Copied Array= [[100, Emma], [115, Alex], [225, Amelia]]
```

---

## 7. System.arraycopy() Performs Shallow or Deep Copy?

`System.arraycopy()` always performs **shallow copy**. It means when it is applied to non-primitive arrays then it copies Object references rather than object data.

We can demonstrate it through the multidimensional array. Multidimensional arrays are also called an array of arrays. We will use the previous 2D array.

**Shallow copy demonstration with 2D array:**

```java
// original 2D array 3x2
int src[][] = { { 1, 2 }, { 4, 5 }, { 7, 8 } };

// destination array
int dest[][] = new int[3][2];

// copy array using System.arraycopy
System.arraycopy(src, 0, dest, 0, src.length);

// display array (Before Modification)
System.out.println("Before Modification,");
System.out.println("Source array = " + Arrays.deepToString(src));
System.out.println("Destination array = " + Arrays.deepToString(dest));

// modify original array
src[0][0] = 999;
src[1][1] = 888;

// display array (After Modification)
System.out.println("\nAfter Modification,");
System.out.println("Source array = " + Arrays.deepToString(src));
System.out.println("Destination array = " + Arrays.deepToString(dest));
```

📤 **Output:**

```
Before Modification,
Source array = [[1, 2], [4, 5], [7, 8]]
Destination array = [[1, 2], [4, 5], [7, 8]]

After Modification,
Source array = [[999, 2], [4, 888], [7, 8]]
Destination array = [[999, 2], [4, 888], [7, 8]]
```

> ⚠️ **Caution:** We can notice that after copying the array when we changed the content of an element then the copied array element is also modified. Therefore we can say, it is performing shallow copy of the given array.

The [Arrays.copyOf() method](036_Arrays.copyOf_in_Java_With_Example.md) and [Arrays.copyOfRange() methods](037_Arrays.copyOfRange_in_Java_with_Example.md) of [java.util.Arrays class](033_Arrays_Class_Java_With_Examples.md) are internally using `System.arraycopy()` method therefore they are also performing shallow copy of the array.

**Shallow copy demonstration with object array:**

**Student class:**

```java
class Student {
   public int idNum;
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

**Test class:**

```java
import java.util.Arrays;
public class Collage {
   public static void main(String[] args) {
      // array of Student objects
      Student[] st = new Student[3];

      // initialize Student object
      st[0] = new Student(100, "Emma");
      st[1] = new Student(115, "Alex");
      st[2] = new Student(225, "Amelia");

      // create new Student array
      Student[] newSt = new Student[st.length];
      // copy all Student objects
      System.arraycopy(st, 0, newSt, 0, st.length);

      // display array (Before Modification)
      System.out.println("Before Modification,");
      System.out.println("Original Array= " + Arrays.toString(st));
      System.out.println("Copied Array= " + Arrays.toString(newSt));

      // modifying
      st[0].idNum = 99999999;

      // display array (After Modification)
      System.out.println("\nAfter Modification,");
      System.out.println("Original Array= " + Arrays.toString(st));
      System.out.println("Copied Array= " + Arrays.toString(newSt));

   }
}
```

📤 **Output:**

```
Before Modification,
Original Array= [[100, Emma], [115, Alex], [225, Amelia]]
Copied Array= [[100, Emma], [115, Alex], [225, Amelia]]

After Modification,
Original Array= [[99999999, Emma], [115, Alex], [225, Amelia]]
Copied Array= [[99999999, Emma], [115, Alex], [225, Amelia]]
```

---

## 8. Questions on System.arraycopy() in Java

**What is the time complexity of `System.arraycopy()` method in Java?**

- O(n), where N is the length to be copied (i.e. length argument). [See more](https://stackoverflow.com/questions/7165594/time-complexity-of-system-arraycopy)

**`System.arraycopy` source code?**

- The `arraycopy()` is a native method and it uses a direct memory copy outside of Java land. The native method is implemented in platform-dependent code, typically written in another programming language such as C, C++, FORTRAN, or assembly language. The body of a native method is given as a semicolon only, indicating that the implementation is omitted, instead of a block. Native methods and implemented differently by the Virtual Machine you are using. There is no one implementation of this method, and in fact, different codes may be executed on different architectures or VMS. [See more](https://stackoverflow.com/questions/12594046/java-native-method-source-code)

**Performance of `System.arraycopy`? Is it better to use `System.arraycopy()` than a for loop for copying?**

- The `arraycopy()` is likely the fastest way to copy an array, and it gives better performance compared to normal array copy using loops. It's in the system because it uses a direct memory copy outside of Java land. `java.lang.System` class provides useful methods for standard input and output, for loading files and libraries, or to access externally defined properties.

**`System.arraycopy()` performs shallow or deep copy?**

- `System.arraycopy()` always performs shallow copy. It means when `arraycopy()` applied to non-primitive arrays then it copies Object references rather than object data.

---

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

**Java Tutorial**
**Java Programs**
- [Array in Java](026_Java_Array_[With_Examples].md)
- [Multidimensional Array](027_Multidimensional_Array_in_Java.md)
- [Anonymous Array](028_Anonymous_Array_in_Java_With_Example.md)
- [Array of Objects](029_Array_of_Objects_in_Java_With_Example.md)
- [Jagged Array](030_Jagged_Array_in_Java_with_Example.md)
- System.arraycopy()
- [**Java Array Programs**](026_Java_Array_[With_Examples].md)

**Java Arrays Class**
- [Arrays Class & Methods](033_Arrays_Class_Java_With_Examples.md)
- Arrays.toString()
- [Arrays.sort() Method](035_Arrays.sort()_in_Java_With_Examples.md)
- [Arrays.copyof()](036_Arrays.copyOf_in_Java_With_Example.md)
- [Arrays.copyOfRange()](037_Arrays.copyOfRange_in_Java_with_Example.md)
- [Arrays.fill()](038_Arrays.fill()_–_Fill_Java_Arrays.md)
- Arrays.equals() Method

**Others**
- Get Array Input in Java
- [Return Array From Method](042_How_to_Return_an_Array_in_Java.md)
- [2D Array in Java](043_2D_Array_in_Java.md)
- [3D Array in Java](044_3D_Array_in_Java.md)
- [Matrix Tutorial in Java](045_Matrix_in_Java.md)
- [Array of String in Java](046_String_Array_in_Java.md)
- [Array of double in Java](047_Double_Array_in_Java.md)
