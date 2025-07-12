# 📖 Topic: Introduction to Graphs

## 💡 Basic knowledge required

- Understanding of nodes and pointers/references.
- Familiarity with concepts like Arrays and Linked Lists for implementation.

## 🎯 Learning Objectives

- Define a "Graph" as a data structure representing a set of connections.
- Identify and define key graph terminology (Vertex, Edge, Directed, Undirected, Weighted).
- Differentiate between a graph and a tree.
- Describe the two most common ways to represent a graph in code: Adjacency Matrix and Adjacency List.

---

### 1. Introduction: The Ultimate Network Structure

So far, we have studied linear structures (like lists) and hierarchical structures (like trees). A **Graph** is the most general and powerful non-linear data structure, designed to model complex **many-to-many relationships**.

Almost any real-world scenario involving a network of connections can be represented by a graph:
-   Social networks (people and their friendships).
-   Road maps (cities and the roads connecting them).
-   The internet (web pages and the links between them).

### 2. Anatomy of a Graph

A graph `G` is defined by a set of Vertices (V) and a set of Edges (E).
-   **Vertex (or Node):** The fundamental unit of a graph. It represents an entity or an object.
-   **Edge (or Link):** The connection between two vertices.

```
      (A)-------(B)
       |         |
       |         |
      (C)-------(D)
```

### 3. Types of Graphs

-   **Undirected vs. Directed Graph:**
    -   **Undirected:** Edges have no direction. If A is connected to B, then B is connected to A. (e.g., a Facebook friendship).
    -   **Directed (Digraph):** Edges have a direction. A connection from A to B does not imply a connection from B to A. (e.g., following someone on Twitter).

-   **Unweighted vs. Weighted Graph:**
    -   **Unweighted:** Edges simply represent a connection.
    -   **Weighted:** Each edge has an associated numerical "weight" or "cost." (e.g., in a map, the weight could be the distance between two cities).

-   **Cyclic vs. Acyclic Graph:**
    -   **Cyclic:** Contains at least one path that starts and ends at the same vertex.
    -   **Acyclic:** Contains no cycles. A **Directed Acyclic Graph (DAG)** is a very important type of graph in computer science.

**Graph vs. Tree:** A tree is a more restricted type of graph. Specifically, a tree is an undirected, connected graph with no cycles.

### 4. Graph Representation

How do we store a graph in a computer's memory? There are two primary methods:

#### Adjacency Matrix
-   **How it works:** A 2D array (matrix) of size V x V, where `V` is the number of vertices. The entry `matrix[i][j]` is 1 (or the edge weight) if there is an edge from vertex `i` to vertex `j`, and 0 otherwise.
-   **Pros:** Fast to check if an edge exists between two given vertices (O(1)).
-   **Cons:** Uses a lot of memory (O(V²)), even if the graph has very few edges (a "sparse" graph).

#### Adjacency List
-   **How it works:** An array where each slot `i` corresponds to a vertex. Each slot contains a linked list of all the vertices that vertex `i` is connected to.
-   **Pros:** Memory efficient for sparse graphs (O(V + E), where E is the number of edges).
-   **Cons:** Slower to check if an edge exists between two vertices (O(k), where k is the number of neighbors).

---

## 📋 Comprehensive Summary & Practical Exercise

### Comprehensive Summary

A graph is a data structure that models many-to-many relationships using vertices (nodes) and edges (connections). Graphs can be directed or undirected, weighted or unweighted. They are typically represented in code using either an Adjacency Matrix (fast for edge lookup, high memory usage) or an Adjacency List (memory efficient, slower for edge lookup).

### Practical Exercise

Imagine you are modeling a small social network with 4 people: Alice, Bob, Charles, and Diana.
-   Alice is friends with Bob and Charles.
-   Bob is friends with Alice and Diana.
-   Charles is friends with Alice.
-   Diana is friends with Bob.

1.  Is this graph directed or undirected?
2.  Draw this graph.
3.  Represent this graph using both an Adjacency Matrix and an Adjacency List.

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
