# 📖 Topic: Arrays

## 💡 Basic knowledge required

- An understanding of memory as a sequence of addresses.
- Familiarity with Big O Notation (from Section 1).

## 🎯 Learning Objectives

- Define an "Array" as a contiguous block of memory for storing elements of the same type.
- Explain the concept of an "Index" and why it allows for O(1) random access.
- Analyze the time complexity of basic operations on an array.
- Understand the limitations of static arrays and the concept of dynamic arrays.

---

### 1. Definition and Memory Structure

An Array is a data structure consisting of a collection of elements of the same type, stored in a **contiguous memory block**.

This "contiguous" property is the key feature of an array. It means each element is stored right next to the previous one in memory. This allows the computer to instantly calculate the location of any element with a simple formula:

`address(i) = start_address + (i * element_size)`

```
Memory Address: 100  104  108  112  116
              +----+----+----+----+----+
Array:        | 10 | 25 | 5  | 99 | 12 |
              +----+----+----+----+----+
Index:          0    1    2    3    4
```

Analogy: An array is like a "row of lockers." Every locker is the same size and they are all next to each other. If you know where the first locker is, you can instantly calculate the location of the 100th locker without checking them one by one.

An **Index** is the number used to identify an element's position in the array, typically starting from 0 in most programming languages.

### 2. Performance Analysis

-   **Access: `array[i]`**
    -   Time Complexity: **O(1) (Constant Time)**
    -   This is the greatest strength of an array. Because of its contiguous nature, the location of any element can be calculated and accessed instantly, regardless of the array's size.

-   **Search:**
    -   Time Complexity: **O(n) (Linear Time)**
    -   If the array is not sorted, a Linear Search is required in the worst case, meaning we have to look at every element.

-   **Insertion/Deletion:**
    -   At the end (Appending): **O(1) amortized** on average. If there is space, adding to the end is very fast.
    -   At the beginning or middle: **O(n) (Linear Time)**
    -   This is the greatest weakness of an array. To insert or delete an element at the beginning, we must "shift" all subsequent elements one position, which is a very slow process for large arrays.

```
Operation | Access | Search | Insert/Delete (Mid)
-------------------------------------------------
Big O     | O(1)   | O(n)   | O(n)
```

### 3. Limitations and Solutions: Dynamic Arrays

In some low-level languages (like C), traditional **Static Arrays** have a fixed size that must be declared at creation and cannot be changed. This is inflexible.

Most high-level languages solve this by providing **Dynamic Arrays** (e.g., `List` in Python, `ArrayList` in Java).

**How it works:** It's an abstraction built on top of a static array.
1.  It starts by allocating an internal array of a certain size.
2.  When an element is added that exceeds the capacity, it performs a resize:
    a. Creates a new, larger array (typically 2x the size).
    b. Copies all elements from the old array to the new one.
    c. Adds the new element and deletes the old array.

**Amortized Analysis:** Although the resizing operation is slow (O(n)), it doesn't happen often. When averaged out with the many fast insertions, the average cost of adding an element is still considered O(1).

---

## 📋 Comprehensive Summary & Practical Exercise

### Comprehensive Summary

Arrays store same-type elements in contiguous memory, allowing for extremely fast O(1) access by index. However, their weakness is slow O(n) insertion or deletion at the beginning or middle due to the need to shift elements.

### Practical Exercise

Based on the performance characteristics of arrays, state whether an array is a "suitable" or "unsuitable" data structure for the following scenarios and explain why:

1.  Storing player data in an online game where you need to instantly retrieve the data for player number 500,000.
2.  Building the "Undo" system for a text editor, which frequently adds and removes the latest action at the "front" of the data.

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
