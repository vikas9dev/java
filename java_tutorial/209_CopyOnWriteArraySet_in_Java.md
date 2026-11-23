# CopyOnWriteArraySet in Java

**CopyOnWriteArraySet in Java** | It is the part of `java.util.concurrent` package and works as a synchronized version of the Set. Also see: [CopyOnWriteArrayList In Java](208_CopyOnWriteArrayList_In_Java.md), [ConcurrentMap Interface in Java](207_ConcurrentMap_Interface_in_Java.md)

- [Difference between CopyOnWriteArraySet and synchronizedSet()](#difference-between-copyonwritearrayset-and-synchronizedset)

---

The `CopyOnWriteArraySet` hierarchy:

- 📦 Collection(I)
  - 🗂️ Set(I)
    - 🔒 CopyOnWriteArraySet

Key characteristics:

- 🛡️ It is the thread-safe version of Set.
- 📋 Insertion order is preserved.
- 🚫 Duplicate objects are not allowed.
- 🔄 Multiple threads can perform read operation simultaneously but for every update operation a separate cloned copy will be created.
- 💰 As for every update operation a separate cloned copy will be created which is costly hence if multiple update operations are required then it is not recommended to use CopyOnWriteArraySet.
- ✅ While one thread iterates Set the other threads are allowed to modify Set and won't get `ConcurrentModificationException`.
- ⚠️ The iterator of CopyOnWriteArraySet can perform only the read operation and won't perform any remove operation otherwise we will give `UnsupportedOperationException`.

**Constructors of CopyOnWriteArraySet:**

- ⚙️ `CopyOnWriteArraySet();`
- 📦 `CopyOnWriteArraySet(Collection c);`

It doesn't contain any specific methods.

**Example Program:**

```java
import java.util.concurrent.CopyOnWriteArraySet;
public class Test {
   public static void main(String[] args) {
      CopyOnWriteArraySet<String> cas =
           new CopyOnWriteArraySet<String>();
      cas.add("D");
      cas.add("B");
      cas.add("C");
      cas.add("A");
      cas.add(null);
      cas.add("D");
      System.out.println(cas); // [D, B, C, A, null]
   }
}
```

📤 **Output:**

```
[D, B, C, A, null]
```

📝 **Note:** The duplicate `"D"` was not added, preserving the Set property.

---

## 1. Difference between CopyOnWriteArraySet and synchronizedSet()

| Feature 🔍 | CopyOnWriteArraySet 🅰️ | SynchronizedSet() 🅱️ |
|------------|------------------------|---------------------|
| **Thread Safety** | ✅ Every update on separate cloned copy | ✅ Only one thread can operate at a time |
| **Modification During Iteration** | ✅ Allowed, no `ConcurrentModificationException` | ❌️ Throws `ConcurrentModificationException` |
| **Iterator Type** | Fail-safe | Fail-fast |
| **Iterator Operations** | Read only, remove throws `UnsupportedOperationException` | Both read and remove |
| **Version Introduced** | 1.5 | 1.2 |
