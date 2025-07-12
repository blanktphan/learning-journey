# 📖 Topic: Binary Search Trees (BST)

## 💡 Basic knowledge required

- Understanding of the structure and terminology of binary trees (from lesson 3.1).
- Familiarity with Big O Notation.

## 🎯 Learning Objectives

- Define a Binary Search Tree and its core ordering property.
- Explain the algorithms for searching, inserting, and deleting data in a BST.
- Analyze the time complexity (Big O) of these operations in both balanced and unbalanced cases.
- Understand the critical limitation of a BST (the risk of the tree becoming unbalanced).

---

### 1. Definition and The Key Property

A Binary Search Tree (BST) is a special type of binary tree built with a strict **Ordering Property**:

For any given node in the tree:
1.  All values in its **left subtree** must be **less than** the node's value.
2.  All values in its **right subtree** must be **greater than** the node's value.
3.  Both the left and right subtrees must also be binary search trees.

This property is the heart of what makes a BST a powerful data structure for searching.

```
      [10]
      /  \
   (<10) (>10)
    /      \
  [5]      [15]
```

### 2. Operations on a BST

The ordering property makes operations highly efficient.

#### Search
-   **Algorithm:** Start at the root. Compare the target value with the current node's value:
    -   If equal -> Found.
    -   If less -> Go to the left child.
    -   If greater -> Go to the right child.
-   Repeat this process until the value is found or you reach a null link (meaning the value is not in the tree). This logic is identical to a Binary Search in a sorted array.

#### Insertion
-   **Algorithm:** Perform a "search" for the value you want to insert. This search will end at a null child link. That position is precisely where the new node should be inserted to maintain the BST property.

#### Deletion
This is the most complex operation, with three cases for the node to be deleted:
1.  **Node is a Leaf:** It can be removed directly.
2.  **Node has one child:** "Bypass" the node by pointing its parent directly to its child.
3.  **Node has two children:**
    a. Find a replacement node, typically the **in-order successor** (the smallest value in the right subtree).
    b. Copy the successor's value to the node being deleted.
    c. Delete the original successor node (which now becomes an easier case 1 or 2 deletion).

### 3. Performance Analysis and Limitations

#### Best/Average Case (Balanced Tree)
-   If the tree is reasonably "balanced" (the height of left and right subtrees are similar), the tree's height is approximately log₂(n).
-   **Time Complexity (Search, Insertion, Deletion): O(log n)**
-   This logarithmic performance is the ideal and the primary reason for using a BST.

#### Worst Case (Unbalanced / Degenerate Tree)
-   **Problem:** If you insert data that is already sorted (e.g., 10, 20, 30, 40, 50), the resulting BST will have no branches. It will become a long, straight line, behaving exactly like a Linked List.
-   **Time Complexity (Search, Insertion, Deletion): O(n)**
-   In this case, the BST's performance degrades to that of a simple list search, which is very poor.

The key takeaway: **The performance of a BST is critically dependent on its height.**

---

## 📋 Comprehensive Summary & Practical Exercise

### Comprehensive Summary

A BST is a binary tree with a `left < root < right` ordering property, which allows for efficient O(log n) search, insertion, and deletion on average. Its critical weakness is that performance degrades to O(n) if the tree becomes unbalanced.

### Practical Exercise

Starting with an empty BST, draw the tree that results from inserting the following numbers in order: `8, 3, 10, 1, 6, 14, 4, 7, 13`. Then, describe the steps to search for the number `6` in the tree you drew.

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
