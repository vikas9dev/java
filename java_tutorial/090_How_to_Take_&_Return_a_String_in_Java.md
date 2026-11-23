# How to Take & Return a String in Java

**How to Take & Return a String in Java** | In the Java programming language `char[]`, `String`, `StringBuffer`, and `StringBuilder` are used to store, take and return string data. One question can come into your mind that *what is the best way for defining a method to take string data and return string data in Java?*

- [Using only StringBuilder to take and return string data in Java](#using-only-stringbuilder-to-take-and-return-string-data-in-java)
- [Using only StringBuffer to take and return string data in Java](#using-only-stringbuffer-to-take-and-return-string-data-in-java)
- [Then how we should write the method?](#then-how-we-should-write-the-method)
- [Related Links](#related-links)

---

We have four ways to take and return string data:

1. `char[]` / `byte[]`
2. `String`
3. `StringBuilder`
4. `StringBuffer`

The `char[]` is not a better option because it works on an array. Taking and returning string data using `char[]` is not a better option.

The second way is by using the `String` class. The `String` class is immutable. After every modification, it creates a new object. In this way, we are creating many new objects which are not actually required for our program. So, it is not recommended to only work with the `String` class. Read more: [Mutable and immutable](091_Immutable_Class_in_Java.md)

Below Java program to reverse String shows that, for a small task that is for reversing "Hello" it creates 5 objects.

**Reversing with String (creates multiple objects):**

```java
import java.util.Scanner;

public class ReverseString {

  public static void main(String[] args) {

    // take input
    Scanner scan = new Scanner(System.in);
    System.out.print("Enter string: ");
    String str = scan.nextLine();

    // reverse the string
    String reverseStr = reverseStringData(str);

    // display result string
    System.out.println( "Reverse String: " +
                           reverseStr);
  }

  public static String reverseStringData(String s) {

    String rev = new String();

    for(int i=s.length()-1; i>=0; i--){
      rev = rev + s.charAt(i);

      // On every iteration new string
      // object will be created
      System.out.println("Address of rev: "+
                  System.identityHashCode(rev));
    }

    return rev;
  }

}
```

📤 **Output:**

```
Enter string: Hello
Address of rev: 531885035
Address of rev: 1044036744
Address of rev: 1826771953
Address of rev: 1406718218
Address of rev: 245257410
Reverse String: olleH
```

> ⚠️ **Caution:** For big tasks, it will create so many string class objects, which actually don't need in the program. In this way, we are wasting memory.

---

## 1. Using only StringBuilder to take and return string data in Java

The third way is by using the `StringBuilder` class. The `StringBuilder` class is mutable. On every modification, it doesn't create a new object rather it stores in the same object. But the problem comes here: Since we are using `StringBuilder` to take an argument, so the caller method should pass the value in the `StringBuilder` form. Again, we are returning the string data using `StringBuilder` due to this the caller method should store returning value as `StringBuilder`.

The caller method developer needs to create a new `StringBuilder` object and convert the string data to `StringBuilder` just because the called method taking argument is in `StringBuilder` form not in the `String` form. Similarly, he/she needs to create a `StringBuilder` object just because the called method is returning the string data as `StringBuilder`.

**Reversing with StringBuilder (extra conversion needed):**

```java
import java.util.Scanner;

public class ReverseString {

  public static void main(String[] args) {

    // take input
    Scanner scan = new Scanner(System.in);
    System.out.print("Enter string: ");
    String str = scan.nextLine();

    // The reverseStringData() takes StringBuilder
    // objects we need to convert
    // string into StringBuilder
    StringBuilder sb = new StringBuilder(str);

    // Now, the return type is also StringBuilder
    // So, create new StringBuilder class object to
    // receive the return value
    StringBuilder reversrSb = reverseStringData(sb);

    // find reverse
    String reverseStr = new String(reversrSb);

    // display result
    System.out.println("Reverse String: "+reverseStr);
  }

  public static StringBuilder reverseStringData(StringBuilder sb){
    StringBuilder rev = new StringBuilder("");
    for(int i=sb.length()-1; i>=0; i--){
      rev.append(sb.charAt(i));
      // On every iteration new string object is created.
      System.out.println("Address of rev: "+
                    System.identityHashCode(rev));
    }
    return rev;
  }

}
```

📤 **Output:**

```
Enter string: Hello
Address of rev: 980546781
Address of rev: 980546781
Address of rev: 980546781
Address of rev: 980546781
Address of rev: 980546781
Reverse String: olleH
```

It doesn't create a new `StringBuilder` object, so no memory wastage but inside the caller method we need to write some extra logic for converting the string to `StringBuilder` and later `StringBuilder` to string. So, it is also not a recommended way. It is not the correct way, we should simplify these things.

---

## 2. Using only StringBuffer to take and return string data in Java

The fourth way is by using the `StringBuffer` class. The `StringBuffer` class is similar to the `StringBuilder` class. Implementation wise no difference will be there. `StringBuffer` class is synchronized so it is better for a multi-thread model application, not for the single thread model application. The `StringBuffer` class also will create the only object as `StringBuilder`, but we need to write extra logic for converting `StringBuffer` to `String` and `String` to `StringBuffer`.

**Reversing with StringBuffer (extra conversion needed):**

```java
import java.util.Scanner;

public class ReverseString {

  public static void main(String[] args) {

    // take input
    Scanner scan = new Scanner(System.in);
    System.out.print("Enter string: ");
    String str = scan.nextLine();

    // The reverseStringData() takes StringBuffer
    // object so converting string into StringBuffer
    StringBuffer sb = new StringBuffer(str);

    // Now, the return type is also StringBuffer
    // So, create new StringBuffer class object
    // to receive the return value
    StringBuffer reversrSb = reverseStringData(sb);

    // find reverse
    String reverseStr = new String(reversrSb);

    // display result
    System.out.println("Reverse String: "+reverseStr);
  }

  public static StringBuffer reverseStringData(StringBuffer sb){
    StringBuffer rev = new StringBuffer("");
    for(int i=sb.length()-1; i>=0; i--){
      rev.append(sb.charAt(i));
      System.out.println("Address of rev: " +
               System.identityHashCode(rev));
    }
    return rev;
  }

}
```

📤 **Output:**

```
Enter string: Hello
Address of rev: 980546781
Address of rev: 980546781
Address of rev: 980546781
Address of rev: 980546781
Address of rev: 980546781
Reverse String: olleH
```

It is also not a recommended way.

---

## 3. Then how we should write the method?

We should take and return the argument as a `String` class object. By this way, in the caller method, we don't need to write any additional logic in the caller method.

In the method, we should convert the `String` class object to the `StringBuilder` class, process the logic on the `StringBuilder` class, and then convert the `StringBuilder` class object to `String` class object and return it.

```mermaid
graph LR
    A["🔤 Take String argument"] --> B["🔄 Convert to StringBuilder"]
    B --> C["⚙️ Process business logic"]
    C --> D["🔄 Convert to String"]
    D --> E["📤 Return String"]

    classDef purple fill:#A162F7,stroke:#A162F7,color:#fff
    classDef cyan fill:#00b4d8,stroke:#00b4d8,color:#fff
    classDef green fill:#28C76F,stroke:#28C76F,color:#fff
    classDef orange fill:#FF9F43,stroke:#FF9F43,color:#fff

    class A purple
    class B cyan
    class C orange
    class D cyan
    class E green
```

💡 **Tip:** For converting `String` to `StringBuilder` class there is only one way: by using the `StringBuilder(String)` constructor.

For converting `StringBuilder` to `String` class object there are three ways:

1. `toString()`
2. `valueOf()`
3. `String(StringBuilder)`

Among these three ways, the first way that is using the `toString()` method is better than the remaining two.

**Recommended approach (String in, StringBuilder internally, String out):**

```java
import java.util.Scanner;

public class ReverseString {

  public static void main(String[] args) {

    // take input
    Scanner scan = new Scanner(System.in);
    System.out.print("Enter string: ");
    String str = scan.nextLine();

    // find reverse
    String reverseStr = reverseStringData(str);

    // display result
    System.out.println("Reverse String: " +
                              reverseStr);
  }

  public static String reverseStringData(String sb){

    // Converting string class object to
    // StringBuilder class object
    StringBuilder rev = new StringBuilder("");

    // iterate loop
    for(int i=sb.length()-1; i>=0; i--){
      rev.append(sb.charAt(i));
      System.out.println("Address of rev: "+
                     System.identityHashCode(rev));
    }

    // converting stringBuilder class object
    //  to string class object
    // and returning it to caller method
    return rev.toString();
  }
}
```

📤 **Output:**

```
Enter string: Hello
Address of rev: 980546781
Address of rev: 980546781
Address of rev: 980546781
Address of rev: 980546781
Address of rev: 980546781
Reverse String: olleH
```

🔑 **Key Point: Project development procedure:**

1. In projects, we store string data by using `java.lang.String` object.
2. To perform modifications on that string data we should convert/copy that string into the `StringBuilder` object.
3. After modification, we convert/copy back the result string data to the `String` object and return the result.

Please write comments if you find anything incorrect, or you want to share more information about the topic discussed above.

---

## 4. Related Links

- Leap year program in Java
- Find Factors of a number in Java
- LCM of two numbers
- HCF of two numbers
- Find Reverse of a number
- Kaprekar Number Program in Java

**String Programs**
- Sum of digits in a String
- Count No of Vowels String
- String Pattern Programs in Java
- Take String Input In Java
- Take Multiple String Input in Java
- How To Reverse a String In Java
- Remove Special Characters
- String - Remove Character
- String Palindrome In Java
- Sort String In Java
- How to Compare Strings In Java
- Second Occurrence of Character
- Replace nth Occurrence String
- Last Occurrence of Character
- Uppercase & Lowercase
- Java Check If Char is Uppercase
- Check If String is Uppercase
- Swap Characters in String Java
- [Java String indexOf() Method](110_Java_String_indexOf()_Method.md)
- How to Replace Dot in Java?
- [How to Find Length of String](099_How_to_Find_Length_of_String_in_Java.md)
- [Substring Method In Java](112_Substring_Method_In_Java.md)
- [Split Method In Java](119_Split()_Method_In_Java.md)
