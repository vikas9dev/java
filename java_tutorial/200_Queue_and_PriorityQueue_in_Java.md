# Queue and PriorityQueue in Java

**Queue and PriorityQueue in Java** | Queue is the child interface of the [Collection interface](194_Java_Collection_Interface.md). In this blog, we will discuss the Queue interface and PriorityQueue class along with constructors, methods, and example programs.

- [PriorityQueue Class in Java](#priorityqueue-class-in-java)

---

## 1. Overview

**Implementation classes:**

- Collection(I) _1.2v_
  - Queue(I) _1.5v_
    - PriorityQueue _1.5v_
    - BlockingQueue _1.5v_
      - PriorityBlockingQueue _1.5v_
      - LinkedBlockingQueue _1.5v_
    - Other classes

If we want to represent a group of individual objects before processing then we should go for Queue. For example: before sending SMS messages, all mobile numbers have to be stored in some data structure. In which order we added the mobile number in the same order only the message should be delivered. For this first in first out requirement Queue is the best choice.

Usually, Queue follows FIFO (First in First out) order but based on our requirements we can implement our priority order also (`PriorityQueue`).

From the 1.5 version onwards `LinkedList` class also implements `Queue(I)`. LinkedList-based implementation of Queue always follows FIFO order.

```mermaid
graph LR
    IN[Enqueue] --> Q1[Front]
    Q1 --> Q2[...]
    Q2 --> Q3[Rear]
    Q3 --> OUT[Dequeue]

    classDef purple fill:#A162F7,stroke:#A162F7,color:#fff
    classDef cyan fill:#00b4d8,stroke:#00b4d8,color:#fff
    classDef green fill:#28C76F,stroke:#28C76F,color:#fff

    class IN green
    class Q1,Q2,Q3 cyan
    class OUT purple
```

**Queue(I) Specific Methods:**

- 📥 `boolean` **`offer(Object o)`** - To add an object into the queue.
- 👁️ `Object` **`peek()`** - To return the head element of the queue. If the queue is empty then this method returns `null`.
- 🔍 `Object` **`element()`** - To return the head element of the queue. If the queue is empty then it raises: `NoSuchElementException`.
- 📤 `Object` **`poll()`** - To remove and return the head element of the queue. If the queue is empty then this method returns `null`.
- 🗑️ `Object` **`remove()`** - To remove and return the head element of Queue. If the queue is empty then it raises: `NoSuchElementException`.

---

## 2. PriorityQueue Class in Java

- ⚖️ If we want a group of individual objects before processing according to some priority then we should go for `PriorityQueue`.
- 🔀 The priority can be a default natural sorting order or a customized sorting order defined by `Comparator(I)`.
- 📋 Insertion order is not preserved and it is based on some priority.
- ❌️ Duplicate objects are not allowed.
- 🏷️ If we are depending on the default natural sorting order then the objects should be homogeneous and `Comparable` otherwise we will get `ClassCastException`.
- 🔧 If we are defining our sorting by `Comparator` then objects need not be homogeneous and Comparable.
- 🚫 The `null` insertion is not allowed even as the 1st element also.

**Constructors of PriorityQueue Class in Java:**

- **`PriorityQueue();`** It creates an empty PriorityQueue with a default initial capacity of 11 and all objects will be inserted according to the default natural sorting order.
- **`PriorityQueue(int initialCapacity);`**
- **`PriorityQueue(int initialCapacity, Comparator c);`**
- **`PriorityQueue(SortedSet s);`**
- **`PriorityQueue(Collection c);`**

🛠️ **PriorityQueue example with default sorting:**

```java
import java.io.IOException;
import java.util.PriorityQueue;

public class Test {
    public static void main(String[] args) throws IOException {
        PriorityQueue<Integer> priorityQueue = new PriorityQueue<>();
        System.out.println(priorityQueue.peek()); // null

        // System.out.println(priorityQueue.element());
        // java.util.NoSuchElementException

        for (int i = 0; i <= 10; i++) {
            priorityQueue.offer(i);
        }
        System.out.println(priorityQueue);
        // [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

        System.out.println(priorityQueue.poll()); // 0
        System.out.println(priorityQueue);
        // [1, 3, 2, 7, 4, 5, 6, 10, 8, 9]
    }
}
```

In the last line, we were expecting `[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]` but we get `[1, 3, 2, 7, 4, 5, 6, 10, 8, 9]` i.e. the order is different.

> 📝 **Note:** Some platforms won't provide support for thread priorities and priority queues.

🛠️ **Demo Program for customized PriorityQueue:**

```java
import java.util.Comparator;
import java.util.PriorityQueue;
import java.util.Queue;

public class Test {
    public static void main(String[] args) {
        Queue<String> queue = new PriorityQueue<>(15, new Comparator<String>() {

            @Override
            public int compare(String o1, String o2) {
                return o2.compareTo(o1);
            }
        });
        queue.offer("A");
        queue.offer("Z");
        queue.offer("L");
        queue.offer("B");
        System.out.println(queue); // [Z, B, L, A]
    }
}
```
