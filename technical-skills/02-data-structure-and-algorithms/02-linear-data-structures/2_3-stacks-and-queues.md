# 📖 Topic: Stacks and Queues

## 💡 Basic knowledge required

- Understanding of Abstract Data Types (ADTs) (from Section 1).
- Familiarity with Arrays and Linked Lists, which can be used to implement stacks and queues.

## 🎯 Learning Objectives

- Define Stack and Queue as ADTs with restricted data access.
- Explain the LIFO (Last-In, First-Out) principle of a Stack and its core operations (push, pop).
- Explain the FIFO (First-In, First-Out) principle of a Queue and its core operations (enqueue, dequeue).
- Identify and describe use cases for both Stacks and Queues in computing and real life.

---

### 1. Introduction: Restricted-Access Data Structures

Stacks and Queues are not complex new data structures. Instead, they are **Abstract Data Types (ADTs)** based on the concept of a List, but with intentionally **restricted access methods**.

This restriction is not a drawback; it is a **feature**. It gives these two structures a predictable behavior that is extremely useful for solving many types of computational problems.

### 2. The Stack: Last-In, First-Out (LIFO)

A Stack is a linear data structure that operates on the LIFO principle. This means the **last** element added is the **first** one to be removed.

Analogy: Imagine a "stack of plates." You can only place a new plate on the **top**, and when you take a plate, you must also take it from the **top**.

```
      pop() -> [ Item C   ]  <- push(C)
               [ Item B   ]
               [ Item A   ]
               +----------+
```

**Core Operations:**
-   `push(item)`: Adds a new item to the "top" of the stack.
-   `pop()`: Removes and returns the item from the "top" of the stack.
-   `peek()` or `top()`: "Looks at" the top item without removing it.

**Use Cases in Computing:**
-   **Function Call Stack:** How programming languages manage nested function calls. When function A calls B, B's data is pushed onto the stack. When B finishes, it's popped off, and control returns to A.
-   **Undo/Redo Systems:** Each user action is pushed onto a stack. Pressing "Undo" simply pops the last action.
-   **Syntax Checking:** Used to check for balanced parentheses, such as `()`, `{}`, `[]`, in source code.

### 3. The Queue: First-In, First-Out (FIFO)

A Queue is a linear data structure that operates on the FIFO principle. This means the **first** element added is the **first** one to be removed.

Analogy: It's exactly like a "line at a checkout counter." The first person to get in line is the first person to be served.

```
dequeue() <- [ P1 | P2 | P3 ] <- enqueue(P4)
(Front)                          (Back)
```

**Core Operations:**
-   `enqueue(item)`: Adds a new item to the "back" (or tail) of the queue.
-   `dequeue()`: Removes and returns the item from the "front" (or head) of the queue.
-   `peek()` or `front()`: "Looks at" the front item without removing it.

**Use Cases in Computing:**
-   **Task Scheduling:** A printer queue. The first print job submitted is the first one to be printed.
-   **Buffering:** Managing a data stream between a fast producer and a slow consumer, such as in video streaming.
-   **Graph Traversal Algorithms:** The Breadth-First Search (BFS) algorithm uses a queue to explore graph nodes level by level.

### 4. Implementation

Both stacks and queues can be implemented using an **Array** or a **Linked List** as the underlying data structure, each with different performance trade-offs.

---

## 📋 Comprehensive Summary & Practical Exercise

### Comprehensive Summary

Stacks and Queues are list-like ADTs with restricted access. A **Stack** is LIFO (Last-In, First-Out), like a stack of plates, used for function calls or undo systems. A **Queue** is FIFO (First-In, First-Out), like a waiting line, used for task scheduling.

### Practical Exercise

For the following systems, state whether you should use a **Stack** or a **Queue** and why:
1.  A web browser's history system, where the "Back" button must take you to the most recently visited page.
2.  A restaurant's order management system, where the chef must prepare dishes in the order they were received.

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
