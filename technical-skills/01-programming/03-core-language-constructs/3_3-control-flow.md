# 📖 Topic: Control Flow

## 💡 Basic knowledge required

An understanding of variables, and especially comparison and logical operators that produce Boolean (`true`/`false`) results (from Lessons 3.1-3.2).

## 🎯 Learning Objectives

- Define "Control Flow" and explain its importance in creating programs that execute non-linearly.
- Understand and write conditional statements using `if`, `else if`, and `else` to create decision-making branches.
- Understand and write loop statements using `while` and `for` to execute code repeatedly.
- Distinguish the appropriate use cases for a `while` loop versus a `for` loop.

---

### 1. Introduction to Control Flow

By default, a computer processes a program sequentially—it executes commands one by one, from the top line down to the bottom. Control Flow refers to the set of statements that allow us to change this execution order. It enables our programs to "make decisions" to skip certain instructions or "loop back" to repeat a set of instructions, which is what makes programs intelligent and responsive to different situations.

```
  Sequential Flow
+-----------------+
|  Instruction A  |
+-----------------+
         |
         v
+-----------------+
|  Instruction B  |
+-----------------+

  Control Flow (Decision)
+-----------------+
|   Condition?    |
+-----------------+
   |           |
 True        False
   |           |
   v           v
[Do A]       [Do B]
```

### 2. Conditional Statements: The Power of Decision Making

This structure creates "branches" or "choices" in your program. It executes different blocks of code depending on whether a condition evaluates to `true` or `false`.

- `if`: Executes the code block
### 2. Conditional Statements: The Power of Decision Making

This structure creates "branches" or "choices" in your program. It executes different blocks of code depending on whether a condition evaluates to `true` or `false`.

- **`if`**: Executes the code block inside it only if the condition is `true`.
  ```java
  if (isRaining == true) {
      // Bring an umbrella
  }
  ```
- **`if-else`**: Provides a clear two-way path.
  ```java
  if (isRaining == true) {
      // Bring an umbrella
  } else {
      // Wear sunglasses
  }
  ```
- **`if-else if-else`**: Used for creating complex decision branches with more than two possibilities. Conditions are checked in order.
  ```java
  int score = 85;
  char grade;

  if (score >= 90) {
      grade = 'A';
  } else if (score >= 80) {
      grade = 'B'; // The program enters this block and skips the rest.
  } else if (score >= 70) {
      grade = 'C';
  } else {
      grade = 'F';
  }
  ```

### 3. Loop Statements: The Art of Repetition

This structure allows a block of code to be executed repeatedly, which is essential for automation and processing collections of data.

#### `while` loop (Condition-Based Repetition)
- **Structure**: Executes a block of code as long as a specified condition remains `true`. The condition is checked **before** each new iteration.
- **Use Case**: Ideal when you **do not know the exact number of iterations** but you know the **condition that should stop the loop**.
- **Example**: The program keeps asking for a password until the user enters the correct one.

#### `for` loop (Count-Based or Collection-Based Repetition)
- **Structure**: Designed to iterate a specific number of times or to iterate over every element in a data collection (like a list).
- **Use Case**: Ideal when you **know the number of repetitions** in advance or need to process every item in a collection.
- **Example**: The program prints every fruit name from a list.
  ```python
  fruits = ["Apple", "Banana", "Cherry"]
  for fruit in fruits:
      print(fruit)
  ```

---

## 📋 Comprehensive Summary & Practical Exercise

### Comprehensive Summary

Control Flow allows programs to execute in a non-linear fashion. Conditional Statements (`if-else`) are used to make decisions, while Loops (`while`, `for`) are used for repetition. A `while` loop is suitable for condition-based iteration, and a `for` loop is suitable for a fixed number of iterations or iterating over a collection.

### Practical Exercise

You are programming the logic for an ATM.

1.  To verify if a user enters the correct **PIN**, what type of Control Flow would you use? (`if-else` or a loop?)
2.  For the ATM to **continuously accept user commands until the user selects the 'Quit' menu**, which type of loop should be used (`for` or `while`), and why?

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.