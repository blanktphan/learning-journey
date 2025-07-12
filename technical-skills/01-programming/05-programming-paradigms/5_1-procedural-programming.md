# 📖 Topic: Procedural Programming

## 💡 Basic knowledge required

- An understanding of core language constructs, especially Functions and Variables (from Section 3).

## 🎯 Learning Objectives

- Define "Procedural Programming" and explain the core concept of a sequence of commands.
- Identify that "procedures" (or functions) are the main mechanism for structuring code.
- Understand the concept of "Shared State" and how data is passed between procedures.
- Analyze the pros (simplicity) and cons (managing complexity) of this paradigm.

---

### Introduction to Section 5: Programming Paradigms

In previous sections, we learned the "thinking processes" and "tools" for creating programs. In this section, we will explore "Paradigms," which are not languages or tools, but rather "styles," "philosophies," or "conceptual frameworks" for structuring entire programs.

The choice of a paradigm directly influences how we design, organize, and reason about our code. Each paradigm is suited to different types of problems.

---

### 1. Definition and Core Concept

Procedural Programming is a paradigm based on the concept of the "procedure call." Procedures, also known as functions or subroutines, are simply a series of computational steps to be carried out. A program in this paradigm is a "sequence of computational steps" executed from top to bottom.

**Analogy**: A procedural program is like a **recipe** with clear steps: 1, 2, 3... We read and follow each step in order. There might be "sub-steps" (procedures) that we need to perform, such as an "ingredient preparation" step, which we can call upon whenever needed.

**Focus**: This paradigm focuses on **actions** (verbs). The program is a list of "things to do."

### 2. Key Characteristics

-   **Top-Down Approach**: Design typically starts with the main task, which is then decomposed into smaller and smaller procedures.
-   **Shared State**: Data is often stored in global variables that multiple procedures can read from and write to. Alternatively, data is passed between procedures as arguments. The data and the procedures that operate on it are distinctly separate.
-   **Sequential Execution**: The program follows a sequential flow of execution, with procedure calls altering the flow as needed.

### 3. Example of Operation

Consider a simple program simulating bank deposits and withdrawals:

```
// A global variable used to store the shared state
account_balance = 1000.00

// Procedure for withdrawing money
PROCEDURE withdraw(amount)
    IF account_balance >= amount THEN
        account_balance = account_balance - amount
        print("Withdrawal successful. New balance:", account_balance)
    ELSE
        print("Insufficient funds.")
    END IF
END PROCEDURE

// Procedure for depositing money
PROCEDURE deposit(amount)
    account_balance = account_balance + amount
    print("Deposit successful. New balance:", account_balance)
END PROCEDURE

// The main sequence of the program
print("Initial balance:", account_balance)
withdraw(200.00)   // Call the withdraw procedure
deposit(50.00)     // Call the deposit procedure
print("Final balance:", account_balance)
```

As you can see, `account_balance` is an independent piece of data, and both procedures modify this shared data.

### 4. Advantages and Disadvantages

#### Advantages:

-   **Simplicity**: Easy to understand and straightforward, making it suitable for small programs or simple scripts.
-   **Efficiency**: For linear computational tasks, it often has low overhead and can execute quickly.

#### Disadvantages (The reason other paradigms were created):

-   **Difficult to Manage Complexity**: As a program grows, having many procedures accessing and modifying shared global data can create a complex web of dependencies, often called "Spaghetti Code." This makes it very difficult to track and debug.
-   **Poor Data Encapsulation**: Because data and the functions that operate on it are separate, it is easy for one procedure to unintentionally modify data, leading to hard-to-find bugs. This is the primary problem that **Object-Oriented Programming (OOP)** was created to solve.

---

## 📋 Comprehensive Summary & Practical Exercise

### Comprehensive Summary

Procedural Programming structures a program as a sequence of procedures (functions) that operate on shared data. It is simple but becomes difficult to manage as program complexity increases.

### Practical Exercise

Is a cooking recipe you use in daily life an example of a procedural algorithm? Why or why not? Try to identify potential "sub-procedures" within that recipe (e.g., 'ingredient preparation step,' 'dough mixing step').

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
