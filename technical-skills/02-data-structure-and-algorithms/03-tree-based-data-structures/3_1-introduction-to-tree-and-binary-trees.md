# 📖 Topic: Introduction to Trees & Binary Trees

## 💡 Basic knowledge required

- Understanding of nodes and pointers from the lesson on Linked Lists.

## 🎯 Learning Objectives

- Define a "Tree" as a hierarchical data structure.
- Identify and define key tree terminology (root, node, edge, parent, child, leaf).
- Define a "Binary Tree" and its specific property (each node has at most two children).
- Differentiate between various types of binary trees (Full, Complete, Perfect).

---

### 1. Introduction: Beyond Linearity

A **Tree** is a non-linear data structure composed of **Nodes** connected by **Edges** to represent a hierarchical relationship. A key characteristic is that there are no cycles within the structure.

Analogy: A family tree or an organizational chart is a real-life example. There is a single "ancestor" or "CEO" at the top (the **Root**), with branches extending to descendants or subordinates. Unlike a linked list where a node points to only one next node, a tree node can point to multiple child nodes.

### 2. Anatomy of a Tree

```
        A (Root)
       / \
(Edge)/   \
     /     \
    B (Parent) C (Sibling)
   / \
  D   E (Leaf)
```

-   **Node:** The basic unit of a tree, storing data and pointers to child nodes.
-   **Edge:** The connection between a parent node and a child node.
-   **Root:** The topmost node in the tree; it has no parent.
-   **Parent:** A node that has at least one child node.
-   **Child:** A node that has a parent node.
-   **Siblings:** A group of nodes with the same parent.
-   **Leaf:** A node with no children; the endpoint of a branch.
-   **Height:** The length of the longest path (number of edges) from the root to a leaf.
-   **Depth:** The length of the path from the root to a specific node.

### 3. The Binary Tree

A Binary Tree is a special, widely used type of tree with one crucial property:

**"Each node in the tree can have at most two children."**

These two children are referred to as the **Left Child** and the **Right Child**. This simple constraint makes binary trees easy to implement and analyze, and they form the basis for many highly efficient tree-based data structures like Binary Search Trees and Heaps.

**Recursive Definition:**
A binary tree is either:
1.  An empty tree.
2.  A root node with a left subtree and a right subtree, both of which are also binary trees.

### 4. Types of Binary Trees

-   **Full Binary Tree:** A binary tree where every node has either 0 or 2 children. (No nodes have only one child).
-   **Complete Binary Tree:** A binary tree in which every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible.
-   **Perfect Binary Tree:** A full binary tree in which all leaf nodes are at the same depth.

---

## 📋 Comprehensive Summary & Practical Exercise

### Comprehensive Summary

A tree is a hierarchical data structure used to model one-to-many relationships. A binary tree is a special type where each node has at most two children. Understanding the terminology (root, leaf, parent, child) is essential for studying this type of data structure.

### Practical Exercise

Draw a fictional company's organizational chart with a CEO at the top, two managers under the CEO, and each manager having two subordinates.
1.  What type of data structure is this chart?
2.  Who is the "Root" of this tree?
3.  In tree theory, what are the employees with no subordinates called?

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
