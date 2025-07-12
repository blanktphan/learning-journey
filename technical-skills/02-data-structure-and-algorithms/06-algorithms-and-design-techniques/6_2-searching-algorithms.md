# 📖 Topic: Searching Algorithms: Binary Search

## 💡 Basic knowledge required

- The data in the collection (e.g., an array) must be **sorted**.
- An understanding of Big O Notation.

## 🎯 Learning Objectives

- Define the "searching problem" and explain the basic approach (Linear Search).
- Explain the algorithm and logic behind Binary Search.
- Analyze the time complexity of Binary Search (O(log n)) and compare it to Linear Search (O(n)).
- Understand the importance of sorted data as a prerequisite for this algorithm.

---

### 1. The Searching Problem and the Basic Approach

The **Searching Problem** is the process of finding the position of a target value within a collection of data.

The simplest approach is **Linear Search**, which involves checking each item one by one from the beginning to the end. While simple, it is highly inefficient for large datasets, with a time complexity of **O(n)**.

### 2. Binary Search: A Divide and Conquer Approach

**Binary Search** is a highly efficient searching algorithm that works only on **sorted** data structures. It uses a "divide and conquer" method by repeatedly **eliminating half** of the remaining search space in every comparison.

**Analogy:** It's like searching for a word in a dictionary. You don't start from the first page. You open to the middle, decide if your word is in the first or second half, discard the half you don't need, and repeat the process with the remaining section.

**Algorithm:**
1.  Define two pointers: `low` pointing to the start of the array (index 0) and `high` pointing to the end (index n-1).
2.  As long as `low` is less than or equal to `high`:
    a. Calculate the middle index: `mid = floor((low + high) / 2)`.
    b. Compare the `target` value with the value at `array[mid]`.
    c. **Case 1: Target Found.** If `target == array[mid]`, the search is successful. Return `mid`.
    d. **Case 2: Target is Smaller.** If `target < array[mid]`, the target must be in the **left half**. Discard the right half by setting `high = mid - 1`.
    e. **Case 3: Target is Larger.** If `target > array[mid]`, the target must be in the **right half**. Discard the left half by setting `low = mid + 1`.
3.  If the loop finishes without finding the target (when `low` becomes greater than `high`), the item is not in the array.

### 3. Performance Analysis

-   **Time Complexity: O(log n) (Logarithmic Time)**
    -   This is the greatest strength of Binary Search. With every comparison, the algorithm eliminates half of the search space. This means the number of steps required to find an item grows very slowly as the dataset size increases.
    -   For a dataset of 1 million items (n=1,000,000), Binary Search takes only about 20 comparisons in the worst case, whereas Linear Search could take up to 1,000,000.

-   **Space Complexity: O(1)**
    -   If implemented with a loop (the iterative version), it uses constant memory, as it only requires a few variables to store `low`, `high`, and `mid`.

### 4. The Critical Prerequisite: Sorted Data

This O(log n) performance is only possible under one strict condition: **the data must be sorted**. The algorithm relies on the sorted property to decide which half of the search space to discard.

**The Trade-off:** While there is an initial cost to sort the data (typically O(n log n)), if your system needs to perform many searches on that dataset, this one-time sorting cost is well worth the significantly faster search performance in the long run.

---

## 📋 Comprehensive Summary & Practical Exercise

### Comprehensive Summary

Binary Search is a highly efficient O(log n) algorithm for finding an item in a **sorted array**. It works using a divide and conquer approach, making it vastly faster than the O(n) Linear Search for large datasets.

### Practical Exercise

Given the sorted array: `[2, 5, 8, 12, 16, 23, 38, 56, 72, 91]`.
Trace the steps of the Binary Search algorithm to find the value `23`, showing the values of `low`, `high`, and `mid` for each iteration.

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
