# 📖 Topic: Heaps

## 💡 Basic knowledge required

- Understanding of binary tree structures, especially the Complete Binary Tree (from lesson 3.1).
- Familiarity with Big O Notation.

## 🎯 Learning Objectives

- Define a "Heap" as a tree-based data structure that satisfies the Heap Property.
- Differentiate between a Min-Heap and a Max-Heap.
- Describe the efficient array-based implementation of a heap.
- Analyze the time complexity of core heap operations (insert, extract-min/max).
- Understand the most important use case for a heap: implementing a Priority Queue.

---

### 1. Introduction: Beyond Searching

While Binary Search Trees (BSTs) are optimized for fast data **searching** using an ordering property, the **Heap** is another type of tree-based data structure designed not for searching, but for one primary goal: **instant access to the maximum or minimum element**.

### 2. The Heap Property

A Heap is a **Complete Binary Tree** that also satisfies an additional condition called the Heap Property. There are two types:

-   **Min-Heap:**
    -   The value of every parent node must be **less than or equal to** the value of its children.
    -   Result: The root node is always the **minimum value** in the heap.

-   **Max-Heap:**
    -   The value of every parent node must be **greater than or equal to** the value of its children.
    -   Result: The root node is always the **maximum value** in the heap.

```
      Min-Heap                Max-Heap
      +--------+              +--------+
      |   10   |              |   50   |
      |  /  \  |              |  /  \  |
      | 15  20 |              | 40  30 |
      +--------+              +--------+
```
Important: There is no ordering rule between siblings. A left child can be greater or smaller than a right child.

### 3. Array-Based Implementation

Because a heap is always a complete binary tree, we can represent it very efficiently in an **array**, saving memory by not needing pointers.

-   **Method:** Store nodes level by level, from left to right.
-   **Relationship Formulas:** For a node at index `i` in the array:
    -   Left child is at index `2*i + 1`
    -   Right child is at index `2*i + 2`
    -   Parent is at index `floor((i-1)/2)`

### 4. Core Heap Operations

When we add or remove data, we must run an algorithm to "fix" the heap to maintain its property. (Examples based on a Max-Heap):

-   **Insert:**
    -   **Algorithm (Bubble-up / Sift-up):**
        1.  Add the new element to the last available spot in the array (to keep it a complete tree).
        2.  Compare the new element with its parent.
        3.  If it's larger than its parent, swap them.
        4.  Repeat this comparison and swapping process (bubbling up) until it's in the correct position or becomes the root.
    -   **Time Complexity: O(log n)** because the height of the tree is log n.

-   **Extract-Max:**
    -   **Algorithm (Bubble-down / Sift-down):**
        1.  The max value is always at the root (index 0). Remove it.
        2.  Take the **last** element from the array and move it to the root's position.
        3.  This new root is likely violating the heap property. Fix it by comparing it to its children and swapping it with the **larger** child.
        4.  Repeat this comparison and swapping process (bubbling down) until it's in a valid position or becomes a leaf.
    -   **Time Complexity: O(log n)**.

### 5. Primary Application: Priority Queues

A **Priority Queue** is an Abstract Data Type (ADT) where each element has an associated "priority." When you dequeue, you always remove the element with the **highest priority**.

A heap is the best data structure for implementing a Priority Queue.
-   A **Max-Heap** implements a priority queue where a higher value means higher priority. The `extract-max` operation is the `dequeue`.
-   Use cases: CPU task scheduling in an operating system (more important jobs run first), Dijkstra's shortest path algorithm, and various event simulation systems.

---

## 📋 Comprehensive Summary & Practical Exercise

### Comprehensive Summary

A heap is a complete binary tree satisfying the min/max heap property. Its main goal is O(1) access to the min/max element and O(log n) insertion/deletion. It is typically implemented with an array and is the best choice for building a Priority Queue.

### Practical Exercise

Starting with an empty Max-Heap, draw the heap (as a tree) that results from inserting the following numbers in order: `10, 20, 15, 30, 40`. Afterwards, what does the heap look like after you perform one `extract-max` operation?

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
