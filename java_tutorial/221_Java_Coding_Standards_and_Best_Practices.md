# Java Coding Standards and Best Practices

**Java Coding Standards and Best Practices** | Writing clean, readable, and maintainable Java code following industry standards and conventions.

- [Java Naming Conventions](#java-naming-conventions)
- [Google Java Style Guide](#google-java-style-guide)
- [Accessibility Modifier for Class Members](#accessibility-modifier-for-class-members)
- [In Concatenation Operation Using StringBuilder or StringBuffer instead of String](#in-concatenation-operation-using-stringbuilder-or-stringbuffer-instead-of-string)
- [Handle Null Pointer Exceptions Properly](#handle-null-pointer-exceptions-properly)

---

## 1. Java Naming Conventions

We are writing code not only for the computers but also for the other programmers who will later work on these codes. Assume we have written the unreadable code and after a few days or months, we want to modify some part of the code. In that case, we forget what we had done at the code development time and now we need to spend some time to understand what is going on in this part of the code.

> 💡 **Quote:**  
> Any fool can write code that a computer can understand. Good programmers write code that humans can understand.  
> — **Martin Fowler**

Naming conventions of identifiers make programs more understandable. These naming suggestions are **suggested by** Sun Microsystems (now **Oracle**) and Java communities. All Java APIs including JDK follow these naming conventions for classes, interfaces, packages, methods, variables, and constants.

According to Robert C. Martin (the author of Clean Code), an identifier should have the following characteristics: Self-explanatory, meaningful distinctions, and pronounceable.

| Identifier 🏷️ | Convention 📏 | Examples 🛠️ |
|---------------|--------------|-------------|
| **Packages** | All lowercase ASCII letters | `com.sun.eng`, `com.apple.quicktime.v2` |
| **Classes** | UpperCamelCase (noun/noun phrases) | `Employee`, `ImageSprite`, `BufferedReader` |
| **Interfaces** | UpperCamelCase (adjectives preferred) | `List`, `Cloneable`, `Serializable` |
| **Methods** | lowerCamelCase (verbs) | `toString()`, `getValue()`, `add()` |
| **Variables** | lowerCamelCase, short & meaningful | `out`, `balance`, `myHeight` |
| **Constants** | ALL_UPPERCASE with underscores | `MIN_WIDTH`, `MAX_PRIORITY` |

### Packages

- 📦 The **package name should contain only lowercase ASCII letters.**
- 🌐 The topmost package name should be the top-level domain names like `com`, `edu`, `org`, `gov`, `net`, etc.
- 🏗️ The subsequent components of the package name may vary based on the organization's own internal naming conventions.

### Classes

- 📝 The **class name should be noun or noun phrases**.
- 🔤 The **class name should be in UpperCamelCase** i.e the first letter of each word of the class name should be capitalized.
- ✅ We should try to keep the class names simple and descriptive.
- ❌️ Instead of using acronyms and abbreviations, we should use whole words.

### Interfaces

- 📝 Similar to the class names, the **interface name also should be UpperCamelCase**.
- 🏷️ The interface name can be noun or noun phrases but it is better to use **adjectives or adjective phrases**.
- 🛠️ Examples: `List`, `Collections`, `Reader`, `Writer`, `Storing`, `Cloneable`, `AutoCloseable`, `Serializable`

### Methods

- 📝 The **method name should be verbs**.
- 🔤 **Method name should be in lowerCamelCase** i.e. the first letter of the method name should be lowercase and the first letter of the next internal word onwards should be in uppercase.
- 🛠️ Examples: `toString()`, `add()`, `put()`, `getBackground()`, `print()`, `getValue()`

### Variables

- 📝 The **variable name also should be in lowerCamelCase**.
- ❌️ It **should not start with digits and any special character**.
- 💡 In variable names only `$` and `_` symbols are allowed as special characters but it is better to use camel case instead of these special characters.
- ⚠️ Only underscore (`_`) as the variable name is not allowed.
- ✅ Variable names should be short and meaningful.
- 🔤 One character variable name should not be used except for the temporary variables. Generally `i`, `j`, `k`, `m`, and `n` for integers; `c`, `d`, and `e` for characters are used for temporary variables.

### Constants

- 📝 The **constant names should be in all-uppercase**.
- 🔗 To separate words in the constant name we can use the underscore (`_`) symbol.
- 🛠️ Examples: `MIN_WIDTH`, `TOTAL_RUNS`, `MAX_PRIORITY`, `NORM_PRIORITY`

---

## 2. Google Java Style Guide

Google has also given Google's coding standards for source code in the Java programming language. The main points for Java Coding Standards are:

1. In the import statement, **don't use wildcard imports**.
2. All static imports should be in a single block and all the non-static imports should be in another block. Both blocks should be separated with a single blank line.
3. **Braces should be used** with conditional (`if-else`) and control flow (`while`, `do`, `for-loop`) statements **even though it contains only one statement**.
4. Place a blank line before the first member of the class.
5. Don't place a blank line after the last member of the class.
6. Write **one statement per line**.
7. Don't create local variables at the start of their containing block instead declare/initialize them close to the point they are first used, to minimize their scope.
8. Declare only **one variable per declaration**.
9. In switch case statement **include the default statement** even though it contains no code.
10. The order for the class and member modifiers recommended by Java Language specification: `public` => `protected` => `private` => `abstract` => `default` => `static` => `final` => `transient` => `volatile` => `synchronized` => `native` => `strictfp`
11. There should be **only one annotation per line** for the class/method/constructor.
12. **For long valued literals** always **use `L`** (uppercase letter) suffix, not the `l` (lowercase letter) i.e. use `50546L` but not `50546l`.
13. Whenever it is an overridden method then **use `@Override` annotation**.
14. The multiline comment style should be in `/* … */` style and each subsequent line must start with `*`.
15. It is extremely rare to override the `finalize()` method of the `Object` class.

> 💡 **Tip:** Following a consistent style guide across your team prevents bikeshedding and keeps code reviews focused on logic, not formatting.

---

## 3. Accessibility Modifier for Class Members

We should make our class members inaccessible as much as possible. The lowest possible access modifier for the member is `private`. This practice is used to develop encapsulation in software design.

**Bad practice -- public fields:**

```java
public class Student {

   public int sid;
   public String sname;
   public String address;
}
```

Since all fields are `public` therefore anyone can access them directly. We should assign a `private` accessibility modifier so that directly other classes can't access them. If other classes want to access these values then they can use the getter and setter methods of this class.

**Good practice -- private fields with getters/setters:**

```java
public class Student {

   private int sid;
   private String sname;
   private String address;

   public int getSid() {
      return sid;
   }

   public void setSid(int sid) {
      this.sid = sid;
   }

   public String getSname() {
      return sname;
   }

   public void setSname(String sname) {
      this.sname = sname;
   }

   public String getAddress() {
      return address;
   }

   public void setAddress(String address) {
      this.address = address;
   }
}
```

> 🔑 **Key Point:** Always prefer the lowest possible access modifier. Use `private` for fields, expose them through getter/setter methods only when needed.

---

## 4. In Concatenation Operation Using StringBuilder or StringBuffer instead of String

The string is one of the most commonly used classes in Java. The string is immutable and each modification done on a string object creates a new `String` object. If we are using `String` for modification, then unnecessarily it will create many `String` objects which are not useful for our program. Let us understand it through a `reverse()` method.

**Using String (creates unnecessary objects):**

```java
class Test {

   public static void main(String[] args) {
      String string = "Hello";
      System.out.println("Original String:: " + string);
      System.out.println("Reverse of String:: " + reverse(string));
   }

   public static String reverse(String string) {
      String reverseString = new String();
      for(int i=string.length()-1; i>=0; i--){
         reverseString = reverseString + string.charAt(i);
         System.out.println(reverseString + ", "
                  + System.identityHashCode(reverseString));
      }
      return reverseString;
  }
}
```

📤 **Output:**

```
Original String:: Hello
o, 1309552426
ol, 1943105171
oll, 1704856573
olle, 705927765
olleH, 366712642
Reverse of String:: olleH
```

In the above program, we can see that for each concatenation operation one new object is created because they have different hashcode values. Just to reverse "Hello" it has created 5 new objects which are not useful. Therefore it is better to use `StringBuffer` or `StringBuilder`. Both of these classes are mutable, and each modification will use an existing object rather than creating a new object.

| Feature ⚖️ | `StringBuffer` 🅰️ | `StringBuilder` 🅱️ |
|------------|-------------------|---------------------|
| **Mutability** | ✅ Mutable | ✅ Mutable |
| **Thread Safety** | ✅ Synchronized | ❌️ Non-synchronized |
| **Use Case** | Multi-threaded apps | Single-threaded apps |
| **Performance** | Slower (sync overhead) | ⚡ Faster |

📝 **Note:** We should develop our method in such a way that it should accept and return a `String` value, even if internally we use `StringBuilder`/`StringBuffer`. This avoids burdening other programmers with unnecessary type conversions.

**Using StringBuilder (reuses the same object):**

```java
public static String reverse(String string) {
   StringBuilder reverseString = new StringBuilder("");
   for(int i=string.length()-1; i>=0; i--){
      reverseString.append(string.charAt(i));
      System.out.println(reverseString + ", "
                    + System.identityHashCode(reverseString));
   }
   return reverseString.toString();
}
```

📤 **Output:**

```
Original String:: Hello
o, 622488023
ol, 622488023
oll, 622488023
olle, 622488023
olleH, 622488023
Reverse of String:: olleH
```

> ✅ **Result:** All concatenation operations reuse the same object (same hashcode), proving that `StringBuilder` is far more efficient for string modifications.

---

## 5. Handle Null Pointer Exceptions Properly

`NullPointerException` is one of the most common exceptions in Java. This exception occurs when we are trying to use an object but the object has a `null` reference. When we are accessing objects from other resources like databases, servers, files, etc., there is a high chance of getting a `null` reference. Therefore before using these objects we should check if it is `null` or not, and perform the operation only if it is not `null`.

**Null check example:**

```java
try(Connection connection =
           DriverManager.getConnection(url, user, password)) {
   if(connection != null) {
      // perform operations
   } else {
      System.out.println("Connection doesn't established successfully.");
      return;
   }
}
```

> ⚠️ **Caution:** Always perform null checks on objects obtained from external resources (databases, APIs, files) before using them.

If you want to learn more about Java coding standards then you can follow the below resources:

- 📖 [Oracle Java Code Conventions](https://www.oracle.com/java/technologies/javase/codeconventions-contents.html)
- 📖 [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html)
