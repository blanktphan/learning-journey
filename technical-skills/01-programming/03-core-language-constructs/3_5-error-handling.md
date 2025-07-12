# 📖 Topic: Error Handling

## 💡 Basic knowledge required

An understanding of program operation and control flow structures (from lessons 3.1-3.4).

## 🎯 Learning Objectives

- Be able to distinguish between Syntax Errors and Runtime Errors (Exceptions).
- Be able to explain the purpose of Structured Exception Handling.
- Be able to apply a try-catch (or try-except) block to handle Exceptions appropriately.
- Understand the roles of `finally` and `throw` (or `raise`) in error management.

---

### 1. Introduction: Errors are Unavoidable

In the real world, many things can go wrong that are outside a programmer's direct control. For example:

- A user enters data in an incorrect format.
- The program attempts to open a file that does not exist.
- A network connection fails.
- The system runs out of memory.

A program written without a plan to handle these situations will "crash" immediately when they occur. This creates a poor user experience and can lead to data loss. Error Handling is a set of techniques and practices for creating "robust" programs that can anticipate and properly manage these unexpected scenarios.

### 2. Types of Errors

We can categorize program errors into two main types:

#### Syntax Errors

- **Description**: These are errors caused by writing code that violates the grammatical (syntax) rules of the programming language. It is like making a spelling or grammar mistake in an English sentence.
- **Detection**: They are detected by the compiler or interpreter *before* the program starts to run. The program cannot be executed at all until these errors are corrected.
- **Examples**: Forgetting a semicolon, misspelling a command, or having mismatched parentheses.

#### Runtime Errors or Exceptions

- **Description**: These errors occur *while* the program is running. Even if the code's syntax is completely correct, an unexpected situation arises that prevents the program from continuing its normal execution. This is the type of error we need to "handle".
- **Examples**: `DivisionByZeroError` (dividing by zero), `FileNotFoundError` (file not found), `NullPointerException` (attempting to use a method on a null object).

### 3. Structured Exception Handling

This is the standard approach used in modern programming languages to manage Runtime Errors. Its core principle is to "separate" the code for normal operation from the code that handles errors, making the overall code cleaner and much easier to read.

#### The try-catch Structure (or try-except in Python)

- **`try` block**: This is where we place "risky" code, or code that we anticipate "might" cause an Exception.
- **`catch` / `except` block**: This block of code executes *only if* an Exception occurs within the `try` block. It serves to "catch" the error and allows us to handle it appropriately, such as by displaying a user-friendly message, logging the error, or trying an alternative operation. If no error occurs in the `try` block, this section of code is skipped entirely.

Here is an ASCII diagram illustrating the flow:

```
Start
  |
  v
+----------------------+
|      try block       |  <-- Execute risky code
|  (e.g., file access) |
+----------------------+
  |
  |
  v
/--------------------\  No  +--------------------+
| Did an error occur?|----->|  Skip catch block  |
\--------------------/      +--------------------+
  | Yes                           |
  v                               |
+----------------------+          |
|     catch block      |          |
| (Handle the error)   |          |
+----------------------+          |
  |                               |
  v                               v
End of try-catch structure, continue program
```

**Example (Python-like syntax):**

```python
try:
    # Risky code
    file = open("data.txt", "r")
    number = int(file.read())
    result = 100 / number
    print(result)
except FileNotFoundError:
    # Executes when data.txt is not found
    print("Error: The specified file was not found.")
except ValueError:
    # Executes when data in the file is not a number
    print("Error: Data in the file cannot be converted to a number.")
except ZeroDivisionError:
    # Executes when trying to divide by zero
    print("Error: Cannot divide by zero.")
```

### 4. Additional Constructs: `finally` and `throw`

#### `finally` block

This is an optional block of code that is *always* executed, regardless of whether an Exception occurred or not. It is typically used for necessary "cleanup" tasks, such as closing a file (`file.close()`) or terminating a network connection, to ensure resources are always returned to the system.

```
Start
  |
  v
+----------------------+
|      try block       |
+----------------------+
  |
  |
  v
/--------------------\
| Did an error occur?|
\--------------------/
  |            | No
  | Yes        |
  v            v
+----------------------+
|     catch block      |
+----------------------+
  |
  v
+----------------------+
|    finally block     |  <-- This ALWAYS runs
+----------------------+
  |
  v
End
```

#### `throw` or `raise`

This is a command used to "intentionally" create an Exception. It is used when a programmer detects a logical error in the program (e.g., a function receives an invalid argument) and wants to signal that error to be handled by another part of the program.

---

## 📋 Comprehensive Summary & Practical Exercise

### Comprehensive Summary

Error handling is essential for creating robust programs. We use the `try-catch` block to separate normal code from error-handling code. The `try` block is for code that might fail, and the `catch` block is for catching and managing errors when they actually happen. The `finally` block ensures cleanup code runs, and `throw` allows us to create our own exceptions.

### Practical Exercise

You are writing a function that takes two numbers as input and divides them (a / b).
1. What is the most likely Exception that could occur in this function?
2. How would you use a `try-except` block to handle this error? (e.g., what message would you show the user?)

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
