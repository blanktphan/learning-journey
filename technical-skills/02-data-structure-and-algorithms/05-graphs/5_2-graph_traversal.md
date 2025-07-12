# 📖 Topic: Graph Traversal Algorithms

## 💡 Basic knowledge required

- Understanding of what a graph is and its representations (Adjacency List/Matrix).
- Familiarity with Stacks and Queues.

## 🎯 Learning Objectives

- Understand the goal of graph traversal: to visit every vertex in a systematic way.
- Explain the algorithm for Breadth-First Search (BFS) and its level-by-level exploration.
- Explain the algorithm for Depth-First Search (DFS) and its "go deep" exploration strategy.
- Identify the data structures that power each traversal (Queue for BFS, Stack for DFS).
- Recognize common use cases for both BFS and DFS.

---

### 1. Introduction: How to Explore a Network

Graph traversal (or graph search) is the process of visiting (checking and/or updating) each vertex in a graph. Unlike linear data structures or trees, graphs can have cycles, so we need a systematic way to visit each vertex exactly once and avoid getting stuck in an infinite loop. The two primary algorithms for this are Breadth-First Search (BFS) and Depth-First Search (DFS).

### 2. Breadth-First Search (BFS): The Level-by-Level Explorer

BFS explores the graph "layer by layer." It starts at a source vertex, explores all of its immediate neighbors, then explores all of their neighbors, and so on.

-   **Core Idea:** Explore vertices in increasing order of their distance from the source.
-   **Data Structure:** A **Queue** (First-In, First-Out).

**Algorithm:**
1.  Pick a starting vertex and add it to a queue. Mark it as visited.
2.  While the queue is not empty:
    a. Dequeue a vertex, let's call it `u`.
    b. For each of `u`'s unvisited neighbors:
        i. Mark the neighbor as visited.
        ii. Enqueue the neighbor.

```
BFS explores like ripples in a pond:
       (A)
      / | \
     /  |  \
   (B) (C) (D)  <- Level 1
   / \   |
 (E) (F) (G)    <- Level 2
```

-   **Use Cases:** Finding the shortest path in an unweighted graph, social network analysis (e.g., finding all friends of friends), web crawlers.

### 3. Depth-First Search (DFS): The Deep Dive Explorer

DFS explores as far as possible along each branch before backtracking. It goes deep down one path until it hits a dead end, then backtracks to the last junction and tries a different path.

-   **Core Idea:** Go as deep as you can, then backtrack.
-   **Data Structure:** A **Stack** (Last-In, First-Out). This is often implemented implicitly using recursion (the "call stack").

**Algorithm (Recursive):**
1.  Pick a starting vertex `u`.
2.  Mark `u` as visited.
3.  For each of `u`'s unvisited neighbors `v`:
    a. Recursively call DFS on `v`.

```
DFS explores like navigating a maze:
       (A) -> (B) -> (E) -> backtrack
        |
       (C) -> (G) -> backtrack
        |
       (D)
```

-   **Use Cases:** Detecting cycles in a graph, topological sorting (for scheduling tasks with dependencies), solving puzzles like mazes.

### 4. BFS vs. DFS Comparison

| Feature        | Breadth-First Search (BFS) | Depth-First Search (DFS)      |
|----------------|----------------------------|-------------------------------|
| **Data Structure** | Queue                      | Stack (or recursion)          |
| **Exploration**  | Wide, level by level       | Deep, path by path            |
| **Shortest Path**| Finds it in unweighted graphs | Not guaranteed to find it     |
| **Memory Usage** | Can be high if graph is wide | Can be high if path is long   |

---

## 📋 Comprehensive Summary & Practical Exercise

### Comprehensive Summary

Graph traversal is about visiting all vertices systematically. **BFS** uses a queue to explore level by level and is ideal for finding the shortest path in an unweighted graph. **DFS** uses a stack (often via recursion) to explore as deeply as possible along each branch and is excellent for tasks like cycle detection or pathfinding in a maze.

### Practical Exercise

Consider the following graph:
A is connected to B and C.
B is connected to D.
C is connected to E.
D and E are not connected to anything else.

Starting from vertex A, list the order in which the vertices would be visited for:
1.  A Breadth-First Search (BFS).
2.  A Depth-First Search (DFS).

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
