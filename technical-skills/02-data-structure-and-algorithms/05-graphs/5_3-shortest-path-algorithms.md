# 📖 Topic: Shortest Path Algorithms: Dijkstra's

## 💡 Basic knowledge required

- Understanding of weighted graphs.
- Familiarity with BFS and the Priority Queue data structure.

## 🎯 Learning Objectives

- Define the "shortest path problem" in graph theory.
- Explain the algorithm and logic behind Dijkstra's algorithm.
- Understand the critical role of a Priority Queue in optimizing Dijkstra's algorithm.
- Explain the key limitation of Dijkstra's algorithm regarding negative weights.

---

### 1. Introduction: Finding the Most Efficient Route

From the previous lesson, we know that Breadth-First Search (BFS) can find the shortest path in terms of the "fewest number of edges." However, in the real world, different paths often have different "costs," such as distance, time, or tolls.

The **Shortest Path Problem** is the challenge of finding a path between two vertices in a weighted graph such that the **sum of the weights** of all edges in that path is minimized.

### 2. Dijkstra's Algorithm

Dijkstra's algorithm is a classic and fundamental algorithm for solving the **single-source shortest path problem** on a graph where all **edge weights are non-negative**.

**Core Idea:** It is a **Greedy Algorithm**. At each step, it makes the choice that looks best at the moment. It always chooses to visit the "unvisited vertex that is currently closest to the start."

**Required Data Structures:**
-   `distances`: An array or hash table to store the "shortest distance found so far" from the source to every other vertex. (Initialize to ∞ for all, except 0 for the source).
-   `visited`: A set to keep track of vertices for which the absolute shortest path has been found and finalized.
-   `Priority Queue` (implemented with a Min-Heap): This is the key to the algorithm's efficiency. It stores unvisited vertices, ordered by their current `distance`, allowing us to retrieve the "closest" vertex in O(log V) time.

**The Algorithm:**
1.  Initialize `distances` for all vertices to ∞, and the `source` vertex's distance to 0.
2.  Add the `source` vertex to the Priority Queue.
3.  While the Priority Queue is not empty:
    a. Extract the vertex `u` with the smallest distance from the Priority Queue.
    b. If `u` has already been visited, skip it.
    c. Mark `u` as visited (its shortest path is now considered final).
    d. For each neighbor `v` of `u`:
        i.  Calculate the new potential distance: `new_dist = distance[u] + weight(u, v)`.
        ii. If `new_dist` is less than the currently known `distance[v]`:
            -   Update `distance[v]` to `new_dist`.
            -   Add `v` to the Priority Queue with its new, smaller distance.

### 3. Limitation: The Problem with Negative Weights

Dijkstra's algorithm is built on the greedy assumption that "once we finalize the shortest distance to a node, we never need to reconsider it."

This assumption **breaks** if the graph has a negative weight edge. A negative edge could create a "shortcut" that reduces the path distance to a node that has already been finalized, leading the algorithm to produce an incorrect result.

**Solution:** For graphs that may contain negative weights, a more complex algorithm like the Bellman-Ford algorithm must be used.

---

## 📋 Comprehensive Summary & Practical Exercise

### Comprehensive Summary

Dijkstra's algorithm is a greedy approach to solving the single-source shortest path problem in graphs with no negative edge weights. It uses a Priority Queue to efficiently select the next closest vertex to process, resulting in a time complexity of O(E + V log V).

### Practical Exercise

A map application (like Google Maps) calculates the "fastest" driving route based on the "time" it takes to travel along each road segment.
1.  What does the "time" on each road represent in graph theory?
2.  What is the likely base algorithm the app uses?
3.  Why is this algorithm suitable? (e.g., can the edge weights be negative?)

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
