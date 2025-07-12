# 📖 Topic: Abstract Data Types (ADT)

## 💡 Basic knowledge required

- A basic understanding of what a data structure is (from lesson 1.1).
- Familiarity with the concept of abstraction.

## 🎯 Learning Objectives

- Define "Abstract Data Type (ADT)" as a mathematical model for a data type.
- Distinguish the key difference between an ADT (logical description) and a Data Structure (concrete implementation).
- Describe the components of an ADT: the data it stores and the operations it supports.
- Understand how an ADT serves as a "blueprint" for designing and reasoning about data structures.

---

### 1. Introduction: Separating "What" from "How"

In engineering, we often separate the concept of "WHAT it does" from "HOW it does it."

**Example: The concept of a "Car"**
-   **WHAT (Behavior):** A car is something that can `startEngine()`, `accelerate()`, `brake()`, and `turn()`. This is a behavioral definition. We don't care if it uses a combustion engine, an electric motor, or nuclear power.
-   **HOW (Implementation):** This refers to the engineering details, such as a gasoline engine, an electric motor, or a four-wheel-drive system. These are all different "methods" of implementing a "car."

An Abstract Data Type (ADT) is the "WHAT" side of this concept. It is a **mathematical or logical model** of a data type defined solely by its **behavior** (what data it can hold and what operations can be performed on it), while intentionally **hiding all implementation details.**

### 2. ADT vs. Data Structure

This is the most critical distinction to understand:

-   **ADT (The "Blueprint"):**
    -   It is a logical description, a set of specifications, an interface.
    -   It defines WHAT can be done and what results to expect.
    -   Example: A "List" is an ADT that specifies an ordered collection of data supporting operations like `add`, `remove`, and `get`.

-   **Data Structure (The "Building"):**
    -   It is the concrete, physical implementation—the code and memory structure that makes the ADT work.
    -   It defines HOW those operations are actually carried out.

```
+-----------+      can be implemented by
|    ADT    |      (one-to-many)
|  (Logic)  |----------------+
+-----------+                |
                             v
           +------------------+ +------------------+
           | Data Structure 1 | | Data Structure 2 |
           | (e.g., Array)    | | (e.g., Linked List)|
           +------------------+ +------------------+
```

**Example: The List ADT**

-   **Logical Description (ADT):** A List is an ordered collection of data that supports `add(item)`, `remove(index)`, and `get(index)`.
-   **Concrete Implementations (Data Structures):**
    1.  **Array-based List:**
        -   **How:** Uses a contiguous block of memory.
        -   **Performance:** `get(index)` is very fast (O(1)), but `add(item)` can be slow (O(n)) if the array is full and needs resizing.
    2.  **Linked List-based List:**
        -   **How:** Uses nodes and pointers linking to the next node.
        -   **Performance:** `add(item)` at the beginning is very fast (O(1)), but `get(index)` is slow (O(n)) because it requires traversing from the start.

### 3. Components of an ADT

An ADT is generally defined by two parts:
1.  **Data:** A description of the type of values it stores.
2.  **Operations:** A list of functions or methods that can be performed on the data, specifying their expected inputs and outputs. This serves as the "public interface" of the ADT.

**Example: The Stack ADT**
-   **Data:** A collection of items.
-   **Operations:**
    -   `push(item)`: Adds an item to the top of the stack.
    -   `pop()`: Removes and returns the item from the top of the stack.
    -   `peek()`: Returns the top item without removing it.
    -   `isEmpty()`: Returns true if the stack is empty.

Notice this definition says nothing about whether we will build the Stack with an Array or a Linked List.

---

## 📋 Comprehensive Summary & Practical Exercise

### Comprehensive Summary

An ADT is a "logical blueprint" that defines a data type by its behavior (WHAT), while a Data Structure is the "concrete implementation" that describes how it's built (HOW). One ADT can be implemented by multiple Data Structures, each with different performance trade-offs.

### Practical Exercise

Consider a real-world "queue at a bank counter":
1.  As an ADT, what `Operations` should this "Queue" have? (e.g., joining the queue, the first person leaving, seeing who is at the front).
2.  What `Data Structures` do you think could be used to "implement" this queue in code?

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
