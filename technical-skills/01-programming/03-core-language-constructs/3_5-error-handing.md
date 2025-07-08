# 📖 Error Handling

## 💡 Basic knowledge required:

Understanding of program execution and control flow structures (from lessons 3.1-3.4)

## 🎯 Learning Objectives

By the end of this lesson, you will be able to:

- Distinguish between Syntax Errors and Runtime Errors (Exceptions)
- Explain the purpose of Structured Exception Handling
- Apply try-catch (or try-except) blocks to handle exceptions appropriately
- Understand the role of finally and throw (or raise) in error management

---

## 1. Introduction: Errors Are Inevitable

In the real world, many things can go wrong that are beyond the programmer's direct control, such as:

- Users entering data in incorrect formats
- Programs attempting to open files that don't exist
- Network connections failing
- System memory becoming full

Programs written without proper planning will "crash" immediately when encountering these situations, creating a poor user experience and potentially leading to data loss. Error Handling is a set of techniques and best practices for creating "robust" programs that can anticipate and appropriately handle these unexpected situations.

```
Program Behavior Comparison:

Without Error Handling:
User Input ──► Program ──► CRASH! ✗
     │             │
     │             └─ Unexpected situation
     └─ Invalid data

With Error Handling:
User Input ──► Program ──► Graceful Recovery ✓
     │             │              │
     │             │              ├─ User-friendly message
     │             │              ├─ Log the error
     │             │              └─ Continue execution
     └─ Invalid data
```

## 2. Types of Errors

We can categorize programming errors into two main types:

```
Error Classification Timeline:

Before Program Runs          During Program Execution
       │                            │
       ▼                            ▼
┌─────────────────┐          ┌──────────────────┐
│  Syntax Errors  │          │ Runtime Errors   │
│                 │          │   (Exceptions)   │
│ • Missing ;     │          │ • Division by 0  │
│ • Wrong spelling│          │ • File not found │
│ • Incomplete () │          │ • Null pointer   │
│                 │          │ • Network fail   │
│ PREVENTS START  │          │ CRASHES RUNNING  │
└─────────────────┘          └──────────────────┘
```

### Syntax Errors

Description: Errors that occur due to incorrect syntax or grammar rules of the programming language. Like spelling mistakes or grammatical errors in English sentences.

Detection: Detected by the compiler or interpreter before the program starts running. The program cannot execute until these errors are fixed.

Examples: Missing semicolons, incorrect command names, incomplete brackets

```
Syntax Error Example:

Source Code:        Compiler Check:        Result:
┌─────────────┐    ┌──────────────┐      ┌─────────────┐
│ int x = 5   │───►│ Missing ';'  │─────►│ COMPILE     │
│ print(x)    │    │ at line 1    │      │ ERROR       │
└─────────────┘    └──────────────┘      │ Won't run!  │
                                         └─────────────┘
```

### Runtime Errors (Exceptions)

Description: Errors that occur while the program is running, even though the code syntax is completely correct. These are unexpected situations that cause the program to be unable to continue normal execution. This is the type of error we need to "handle."

Examples: DivisionByZeroError (division by zero), FileNotFoundError (file not found), NullPointerException (attempting to call a method from a null object)

```
Runtime Error Example:

Program Flow:
┌─────────┐    ┌─────────────┐    ┌─────────────┐
│ Start   │───►│ result = 10 │───►│ EXCEPTION!  │
│ Program │    │ divided by  │    │ Program     │
│         │    │ user_input  │    │ CRASHES     │
└─────────┘    └─────────────┘    └─────────────┘
                       │
                       ▼
                user_input = 0
```

## 3. Structured Exception Handling

This is the standard approach used in modern programming languages to handle Runtime Errors. The core principle is to "separate" normal working code from error handling code, making the overall code much cleaner and more readable.

```
Exception Handling Structure:

Normal Code Flow:        With Exception Handling:
┌─────────────┐         ┌─────────────────────────────┐
│ Statement 1 │         │        try block            │
│ Statement 2 │         │  ┌─────────────────────┐    │
│ Statement 3 │ ──────► │  │ Risky Statement 1   │    │
│ Statement 4 │         │  │ Risky Statement 2   │    │
│ Statement 5 │         │  │ Risky Statement 3   │    │
└─────────────┘         │  └─────────────────────┘    │
     │                  │           │                 │
     ▼                  │           ▼                 │
   CRASH!               │    except/catch blocks      │
                        │  ┌─────────────────────┐    │
                        │  │ Handle Error Type 1 │    │
                        │  │ Handle Error Type 2 │    │
                        │  │ Handle Error Type 3 │    │
                        │  └─────────────────────┘    │
                        └─────────────────────────────┘
                                    │
                                    ▼
                              Continue Program
```

### try-catch Structure (or try-except in Python)

try block: Contains the "risky" code or code that we expect "might" cause an exception.

catch/except block: This code block only executes when an exception occurs in the try block. It "catches" the error and allows us to handle it appropriately, such as displaying user-friendly messages, logging errors, or trying alternative approaches. If no error occurs in the try block, this section is completely skipped.

```
try-catch Flow Diagram:

┌─────────────────────────────────────────────────────────┐
│                    try block                            │
│  ┌─────────────────────────────────────────────────┐    │
│  │ file = open("data.txt", "r")                    │    │
│  │ number = int(file.read())                       │    │
│  │ result = 100 / number                           │    │
│  │ print(result)                                   │    │
│  └─────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────┘
                            │
                 ┌──────────┼──────────┐
                 │          │          │
                 ▼          ▼          ▼
         ┌─────────────┐ ┌─────────┐  ┌─────────────┐
         │FileNotFound │ │ValueError│ │ZeroDivision │
         │Exception    │ │Exception │ │Exception    │
         │             │ │         │  │             │
         │Print:       │ │Print:   │  │Print:       │
         │"File not    │ │"Invalid │  │"Cannot      │
         │ found"      │ │ data"   │  │ divide by 0"│
         └─────────────┘ └─────────┘  └─────────────┘
```

Example (Python-like syntax):

```python
try:
    # Risky code
    file = open("data.txt", "r")
    number = int(file.read())
    result = 100 / number
    print(result)
except FileNotFoundError:
    # Executes when data.txt file is not found
    print("Error: The specified file was not found")
except ValueError:
    # Executes when file data is not a number
    print("Error: File data cannot be converted to a number")
except ZeroDivisionError:
    # Executes when attempting to divide by zero
    print("Error: Cannot divide by zero")
```

## 4. Additional Structures: finally and throw

finally block: An optional code block that will always execute, regardless of whether an exception occurs or not. Commonly used for "cleanup" operations such as closing files (file.close()) or closing network connections to return resources to the system.

throw or raise: Commands used to "intentionally" create exceptions. Used when programmers detect logical errors in the program (such as functions receiving incorrect arguments) and want to signal that error to other parts of the program for handling.

```
Complete Exception Handling Structure:

┌─────────────────────────────────────────────────────────┐
│                    try block                            │
│               (risky operations)                        │
└─────────────────────┬───────────────────────────────────┘
                      │
      ┌───────────────┼───────────────┐
      │ Exception?    │ No Exception  │
      ▼               ▼               ▼
┌─────────────┐ ┌─────────────┐ ┌─────────────┐
│except Block1│ │except Block2│ │ (skip all   │
│(Error Type1)│ │(Error Type2)│ │ except      │
└─────────────┘ └─────────────┘ │ blocks)     │
      │               │         └─────────────┘
      └───────────────┼───────────────┘
                      ▼
              ┌─────────────────┐
              │  finally block  │
              │ (ALWAYS RUNS)   │
              │ • Close files   │
              │ • Clean memory  │
              │ • Release locks │
              └─────────────────┘
                      │
                      ▼
              Continue Program

throw/raise Command:
┌─────────────────────────────────────────┐
│ def validate_age(age):                  │
│     if age < 0:                         │
│         raise ValueError("Negative age")│
│     return age                          │
└─────────────────────────────────────────┘
              │
              ▼ (when age < 0)
┌─────────────────────────────────────────┐
│ Exception thrown to calling code        │
│ Must be caught by try-except block      │
└─────────────────────────────────────────┘
```

---

## 📋 Summary & Practical Exercise

### Comprehensive Summary

Error handling is essential for creating robust programs. We use try-catch blocks to separate normal code from error handling code. The try block contains risky code, while catch blocks handle specific exceptions when they occur.

Key concepts:
- Syntax Errors: Detected before execution, prevent program from running
- Runtime Errors (Exceptions): Occur during execution, can be handled
- try block: Contains potentially problematic code
- catch/except block: Handles specific exceptions
- finally block: Always executes, used for cleanup
- throw/raise: Intentionally creates exceptions

Error handling prevents program crashes, provides better user experience, enables graceful error recovery, and improves program reliability.

### Practical Exercise

Thinking Challenge: You are writing a function that takes two numbers as input and divides them (a / b).

1. Most Likely Exception: What exception is most likely to occur in this function?
2. Error Handling: How would you use a try-except block to handle this error? What message would you display to the user?

```
Division Function Analysis:

Input: divide(a, b)
         │
         ▼
┌─────────────────────┐
│ Potential Problems: │
│                     │
│ 1. b = 0            │ ──► ZeroDivisionError (MOST LIKELY)
│ 2. a,b not numbers  │ ──► TypeError
│ 3. Invalid input    │ ──► ValueError
└─────────────────────┘
```

Step-by-Step Solution:

1. Exception Analysis:
The most likely exception is ZeroDivisionError when the second parameter (b) is zero.

```
Problem Visualization:

Normal Case:           Error Case:
┌─────────────┐       ┌─────────────┐
│ divide(10,2)│       │ divide(10,0)│
│     │       │       │     │       │
│     ▼       │       │     ▼       │
│ 10/2 = 5    │       │ 10/0 = ???  │
│     │       │       │     │       │
│     ▼       │       │     ▼       │
│ Return 5    │       │ CRASH!      │
└─────────────┘       └─────────────┘

With Error Handling:
┌─────────────┐
│ divide(10,0)│
│     │       │
│     ▼       │
│ try: 10/0   │
│     │       │
│     ▼       │
│ Exception   │
│ caught!     │
│     │       │
│     ▼       │
│ Print error │
│ Return None │
└─────────────┘
```

2. Implementation:

```python
def safe_divide(a, b):
    try:
        result = a / b
        print(f"{a} / {b} = {result}")
        return result
    except ZeroDivisionError:
        print("Error: Cannot divide by zero.")
        print("Please ensure the second number is not zero.")
        return None

# Test examples
safe_divide(10, 2)    # Normal: 10 / 2 = 5.0
safe_divide(10, 0)    # Error: Cannot divide by zero
```

```
Function Behavior Comparison:

Test Case: safe_divide(10, 2)
┌─────────────────────────────────┐
│ try:                            │
│   result = 10 / 2  ✓ Success    │
│   print("10 / 2 = 5.0")         │
│   return 5.0                    │
│ except: (skipped)               │
└─────────────────────────────────┘

Test Case: safe_divide(10, 0)
┌─────────────────────────────────┐
│ try:                            │
│   result = 10 / 0  ✗ Exception  │
│ except ZeroDivisionError:       │
│   print("Error: Cannot divide   │
│          by zero.")             │
│   return None                   │
└─────────────────────────────────┘
```

This exercise demonstrates how to identify potential exceptions, implement proper error handling, and provide meaningful feedback while maintaining program stability.

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.