# 📖 Topic: Testing and Debugging

## 💡 Basic knowledge required

- A program or code segment that has been written (from lesson 4.3).
- An understanding of the program's logic and potential sources of error.

## 🎯 Learning Objectives

- Define "Software Testing" and explain its goal of verifying and validating correctness.
- Differentiate between key levels of testing: Unit Testing, Integration Testing, and System Testing.
- Define "Debugging" as the process of finding and resolving defects.
- Identify common debugging techniques, such as using print statements and an Interactive Debugger.

---

### 1. Introduction: The Pursuit of Correctness

Writing code that runs is only half the battle. Just because a program executes without crashing does not mean it produces the correct results in all situations. **Testing** and **Debugging** are two distinct but closely related activities used to ensure software quality.

-   **Testing**: The process of **finding** if and where errors (Bugs) exist. The goal of testing is to try to make the program fail or behave incorrectly.
-   **Debugging**: The process of **finding the cause of and fixing** the errors that testing has discovered.

### 2. Software Testing: A Systematic Approach

Software Testing is a systematic process of evaluating software quality to provide information to stakeholders. Testing is typically divided into different levels based on scope, often represented as a "Testing Pyramid."

```
      / \
     /   \
    /-----\   <-- System Testing
   /       \
  /---------\  <-- Integration Testing
 /           \
/-------------\ <-- Unit Testing
```

#### A. Unit Testing

-   **Scope**: Testing the "smallest testable unit" of software, which is typically a single "function" or "method," tested in isolation.
-   **Goal**: To verify that each unit of code works correctly as designed.
-   **Example**: For an `is_even(number)` function, we would write unit tests for cases like `is_even(4)` (should return true), `is_even(5)` (should return false), and `is_even(0)` (an edge case).

#### B. Integration Testing

-   **Scope**: Testing the interaction "between" multiple units or modules.
-   **Goal**: To find errors that occur at the "interfaces" or points of interaction between components.
-   **Example**: Testing whether a `checkout()` function correctly calls `processPayment()` and `updateInventory()`, and that data is passed between them without issues.

#### C. System Testing

-   **Scope**: Testing the fully assembled software system as a whole.
-   **Goal**: To verify that the overall system meets its functional and non-functional requirements from an end-user's perspective.
-   **Example**: Simulating a real user's end-to-end workflow, such as: Login -> Search for a product -> Add to cart -> Checkout.

### 3. Debugging: The Art of Diagnosis

Debugging is the investigative process of identifying the location of a problem, isolating the root cause, and fixing the error.

#### Common Techniques:

-   **Print Debugging**: The simplest technique, involving inserting `print()` statements at various points in the code to display variable values and trace the execution flow. This method is quick but can clutter the code and must be removed later.

-   **Interactive Debugger**: A powerful tool available in most IDEs. It allows us to:
    -   **Set Breakpoints**: Command the program to "pause" at a specific line.
    -   **Step Through Code**: Execute the program one line at a time.
    -   **Inspect Variables**: View the value of any variable while the program is paused.
    -   **Analyze the Call Stack**: See the sequence of function calls that led to the current point.

Using a debugger is a much more systematic and efficient method than using print statements.

---

## 📋 Comprehensive Summary & Practical Exercise

### Comprehensive Summary

Testing and Debugging are complementary processes for building quality software. Testing is about "finding" bugs and occurs at different levels (Unit, Integration, System). Debugging is about "finding the cause and fixing" those bugs.

### Practical Exercise

Assume your `calculate_average(numbers)` function is faulty. When you input the list `[10, 20, 30]`, it should return 20, but it returns 15 instead.
1.  How would you use Print Debugging to find the source of this problem? (What values would you print, and at what points in the function?)
2.  If using an Interactive Debugger, where would you set a breakpoint to start your investigation?

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
