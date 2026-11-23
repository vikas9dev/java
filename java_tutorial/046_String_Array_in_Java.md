# String Array in Java

**String Array in Java** | A String Array in Java is an object that holds a fixed number of `String` values. The array contains elements of similar data types in a contiguous memory location, and `String` contains the sequence of characters.

- [String Array Declaration in Java](#string-array-declaration-in-java)
- [Initialize String Array in Java](#initialize-string-array-in-java)
- [Java String Array Size](#java-string-array-size)
- [Java Print String Array](#java-print-string-array)
- [Convert String Array to String](#convert-string-array-to-string)
- [Java String Array Example](#java-string-array-example)
- [How to Merge Two String Arrays](#how-to-merge-two-string-arrays)
- [Dynamic String Array in Java](#dynamic-string-array-in-java)
- [Two Dimensional 2D String Array](#two-dimensional-2d-string-array)
- [String Array to Arraylist](#string-array-to-arraylist)
- [List to String Array](#list-to-string-array)
- [String Array To Set](#string-array-to-set)
- [Set to String Array in Java](#set-to-string-array-in-java)

---

When an array stores a fixed number of `String` values then it is called a String Array. Here you will learn how to declare and initialize the String array, how to find the size/length of the String array and how to iterate through it. What are the different ways to print or display the String array? Then you will see some examples on String array like sorting, searching, copying, and comparing. How to declare a two-dimensional String array. How to create a dynamic string array. Finally, we will discuss some conversions on String array like: String array to ArrayList, List to String array, String array to Set, Set to String array.

## 1. String Array Declaration in Java

Syntax to declare String array: `<Accessibility-modifier><Execution-level-modifiers> String[] <variable>;`

In the above declaration of String array, the accessibility modifier and execution-level modifier both are optional, only the variable-name is mandatory.

**Declaration examples:**

```java
String[] str;
public static String[] arr;
```

The rules for [array declaration in Java](026_Java_Array_[With_Examples].md) are also applicable here. Rules are like: Array size can't be mentioned in the declaration part (left side), `[]` is not allowed before `String`.

```java
String[] arr; // valid
String[3] arr; // error
String arr[3]; // error

String[] str; // valid
String [] str; // valid
String []str; // valid
String str[]; // valid
[]String str; // error
```

---

## 2. Initialize String Array in Java

Now let us see how to initialize String Array in Java. Similar to a normal array, the String array also can be initialized in three ways:

- 📦 String Array initialization with explicit values.
- 📦 String Array initialization with default values or without explicit values.
- 📦 Anonymous String array.

### Initialize with Explicit Values

Syntax: `<Accessibility-Modifier><Execution-level-modifiers> String[] <variable> = { <list-of-values-with-comma-separator> };`

**Example:**

```java
String language[] = {"Java", "Python", "C++"};
public static String arr[] = {"Know", "Program"};
```

⚠️ **Caution:** The limitation of this approach is that the String array must be declared and initialized in the same line, because array constants can only be used in initializers.

```java
// declaration
String language[];
// initialization
language = {"Java", "Python", "C++"}; // error
```

> 💡 **Tip:** We can use this approach only if the values/elements are known at the time of String array declaration.

### Initialize with Default Value

The default value for all referenced data types is `null`, and since `String` is also a referenced data type therefore the default value for the `String` is `null`.

Syntax: `<variable> = new String[<array-size>];`

**Example:**

```java
// String array declaration
String language[] = null;
// initialize with default value
language = new String[3];
```

Instead of two lines, we can declare and initialize within a single line:

```java
// declare and initialize with the default value
String language[] = new String[3];
```

We can access the array elements through their indexes and currently:

```java
language[0] = null;
language[1] = null;
language[2] = null;
```

### Anonymous String array

```java
// declaration
String language[] = null;
// initialize with default value
language = new String[]{"Java", "Python", "C++"};
```

✅ **Advantage of this approach:** In the first way of String array initialization i.e. while initializing the String array with explicit values, we must declare and initialize the array in a single line else we will get an error. But using this approach we can declare and initialize with explicit value at different lines.

---

## 3. Java String Array Size

To find the String array length in Java we can use the `length` property. By default every array variable contains the `length` property holding the total number of array elements.

**Find String array length:**

```java
public class StringArray {
  public static void main(String[] args) {
    // String array with explicit values
    String arr1[] = {"Know", "Program"};
    System.out.println("Length of String array arr1 = "
                      + arr1.length);

    // String array with default values
    String arr2[] = new String[9];
    System.out.println("Size of arr2 = " + arr2.length);

    // declaration
    String arr3[] = null;
    // initialize with default value
    arr3 = new String[]{"Java", "Python", "C++"};
    System.out.println("Size of arr3 = " + arr3.length);
  }
}
```

📤 **Output:**

```
Length of String array arr1 = 2
Size of arr2 = 9
Size of arr3 = 3
```

---

## 4. Java Print String Array

How to print string array in Java? To print a String array in Java we can iterate through the String array and fetch the content and display it. To iterate through it we can use the `length` property.

**Print String array using for loop:**

```java
public class StringArray {
  public static void main(String[] args) {
    String lang[] = {"Java", "Python", "C++"};
    for(int i=0; i<lang.length; i++) {
      System.out.println(lang[i]);
    }
  }
}
```

📤 **Output:**

```
Java
Python
C++
```

**Print String array with default values then after initialization:**

```java
public class StringArray {
  public static void main(String[] args) {
     // String array with default values
     String lang[] = new String[3];

     // display default value
     System.out.println("Default value of String array elements:");
     for(int i=0; i<lang.length; i++) {
       System.out.println(lang[i]);
     }

     // initialize String array
     lang[0] = "HTML";
     lang[1] = "CSS";
     lang[2] = "JavaScript";

     // display String array after initialization
     System.out.println("String array after initialization:");
     for(int i=0; i<lang.length; i++) {
       System.out.println(lang[i]);
     }
  }
}
```

📤 **Output:**

```
Default value of String array elements:
null
null
null
String array after initialization:
HTML
CSS
JavaScript
```

**Print String array using for-each loop:**

```java
public class StringArray {
  public static void main(String[] args) {
    String lang[] = {"Java", "Python", "C++"};
    for (String str : lang) {
      System.out.println(str);
    }
  }
}
```

📤 **Output:**

```
Java
Python
C++
```

**Print String array with default values using for-each loop:**

```java
public class StringArray {
   public static void main(String[] args) {
      // String array with default values
      String lang[] = new String[3];

      // display default value
      System.out.println("Default value of String array elements:");
      for (String str : lang) {
         System.out.println(str);
      }

      // initialize String array
      lang[0] = "HTML";
      lang[1] = "CSS";
      lang[2] = "JavaScript";

      // display String array after initialization
      System.out.println("String array after initialization:");
      for (String str : lang) {
         System.out.println(str);
      }
   }
}
```

📤 **Output:**

```
Default value of String array elements:
null
null
null
String array after initialization:
HTML
CSS
JavaScript
```

---

## 5. Convert String Array to String

In [java.util.Arrays class](033_Arrays_Class_Java_With_Examples.md), we have toString() method to convert the array to String. We can use this `Arrays.toString()` method for converting string array to string.

**Convert String array to String:**

```java
import java.util.Arrays;

public class StringArray {
  public static void main(String[] args) {
    // array with default value
    String lang[] = {"Java", "Python", "C++"};

    // convert String array to String
    String str = Arrays.toString(lang);

    // display String str
    System.out.println(str);
  }
}
```

📤 **Output:**

```
[Java, Python, C++]
```

**Display default and initialized values using `Arrays.toString()`:**

```java
import java.util.Arrays;

public class StringArray {
  public static void main(String[] args) {

    // String array with default values
    String lang[] = new String[3];

    // display default value
    System.out.println("Default value of String array elements:");
    System.out.println(Arrays.toString(lang));

    // initialize String array
    lang[0] = "HTML";
    lang[1] = "CSS";
    lang[2] = "JavaScript";

    // display String array after initialization
    System.out.println("String array after initialization:");
    System.out.println(Arrays.toString(lang));
  }
}
```

📤 **Output:**

```
Default value of String array elements:
[null, null, null]
String array after initialization:
[HTML, CSS, JavaScript]
```

---

## 6. Java String Array Example

Let us see some more examples on String array like taking input for String array, sorting the String array, searching for a string in the String array, comparing two String arrays, and more.

**Take String array input from end-user:**

```java
import java.util.Arrays;
import java.util.Scanner;

public class StringArray {

  public static void main(String[] args) {
    // Scanner class object to read input values
    Scanner scan = new Scanner(System.in);

    // declare String array
    String arr[] = null;

    // ask for the size of string array
    System.out.print("Enter size for String array: ");
    int size = scan.nextInt();

    // initialize String array with given size
    arr = new String[size];

    // display default value
    System.out.println("Default value of String array elements:");
    System.out.println(Arrays.toString(arr));

    // take input for String array elements
    System.out.println("Enter String array elements,");
    for (int i = 0; i < arr.length; i++) {
      arr[i] = scan.next();
    }

    // display String array after initialization
    System.out.println("String array after initialization:");
    System.out.println(Arrays.toString(arr));

    // close Scanner object
    scan.close();
  }
}
```

📤 **Output:**

```
Enter size for String array: 3
Default value of String array elements:
[null, null, null]
Enter String array elements,
Hi
Hello
Hey
String array after initialization:
[Hi, Hello, Hey]
```

### Sort String Array

To sort a given String we can use `Arrays.sort()` method. The `sort()` method of `java.util.Arrays` class is implemented based on dual-pivot Quicksort. This algorithm offers O(n log(n)) performance on all data sets. Learn more: [Sort an Array in Java - Arrays.sort() & Arrays.parallelSort()](035_Arrays.sort()_in_Java_With_Examples.md)

**Sort a String array:**

```java
import java.util.Arrays;

public class StringArray {
   public static void main(String[] args) {
      // String array with explicit values
      String lang[] = {"Java", "Python", "HTML", "C++", "CSS"};

      // display String array before sorting
      System.out.println("Initial String array,");
      System.out.println(Arrays.toString(lang));

      // Sort the String array
      Arrays.sort(lang);

      // display String array after sorting
      System.out.println("String array after sorting,");
      System.out.println(Arrays.toString(lang));
   }
}
```

📤 **Output:**

```
Initial String array,
[Java, Python, HTML, C++, CSS]
String array after sorting,
[C++, CSS, HTML, Java, Python]
```

### String Array contains

To search for a String in the given array of String we can use `Arrays.binarySearch()` method which is implemented based on binary search algorithm. See more: Binary Search program in Java.

> ⚠️ **Caution:** Condition to use binary search: The array must be sorted in ascending order. If the array is not sorted in ascending order then first sort the array and then use a binary search algorithm.

🔑 **Return value:** It returns the index of matched String, else it returns -1.

**Search for a String in a String array:**

```java
import java.util.Arrays;
import java.util.Scanner;

public class StringArray {
   public static void main(String[] args) {
      // String array with explicit values
      String lang[] = { "Java", "Python", "HTML", "C++", "CSS" };

      // Sort the String array
      Arrays.sort(lang);

      // take input for search key
      Scanner scan = new Scanner(System.in);
      System.out.print("Enter search key: ");
      String key = scan.next();

      // search for the key
      int index = Arrays.binarySearch(lang, key);
      // Note:- It will return the index of sorted array,
      // not the original array

      // display array
      System.out.println("After sorting the array is,");
      System.out.println(Arrays.toString(lang));

      // display result
      if (index != -1)
         System.out.println(key + " Found at index = " + index);
      else
         System.out.println(key + " not Found");

      // close Scanner class object
      scan.close();
   }
}
```

📤 **Output:**

```
Enter search key: C#
After sorting the array is,
[C++, CSS, HTML, Java, Python]
C# not Found

Enter search key: Java
After sorting the array is,
[C++, CSS, HTML, Java, Python]
Java Found at index = 3
```

### Copy

There are different ways to copy an array. See: How to copy an array in Java. In this example, we will use `Arrays.copyOf()` method given in `java.util.Arrays` class. The `Arrays.copyOf()` method internally uses `System.arraycopy()` method which is a native method and performs operations on operating system level. To copy the range of the String array we can use [Arrays.copyOfRange() method](037_Arrays.copyOfRange_in_Java_with_Example.md), which is very similar to `Arrays.copyOf()` method and internally uses `System.arraycopy()` method.

**Copy String array:**

```java
import java.util.Arrays;

public class StringArray {
  public static void main(String[] args) {
    // String array with explicit values
    String lang[] = { "Java", "Python", "HTML", "C++", "CSS" };

    // display original array
    System.out.println("Original array: ");
    System.out.println(Arrays.toString(lang));

    // copy String array
    String newArr[] = Arrays.copyOf(lang, lang.length);

    // display copied array
    System.out.println("Copied array: ");
    System.out.println(Arrays.toString(newArr));
  }
}
```

📤 **Output:**

```
Original array:
[Java, Python, HTML, C++, CSS]
Copied array:
[Java, Python, HTML, C++, CSS]
```

> 💡 **Tip:** On String arrays the `System.arraycopy()`, `Arrays.copyOf()`, and `Arrays.copyOfRange()` methods perform a **deep copy**. This means after copying, if we change the original array content then the copied String array won't be changed.

**Deep copy verification:**

```java
import java.util.Arrays;

public class StringArray {

   public static void main(String[] args) {
      // String array with explicit values
      String lang[] = { "Java", "Python", "HTML", "C++", "CSS" };

      // display original array
      System.out.println("Original array: ");
      System.out.println(Arrays.toString(lang));

      // copy String array
      String newArr[] = Arrays.copyOf(lang, lang.length);

      // display copied array
      System.out.println("Copied array: ");
      System.out.println(Arrays.toString(newArr));

      // changing original array content
      lang[0] = "English";

      // Now, display both array
      System.out.println("\nAfter modification of Original array: ");
      System.out.println(Arrays.toString(lang));
      System.out.println(Arrays.toString(newArr));
   }
}
```

📤 **Output:**

```
Original array:
[Java, Python, HTML, C++, CSS]
Copied array:
[Java, Python, HTML, C++, CSS]

After modification of Original array:
[English, Python, HTML, C++, CSS]
[Java, Python, HTML, C++, CSS]
```

### Check Equality

To check the equality of two String arrays we can use Arrays.equals() method. This method returns `true` if both arrays are equal else it returns `false`.

**Check equality of String arrays:**

```java
import java.util.Arrays;
public class StringArray {
   public static void main(String[] args) {

      // String array with explicit values
      String lang1[] = { "Java", "Python", "C++" };
      String lang2[] = lang1;
      String lang3[] = Arrays.copyOf(lang1, lang1.length);
      String lang4[] = { "HTML",  "CSS", "JavaScript" };

      // check
      System.out.println(Arrays.equals(lang1, lang2));
      System.out.println(Arrays.equals(lang1, lang3));
      System.out.println(Arrays.equals(lang1, lang4));
   }
}
```

📤 **Output:**

```
true
true
false
```

### Compare

To compare two String arrays we can use `Arrays.compare()` method. The `Arrays.compare()` method was introduced in **Java 9** version.

A `null` array reference is considered lexicographically less than a non-null array reference. Two `null` array references are considered equal.

| Return Value 🔢 | Condition 📋 |
|-----------------|-------------|
| **0** | If both String arrays are equal and contain the same string in the same order |
| **Less than 0** | If the first String array is lexicographically less than the second String array |
| **Greater than 0** | If the first String array is lexicographically greater than the second String array |

**Compare two String arrays:**

```java
import java.util.Arrays;
public class StringArray {
   public static void main(String[] args) {

      // String array with explicit values
      String lang1[] = { "Java", "Python", "C++" };
      String lang2[] = Arrays.copyOf(lang1, lang1.length);
      String lang3[] = { "JavaScript"};
      String lang4[] = { "HTML",  "CSS", "JavaScript" };

      // compare
      System.out.println(Arrays.compare(lang1, lang2));
      System.out.println(Arrays.compare(lang1, lang3));
      System.out.println(Arrays.compare(lang1, lang4));
   }
}
```

📤 **Output:**

```
0
-6
2
```

---

## 7. How to Merge Two String Arrays

**Java program to merge two String arrays:**

```java
import java.util.Arrays;

public class CopyArray {

   public static void main(String[] args) {

      // array which should be merged
      String src1[] = {"Java", "Python", "C++"};
      String src2[] = {"HTML", "CSS", "JavaScript"};

      // create new array
      String newArray[] = new String[src1.length + src2.length];

      // Copy first to new array from 0 to src1.length
      System.arraycopy(src1, 0, newArray, 0, src1.length);

      // copy second array to new array
      System.arraycopy(src2, 0, newArray, src1.length, src2.length);

      // display all array
      System.out.println("Array1 = " + Arrays.toString(src1));
      System.out.println("Array2 = " + Arrays.toString(src2));
      System.out.println("Merged Array = "
                     + Arrays.toString(newArray));
   }
}
```

📤 **Output:**

```
Array1 = [Java, Python, C++]
Array2 = [HTML, CSS, JavaScript]
Merged Array = [Java, Python, C++, HTML, CSS, JavaScript]
```

---

## 8. Dynamic String Array in Java

To create a dynamic string array, we can write code manually like how collection classes are implemented. For this, first create a String array with some small size (example 10), before adding an element in array check remaining size, if the remaining size is 0 then create another String array with more size (example 20) and copy data of existing array, and so on.

But instead of writing our own logic, it is better to use collections classes like `Set`, `List`, etc. They are growable and without size limitation.

**Dynamic String array using ArrayList:**

```java
import java.util.ArrayList;
public class StringArray {
   public static void main(String[] args) {

      // String array with explicit values
      ArrayList<String> str = new ArrayList<String>();

      // add elements
      str.add("Java");
      str.add("Python");
      str.add("C++");
      str.add("HTML");
      str.add("CSS");
      str.add("C++");

      // display arraylist
      for (String string : str) {
         System.out.println(string);
      }
   }
}
```

📤 **Output:**

```
Java
Python
C++
HTML
CSS
C++
```

---

## 9. Two Dimensional 2D String Array

A two-dimensional String array is a collection of single-dimensional String arrays, therefore it also can be called an array of arrays. It is specified by using two subscripts: row size and column size. More dimensions in an array mean more data can be stored in that array.

Similar to a normal two dimensional array, in Java we can also create a two dimensional String array. Learn more: [Two dimensional array in Java](043_2D_Array_in_Java.md)

**Two Dimensional String Array example:**

```java
import java.util.Arrays;
public class StringArray {
   public static void main(String[] args) {
      // Two dimensional String array
      // with explicit values
      String lang[][] = {
            { "Java", "Python", "C++" },
            { "HTML",  "CSS", "JavaScript" },
            { "English", "Spanish", "Hindi"}
      };

      // display String 2D array
      System.out.println(Arrays.deepToString(lang));
   }
}
```

📤 **Output:**

```
[[Java, Python, C++], [HTML, CSS, JavaScript], [English, Spanish, Hindi]]
```

---

## 10. String Array to Arraylist

To convert an array to ArrayList we can use `asList()` method given in the `java.util.Arrays` class. The `asList` method returns a fixed-size list backed by the specified array. Changes made to the array will be visible in the returned list, and changes made to the list will be visible in the array. The returned list is `Serializable` and it implements `RandomAccess`.

**Convert String array to ArrayList:**

```java
import java.util.Arrays;
import java.util.List;
public class StringArray {
   public static void main(String[] args) {

      // String with explicit values
      String lang[] = { "Java", "Python", "HTML", "C++", "CSS" };

      // display String array
      System.out.println("Array: "+Arrays.toString(lang));

      // convert to ArrayList
      List<String> list = Arrays.asList(lang);

      // display list
      System.out.println("List: " + list);

      // change content of array
      lang[0] = "English";

      // display both array and list
      System.out.println("After modification,");
      System.out.println("Array: "+Arrays.toString(lang));
      System.out.println("List: " + list);
   }
}
```

📤 **Output:**

```
Array: [Java, Python, HTML, C++, CSS]
List: [Java, Python, HTML, C++, CSS]
After modification,
Array: [English, Python, HTML, C++, CSS]
List: [English, Python, HTML, C++, CSS]
```

> 📝 **Note:** From this example, we can see that modification done in the array is also reflecting to the ArrayList.

---

## 11. List to String Array

In the below example, we have demonstrated three different ways to convert a list of String to the String array.

**Convert List to String array:**

```java
import java.util.Arrays;
import java.util.LinkedList;
import java.util.List;

public class StringArray {

   public static void main(String[] args) {
      List<String> list = new LinkedList<String>();
      list.add("Java");
      list.add("Python");
      list.add("Program");

      // Method-1: manually assigning to array
      String[] str1 = new String[list.size()];
      for (int i = 0; i < str1.length; i++) {
         str1[i] = list.get(i);
      }
      System.out.println("Array1: " + Arrays.toString(str1));

      // Method-2: using toArray() method
      String str2[] = list.toArray(new String[0]);
      System.out.println("Array2: " + Arrays.toString(str2));

      // Method-3: using Stream
      String[] str3 = list.stream().toArray(String[] ::new);
      System.out.println("Array3: " + Arrays.toString(str3));
   }
}
```

📤 **Output:**

```
Array1: [Java, Python, Program]
Array2: [Java, Python, Program]
Array3: [Java, Python, Program]
```

---

## 12. String Array To Set

To convert an array to a set we can take the help of `ArrayList` or `Stream`.

**Convert String array to Set using ArrayList:**

In this way, first convert the array to `ArrayList` and then convert the ArrayList to `Set` (`HashSet`). Here, modification done in the array doesn't reflect to the Set.

```java
import java.util.Arrays;
import java.util.HashSet;
import java.util.Set;

public class StringArray {
   public static void main(String[] args) {

      // String with explicit values
      String lang[] = { "Java", "Python", "HTML", "C++", "CSS" };

      // display String array
      System.out.println("Array: "+Arrays.toString(lang));

      // convert to set
      Set<String> set = new HashSet<>(Arrays.asList(lang));

      // display list
      System.out.println("Set: " + set);

      // change content of array
      lang[0] = "English";

      // display both array and list
      System.out.println("After modification,");
      System.out.println("Array: "+Arrays.toString(lang));
      System.out.println("Set: " + set);
   }
}
```

📤 **Output:**

```
Array: [Java, Python, HTML, C++, CSS]
Set: [Java, C++, CSS, HTML, Python]
After modification,
Array: [English, Python, HTML, C++, CSS]
Set: [Java, C++, CSS, HTML, Python]
```

**Convert String array to Set using Stream:**

```java
import java.util.Arrays;
import java.util.HashSet;
import java.util.Set;
import java.util.stream.Collectors;

public class StringArray {
   public static void main(String[] args) {

      // String with explicit values
      String lang[] = { "Java", "Python", "HTML", "C++", "CSS" };

      // display String array
      System.out.println("Array: "+Arrays.toString(lang));

      // convert to set
      Set<String> set =
        new HashSet<>(Arrays.stream(lang).collect(Collectors.toSet()));

      // display list
      System.out.println("Set: " + set);

      // change content of array
      lang[0] = "English";

      // display both array and list
      System.out.println("After modification,");
      System.out.println("Array: "+Arrays.toString(lang));
      System.out.println("Set: " + set);
   }
}
```

📤 **Output:**

```
Array: [Java, Python, HTML, C++, CSS]
Set: [Java, C++, CSS, HTML, Python]
After modification,
Array: [English, Python, HTML, C++, CSS]
Set: [Java, C++, CSS, HTML, Python]
```

---

## 13. Set to String Array in Java

**Convert Set to String array:**

```java
import java.util.Arrays;
import java.util.HashSet;
import java.util.Set;

public class StringArray {
   public static void main(String[] args) {

      // set must be of String type
      Set<String> set = new HashSet<>();
      set.add("Java");
      set.add("Python");
      set.add("C++");

      // create String array of set size
      String[] array = new String[set.size()];

      // convert set to array
      set.toArray(array);

      // display String array
      System.out.println("String Array: "
                + Arrays.toString(array));
   }
}
```

📤 **Output:**

```
String Array: [Java, C++, Python]
```

If you enjoyed this post, share it with your friends. Do you want to share more information about the topic discussed above or do you find anything incorrect? Let us know in the comments. Thank you!
