# 📖 Topic: Hash Tables

## 💡 Basic knowledge required

- An understanding of hash functions and the collision problem.
- Familiarity with Arrays and Linked Lists.

## 🎯 Learning Objectives

- Define a "Hash Table" as a data structure that uses a hash function to map keys to values.
- Explain and compare the main collision resolution strategies: Separate Chaining and Open Addressing.
- Analyze the time complexity of hash table operations in both average and worst-case scenarios.
- Understand the importance of Load Factor and Rehashing.

---

### 1. Introduction: Implementing the Hashing Concept

A **Hash Table**, also known as a **Hash Map**, is a data structure that implements the hashing concept to create a mapping between a **Key** and its associated **Value**. It is the practical implementation of an Abstract Data Type (ADT) called a Dictionary or Associative Array.

The fundamental structure of a hash table is an **Array**, often called a Table or Bucket Array. The index for this array is calculated from the key using a hash function.

### 2. Collision Resolution Strategies

This is the critical part that makes hash tables practical. When more than one key hashes to the same index, we need a way to handle it.

#### A. Separate Chaining
-   **Concept:** Instead of each array slot holding a single value, it holds another data structure capable of storing multiple items. The most popular choice is a **Linked List**.
-   **How it works:**
    1.  When a new key-value pair is added, calculate its index using the hash function.
    2.  Go to the array bucket at that index.
    3.  Add the new key-value pair to the linked list within that bucket.

```
Index |
------+
  0   | -> null
  1   | -> [Key: "Bob", Val: 789] -> null
  2   | -> [Key: "Alice", Val: 123] -> [Key: "David", Val: 456] -> null
...   |
(Keys "Alice" and "David" both hashed to index 2)
```

-   **Analogy:** A hotel with a fixed number of rooms (buckets). When a new guest (key) wants a room that's already occupied, the hotel adds an extra bed (a node in the linked list) to that room.
-   **Pros:** Simple to implement and analyze; performance degrades gracefully as the table fills up.

#### B. Open Addressing
-   **Concept:** All data is stored directly within the array itself. If the target slot is occupied (a collision occurs), a **"probing strategy"** is used to find the next available empty slot.
-   **How it works (with Linear Probing):**
    1.  Calculate the index `i` from the key.
    2.  If `array[i]` is empty, insert the data there.
    3.  If `array[i]` is occupied, try `array[i+1]`, then `array[i+2]`, and so on, until an empty slot is found.
-   **Analogy:** Finding a spot in a parking lot. If your preferred spot (the calculated index) is taken, you drive to the next spot, and the next, until you find an empty one.
-   **Pros:** Can have better performance than separate chaining in some cases due to better CPU cache utilization and no overhead from creating list nodes.

### 3. Performance Analysis and Load Factor

-   **Average Case:**
    -   **Time Complexity (Search, Insertion, Deletion): O(1)**
    -   This is the primary reason hash tables are so powerful. With a good hash function and proper collision handling, most operations take constant time, regardless of the number of items (n).

-   **Worst Case:**
    -   **Time Complexity: O(n)**
    -   This occurs with a very poor hash function that causes **all keys to collide at a single index**. In this scenario, the hash table effectively degrades into a single, long Linked List.

-   **Load Factor (α):**
    -   **Definition:** A ratio that measures how "full" the hash table is.
    -   `α = number of items (n) / size of the array (m)`
    -   **Importance:** As the load factor gets high (e.g., > 0.75), the probability of collisions increases dramatically, which degrades performance.

-   **Rehashing:** To maintain O(1) performance, when the load factor exceeds a set threshold, the hash table performs a **rehash**. This involves creating a new, larger array (typically 2x the size) and re-inserting all existing items into this new array using the hash function.

---

## 📋 Comprehensive Summary & Practical Exercise

### Comprehensive Summary

A hash table is a data structure that uses a hash function to map keys to values, enabling average-case O(1) operations. Its effectiveness hinges on a good **collision resolution strategy**, such as **Separate Chaining** (using linked lists) or **Open Addressing** (finding the next empty slot).

### Practical Exercise

Assume you are building a hash table using **Separate Chaining** with an array of size 10 (indices 0-9). Your hash function is `hash(key) = key % 10`. If you insert the following items in order: `(key=12, value="A")`, `(key=22, value="B")`, `(key=3, value="C")`, describe where each item is stored in the hash table.

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
