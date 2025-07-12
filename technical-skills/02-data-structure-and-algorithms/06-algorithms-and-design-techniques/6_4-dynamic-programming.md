# 📖 Topic: Dynamic Programming

## 💡 Basic knowledge required

- A deep understanding of recursion.
- Familiarity with the Divide and Conquer technique.

## 🎯 Learning Objectives

- Define Dynamic Programming as an optimization technique that solves subproblems and remembers their solutions.
- Explain the two properties of problems suitable for DP: Overlapping Subproblems and Optimal Substructure.
- Differentiate and compare the two DP approaches: Memoization (Top-Down) and Tabulation (Bottom-Up).

---

### 1. Introduction: Intelligent Recursion

In the last lesson, we learned that Divide and Conquer works by breaking a problem into **independent** subproblems. But what happens if those subproblems are not independent and instead **overlap**? This means our recursive algorithm ends up re-calculating the same subproblems over and over, often leading to an exponential time complexity like O(2^n).

**Dynamic Programming (DP)** is an algorithmic technique designed specifically to solve this issue. It works by solving each subproblem **only once** and then **"remembering"** or "caching" that solution. If the solution to that same subproblem is needed again later, it can be retrieved from the cache instantly without re-computation.

**Analogy:** Imagine you're filling out a tax form. You might need the "income after expenses" figure in multiple places. Instead of recalculating it every time, you'd calculate it once, jot it down on a notepad, and then just look at the notepad for subsequent uses. That "notepad" is the essence of Dynamic Programming.

### 2. The Two Properties of DP Problems

A problem can typically be solved with Dynamic Programming if it exhibits two key properties:

#### Overlapping Subproblems
-   **Concept:** A recursive algorithm ends up solving the same subproblems multiple times.
-   **Classic Example:** The Fibonacci Sequence, where `fib(n) = fib(n-1) + fib(n-2)`.
    -   To find `fib(5)`, we need `fib(4)` and `fib(3)`.
    -   To find `fib(4)`, we need `fib(3)` and `fib(2)`.
    -   As you can see, `fib(3)` is calculated redundantly. DP solves this by storing the result of `fib(3)` the first time it's computed.
```
          fib(5)
         /      \
      fib(4)     fib(3)
     /    \       /    \
  fib(3) fib(2) fib(2) fib(1)
 (fib(3) is computed twice)
```

#### Optimal Substructure
-   **Concept:** The optimal solution to the overall problem can be constructed from the optimal solutions of its subproblems.
-   **Example:** The shortest path from City A to City C that passes through City B is equal to (the shortest path from A to B) + (the shortest path from B to C).

### 3. The Two Approaches to DP

#### A. Memoization (Top-Down with Caching)
-   **Approach:** This is a direct enhancement of a standard recursive algorithm.
-   **Steps:**
    1.  Write the recursive function as you normally would.
    2.  Create a "cache" (often an array or hash map) to store results.
    3.  Before any computation, check if the solution for the current subproblem is already in the cache.
    4.  If yes -> return the cached value.
    5.  If no -> perform the computation as usual, but **before returning**, save the result in the cache.
-   **Nature:** This is a "lazy" approach. It doesn't compute anything until it's asked to, but it's smart enough to remember the answer for the next time.

#### B. Tabulation (Bottom-Up)
-   **Approach:** This is an iterative approach that avoids recursion entirely.
-   **Steps:**
    1.  Create a "table" (usually an array) to store the results of subproblems.
    2.  "Fill" the table by starting with the smallest possible subproblems (the base cases).
    3.  Iteratively calculate the results for larger problems by referencing the already-computed results of smaller problems stored in the table.
    4.  Continue until the table is filled up to the solution you need.
-   **Nature:** This is a "diligent" approach. It computes the solution for every subproblem, starting from the bottom and working its way up, without waiting to be asked.

---

## 📋 Comprehensive Summary & Practical Exercise

### Comprehensive Summary

Dynamic Programming is an optimization technique for problems with Overlapping Subproblems and Optimal Substructure. It works by "remembering" subproblem results to avoid re-computation. **Memoization** is a top-down, recursive approach, while **Tabulation** is a bottom-up, iterative approach. DP can transform problems with exponential complexity (O(2^n)) into ones with polynomial complexity (O(n²) or O(n)).

### Practical Exercise

You are climbing a staircase and can take either 1 or 2 steps at a time. The problem is to find how many distinct ways there are to climb to the n-th step. (e.g., for 3 steps, there are 3 ways: 1-1-1, 1-2, 2-1).
1.  Does this problem exhibit "Overlapping Subproblems"? (Hint: To get to step `n`, which steps must you have come from?)
2.  Which DP approach (Memoization or Tabulation) would you use to solve this, and why?

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
