# **TreeMap in Java Framework**

A **TreeMap** is part of the **Java Collections Framework** and is found in the **`java.util`** package. It implements the **`NavigableMap`** interface, which is a subtype of **`SortedMap`**, and is based on a **Red-Black Tree** (a self-balancing binary search tree).

---

### **Key Characteristics of TreeMap**

1. **Stores key-value pairs** like `HashMap`.
2. **Keys are sorted in natural order** (ascending by default), or by a custom comparator if provided.
3. **Does not allow null keys**, but allows multiple null values.
4. **Performance**: 
   - `O(log n)` time complexity for `put()`, `get()`, `remove()` operations.
5. **SortedMap implementation**: TreeMap automatically maintains the order of keys.
6. **Thread-unsafe**: Not synchronized by default.

---

### **Basic Example**

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        TreeMap<Integer, String> map = new TreeMap<>();

        map.put(3, "Apple");
        map.put(1, "Banana");
        map.put(2, "Orange");
        map.put(4, "Mango");

        System.out.println(map);
    }
}
```

**Output:**
```
{1=Banana, 2=Orange, 3=Apple, 4=Mango}
```

Note: The keys are **automatically sorted** in ascending order.

---


### **Common Methods in TreeMap**

- `put(K key, V value)` – Adds a key-value pair.
- `get(Object key)` – Returns the value for the given key.
- `remove(Object key)` – Deletes the mapping for the key.
- `firstKey()` / `lastKey()` – Returns the first/last key.
- `headMap(K toKey)` – Returns map of keys less than `toKey`.
- `tailMap(K fromKey)` – Returns map of keys greater than or equal to `fromKey`.
- `subMap(K fromKey, K toKey)` – Returns map from `fromKey` to `toKey`.



###  **Java Program: Demonstrating TreeMap Operations**

```java
import java.util.TreeMap;

public class TreeMapDemo {
    public static void main(String[] args) {
        // Creating a TreeMap
        TreeMap<Integer, String> students = new TreeMap<>();

        // Adding key-value pairs
        students.put(102, "Ravi");
        students.put(101, "Priya");
        students.put(104, "Amit");
        students.put(103, "Sneha");

        // Displaying the TreeMap
        System.out.println("TreeMap: " + students);

        // Getting a value by key
        System.out.println("Name with Roll 103: " + students.get(103));

        // Removing a key-value pair
        students.remove(102);
        System.out.println("After removing Roll 102: " + students);

        // Checking if a key exists
        System.out.println("Contains key 101? " + students.containsKey(101));

        // Checking if a value exists
        System.out.println("Contains value 'Amit'? " + students.containsValue("Amit"));

        // Size of TreeMap
        System.out.println("Total Students: " + students.size());

        // Iterating using for-each loop
        System.out.println("All Entries:");
        for (Integer key : students.keySet()) {
            System.out.println("Roll No: " + key + ", Name: " + students.get(key));
        }
    }
}
```

---

###  **Output:**

```
TreeMap: {101=Priya, 102=Ravi, 103=Sneha, 104=Amit}
Name with Roll 103: Sneha
After removing Roll 102: {101=Priya, 103=Sneha, 104=Amit}
Contains key 101? true
Contains value 'Amit'? true
Total Students: 3
All Entries:
Roll No: 101, Name: Priya
Roll No: 103, Name: Sneha
Roll No: 104, Name: Amit
```

---


### **Java Program: `TreeMap` with All Major Operations**

```java
import java.util.TreeMap;
import java.util.Map;

public class TreeMapOperations {
    public static void main(String[] args) {
        // Creating TreeMap with Integer keys and String values
        TreeMap<Integer, String> map = new TreeMap<>();

        // put() – Adding elements
        map.put(3, "Banana");
        map.put(1, "Apple");
        map.put(4, "Mango");
        map.put(2, "Orange");

        // Display TreeMap (Sorted by key)
        System.out.println("Original TreeMap: " + map);

        // get() – Accessing value by key
        System.out.println("Value at key 2: " + map.get(2));

        // remove() – Removing entry
        map.remove(3);
        System.out.println("After removing key 3: " + map);

        // containsKey() – Check for key
        System.out.println("Contains key 1? " + map.containsKey(1));

        // containsValue() – Check for value
        System.out.println("Contains value 'Mango'? " + map.containsValue("Mango"));

        // size() – Number of entries
        System.out.println("Size of TreeMap: " + map.size());

        // isEmpty() – Check if map is empty
        System.out.println("Is TreeMap empty? " + map.isEmpty());

        // firstKey() and lastKey() – Get first and last keys
        System.out.println("First Key: " + map.firstKey());
        System.out.println("Last Key: " + map.lastKey());

        // higherKey(), lowerKey() – Get key just higher/lower than given key
        System.out.println("Key higher than 2: " + map.higherKey(2));
        System.out.println("Key lower than 2: " + map.lowerKey(2));

        // keySet() – Getting all keys
        System.out.println("Keys: " + map.keySet());

        // values() – Getting all values
        System.out.println("Values: " + map.values());

        // entrySet() – Iterating through entries
        System.out.println("Entries:");
        for (Map.Entry<Integer, String> entry : map.entrySet()) {
            System.out.println("Key: " + entry.getKey() + ", Value: " + entry.getValue());
        }

        // clear() – Removing all entries
        map.clear();
        System.out.println("After clearing TreeMap: " + map);
    }
}
```

---

### **Expected Output:**

```
Original TreeMap: {1=Apple, 2=Orange, 3=Banana, 4=Mango}
Value at key 2: Orange
After removing key 3: {1=Apple, 2=Orange, 4=Mango}
Contains key 1? true
Contains value 'Mango'? true
Size of TreeMap: 3
Is TreeMap empty? false
First Key: 1
Last Key: 4
Key higher than 2: 4
Key lower than 2: 1
Keys: [1, 2, 4]
Values: [Apple, Orange, Mango]
Entries:
Key: 1, Value: Apple
Key: 2, Value: Orange
Key: 4, Value: Mango
After clearing TreeMap: {}
```
