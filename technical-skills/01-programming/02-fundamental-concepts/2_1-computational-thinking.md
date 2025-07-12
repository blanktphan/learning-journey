# 📖 Topic: Computational Thinking

## 💡 Basic knowledge required

A general interest in problem-solving. No prior programming experience is necessary.

## 🎯 Learning Objectives

- Define and explain the meaning of Computational Thinking.
- Identify and explain the four pillars of CT (Decomposition, Pattern Recognition, Abstraction, Algorithm Design).
- Apply the CT framework to analyze technical problems.

---

### Introduction to Chapter 2

In Chapter 1, we built a high-level understanding of "what a program is" and "how computers work with them." In this second chapter, we will step back from the specifics of languages and hardware to delve into the "thought process"—the critical core that happens before a single line of code is written. This chapter is about creating the "mental blueprint," or algorithm, for solving problems systematically.

---

### 1. Definition and Core Concepts

Computational Thinking (CT) is a problem-solving process that involves formulating problems and their solutions in a way that a computer can effectively execute. It is not about "thinking like a computer," but rather a set of mental tools that allows humans to leverage the power of computing to solve complex problems.

This approach is built on four key pillars that work in conjunction:

- **Decomposition**: The process of breaking down a complex problem or system into smaller, more manageable sub-problems.
- **Pattern Recognition**: The process of finding similarities, trends, or recurring patterns among and within the sub-problems.
- **Abstraction**: The process of filtering out and ignoring irrelevant details to focus only on the essential information required to solve the problem.
- **Algorithm Design**: The process of developing a step-by-step, unambiguous set of instructions to solve the problem.

### 2. Application in Problem-Solving

Consider the task: "Analyze a sales data file to find the top 10 customers by total profit."

We can apply the four pillars of CT to structure our approach:

#### Decomposition
First, we break the problem down into smaller steps:
1.  Read the data from the file.
2.  Calculate the profit for each transaction.
3.  Sum the total profit for each individual customer.
4.  Sort the customers based on their total profit.
5.  Select the top 10 customers.
6.  Display the result.

#### Pattern Recognition
Next, we look for patterns:
- We observe that each row in the data file follows a consistent pattern (e.g., `date, customer_id, sale_price, cost_price`).
- We recognize that the process of "aggregation" (summing totals) is a common pattern in data analysis.

#### Abstraction
Then, we abstract away unnecessary details:
- We ignore data that is not relevant to our goal, such as the specific time of the transaction.
- We create a conceptual model for the data we need. A dictionary is a suitable abstraction, where the `key` is the `customer_id` and the `value` is their `cumulative_profit`.

#### Algorithm Design
Finally, we design a step-by-step algorithm based on the previous stages:

```
1. Create an empty dictionary named 'profits_by_customer'.
2. Open the sales data file.
3. FOR each row in the file:
4.     Calculate profit = sale_price - cost_price.
5.     IF the customer_id already exists in 'profits_by_customer':
6.         Add the profit to the existing value.
7.     ELSE:
8.         Create a new entry for the customer_id with the current profit.
9. Convert the dictionary into a list.
10. Sort the list by profit in descending order.
11. Select the first 10 items from the list.
12. Print the result.
```

This entire thought process is Computational Thinking. The final output is a clear algorithm ready to be implemented as a program.

---

## 📋 Comprehensive Summary & Practical Exercise

### Comprehensive Summary

Computational Thinking is a systematic process for creating a "plan" to solve a problem. It consists of four steps: decomposing the problem, finding patterns, filtering out non-essential information, and creating a sequence of steps (an algorithm).

### Practical Exercise

Try applying the four principles of CT to your daily routine: "Getting ready for work or school in the morning."
- **Decompose** the entire activity.
- **Find** the 'patterns' you repeat.
- **Filter out** what isn't necessary.
- **Write down** a clear 'sequence of steps'.

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
