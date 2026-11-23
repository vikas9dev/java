# Anonymous Array in Java With Example

**Anonymous Array in Java With Example** | An array without having any name, used to pass an array with user values without a referenced variable.

- [Sample program using anonymous array in Java](#sample-program-using-anonymous-array-in-java)
- [When we should use anonymous array in Java?](#when-we-should-use-anonymous-array-in-java)
- [Example](#example)

In Java, an Array without having any name is called an anonymous array. Using anonymous array we can pass an array with user values without the referenced variable.

📋 **Syntax to create anonymous array in Java:**

`new <data type>[]{<list of values with comma separator>};`

**Examples:**

```java
new int[] {10, 20, 30, 40};
new char[] {'a', 'b'};
new int[] {}; // empty, no use
new int[][] { {40, 50}, {10, 20, 30} }; // anonymous multidimensional array
```

> 📝 **Note:** For Anonymous array creation, do not mention size in `[]`. The number of values passing in inside `{}` will become the size.

An Anonymous array can also be created with a referenced variable, but it is not recommended. It is only recommended to pass an array as an argument with explicit values without the referenced variable.

```java
int[] a = new int[] {9, 18, 27}; // we can do it, but not recommended
```

---

## 1. Sample program using anonymous array in Java

**Passing anonymous array to a method:**

```java
class AnonymousArrayExample{

  public static void main(String[] args) {
    // passing an Anonymous array to a method
    display(new int[] {1,2,3,4});
  }

  // method to display array elements
  static void display(int[] a){
    for(int i=0; i < a.length; i++){
      System.out.print(a[i]+"\t");
    }
  }

}
```

📤 **Output:**

```
1 2 3 4
```

> ⚠️ **Caution:** Anonymous array has no name so we can't access its index and can't modify its values after creation. Generally, it is used to pass or return multiple elements of the same type to another method.

---

## 2. When we should use anonymous array in Java?

There are three ways of array creation of Java. These ways are:

1. 📦 **Array creation with values.** It uses `{}` bracket. Example: `int[] a = {1,2,3,4};`
2. 📦 **Array creation without explicit values or with a default value.** It uses the `new` keyword and square bracket `[]`. Example: `int[] a = new int[4];`
3. 📦 **Anonymous array creation.** It uses an anonymous array i.e. `new` keyword, `[]` and `{}`. It is the combination of the previous two ways. Example: `new int[] {1,2,3,4};`

Now, question is when we should use which declaration?

- ✅ If we already know the type of values, the number of values, and also values of the array at the time of array creation then we should use the first way of creation i.e. [array creation with explicit values](026_Java_Array_[With_Examples].md).
- ✅ When we know only types of values and number of values to stored in the array then we should use the second way of creation i.e. [array creation without an explicit value](026_Java_Array_[With_Examples].md). Later we can update their value from the default value.
- ✅ If there is no use of array after some lines then we should use an anonymous array. We can't access elements of the anonymous array using an index.

---

## 3. Example

To understand the use of anonymous array check below program, `arithmeticOperation(-,-)` method. We want to write a method which takes two number as parameters and return its sum, subtraction, and multiplication. Using primitive data type we can return only one value so we need to use array. In the below program, `arithmeticOperation(-,-)` method return addition, subtraction, and multiplication values of the given numbers.

**Incomplete program (problem statement):**

```java
// Incomplete program
class Test{

  public static void main(String[] args) {
    int[] a = new int[3];
    a = arithmeticOperation(10, 5);
    System.out.println("Sum = "+a[0]);
    System.out.println("Sub = "+a[1]);
    System.out.println("multiply = "+a[2]);
  }

  static int[] arithmeticOperation(int a, int b){
    int add = a+b;
    int sub = a-b;
    int multiply = a*b;
    // write the logic
    // to return add, sub, multiply
  }

}
```

Now, how to write the logic to return add, sub, and multiply values. We will see the all three ways and compare them.

1️⃣ **Way 1 - Array creation with values:**

In array creation with values, first calculate the values of add, sub, multiply and then create an int array with these values and return them.

```java
static int[] arithmeticOperation(int a, int b){
  int add = a+b;
  int sub = a-b;
  int multiply = a*b;
  int[] arr = {add, sub, multiply};
  return arr;
}
```

2️⃣ **Way 2 - Array creation without explicit value:**

Here we must create an array having size of 3. Later calculate the add, sub, and multiple, and store them into the array. After storing return the array.

```java
static int[] arithmeticOperation(int a, int b){
  int[] arr = new int[3];
  arr[0] = a+b;
  arr[1] = a-b;
  arr[2] = a*b;
  return arr;
}
```

3️⃣ **Way 3 - Anonymous array (recommended):**

In the third way i.e using anonymous array simply calculate the add, sub, and multiply and return it.

```java
static int[] arithmeticOperation(int a, int b){
  int add = a+b;
  int sub = a-b;
  int multiply = a*b;
  return (new int[]{add, sub, multiply});
}
```

> 💡 **Tip:** In the first two ways of array creation, we created an array variable that needs memory to store array elements. Using Anonymous array we can do the same without using any extra memory. Lines of code also increased in those two ways in comparison to an anonymous array. The most important thing to note that there is no use of these array after the return. We are creating these arrays only to return the values otherwise there is no use of any array in this method. So, we should use an anonymous array.

**Complete program using anonymous array:**

```java
class Test{

  public static void main(String[] args) {
    int[] a = new int[3];
    a = arithmeticOperation(10, 5);
    System.out.println("Sum = "+a[0]);
    System.out.println("Sub = "+a[1]);
    System.out.println("multiply = "+a[2]);
  }

  static int[] arithmeticOperation(int a, int b){
    int add = a+b;
    int sub = a-b;
    int multiply = a*b;
    // return values using anonymous array
    return (new int[]{add, sub, multiply});
  }

}
```

📤 **Output:**

```
Sum = 15
Sub = 5
multiply = 50
```

---

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!

**Java Tutorial**
**Java Programs**
- [Array in Java](026_Java_Array_[With_Examples].md)
- [Multidimensional Array](027_Multidimensional_Array_in_Java.md)
- Anonymous Array
- [Array of Objects](029_Array_of_Objects_in_Java_With_Example.md)
- [Jagged Array](030_Jagged_Array_in_Java_with_Example.md)
- [System.arraycopy()](031_System.arraycopy()_in_Java_with_Examples.md)
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
