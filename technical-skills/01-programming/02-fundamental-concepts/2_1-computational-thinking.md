# 📖 Topic: Computational Thinking

## 💡 Basic knowledge required

A general understanding of what a program is and what it does. No prior programming experience is necessary.

## 🎯 Learning Objectives

- To be able to define and explain the meaning of Computational Thinking.
- To be able to identify and explain the four pillars of CT (Decomposition, Pattern Recognition, Abstraction, Algorithm Design).
- To be able to apply the CT framework to analyze technical problems.

---

### Introduction to Chapter 2: The Thinking Process

In Chapter 1, we built an understanding of the big picture: "What are programs?" and "How do computers work with them?" In this chapter, we step back from languages and hardware to dive deep into the "thinking processes" that are crucial before writing a single line of code. This chapter is about creating the "mental blueprint," or algorithm, for systematic problem-solving.

---

### 1. Definition and Core Concepts

Computational Thinking (CT) is a problem-solving process that involves organizing and framing problems and their solutions in a way that a computer can efficiently execute. It is not about "thinking like a computer" but is a set of mental tools that help humans leverage the power of computation to solve complex problems.

This concept is built on four pillars that work together:

- **Decomposition**: The process of breaking down a complex problem into smaller, more manageable sub-problems.
- **Pattern Recognition**: The process of finding similarities, trends, or recurring patterns among the sub-problems.
- **Abstraction**: The process of filtering out unnecessary details to focus on the essential aspects of the problem.
- **Algorithm Design**: The process of developing clear, step-by-step instructions to solve the problem.

### 2. Application in Problem-Solving

Consider the problem: "Analyze a sales data file to find the top 10 customers who generated the most profit."

We can apply the four pillars of CT as follows:

#### Decomposition
- Read data from the file.
- Calculate the profit for each transaction.
- Aggregate the total profit for each customer.
- Sort customers by their total profit.
- Select the top 10 customers.
- Display the results.

#### Pattern Recognition
- Notice that each row in the data file has the same "pattern" (e.g., Date, Customer_ID, Sale_Price, Cost).
- Recognize that the "aggregation" process is a common pattern in data analysis.

#### Abstraction
- We "ignore" unnecessary information for this specific problem, such as the time of the transaction.
- We "model" the necessary data using a Dictionary structure, where the Customer ID is the key and the accumulated profit is the value.

#### Algorithm Design
From the steps above, we can create a clear algorithm:

1.  Create an empty dictionary named `profits_by_customer`.
2.  Open the sales data file.
3.  For each row in the file:
    a. Calculate `profit` = `sale_price` - `cost`.
    b. If the `customer_id` already exists in `profits_by_customer`:
        i. Add the `profit` to the existing value.
    c. Else:
        i. Add the new `customer_id` with the current `profit` as its value.
4.  Convert the dictionary into a list.
5.  Sort the list in descending order based on profit.
6.  Select the first 10 items from the list.
7.  Print the result.

This entire thought process is Computational Thinking. The final output is an algorithm ready to be implemented as a program.

---

## 📋 Comprehensive Summary & Practical Exercise

### Comprehensive Summary

Computational Thinking is a systematic process for creating a "plan" to solve a problem. It consists of four steps: decomposing the problem, finding patterns, abstracting away unnecessary details, and creating a step-by-step sequence of instructions (an algorithm).

### Practical Exercise

Try applying the four pillars of CT to one of your daily routines: "Getting ready for work or school in the morning."

-   Decompose the entire activity into smaller tasks.
-   Find the patterns you repeat every day.
-   Abstract away unnecessary actions.
-   Write down a clear, step-by-step algorithm for your morning routine.

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
