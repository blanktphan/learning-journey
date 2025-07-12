# 📖 Topic: Functions and Methods

## 💡 Basic knowledge required

An understanding of variables, data types, and control flow structures (from Lessons 3.1-3.3).

## 🎯 Learning Objectives

- Define "function" and explain its role in code organization, abstraction, and reusability.
- Identify and describe the main components of a function: its signature (name, parameters) and its body.
- Understand the concept of passing "arguments" to "parameters" and the purpose of a "return value".
- Explain the basic difference between a "function" and a "method" in the context of Object-Oriented Programming.

---

### 1. Introduction: Abstraction and Reusability

As programs grow larger, we often find ourselves writing the same or similar blocks of code in multiple places. This violates the DRY (Don't Repeat Yourself) principle, making the code unnecessarily long, difficult to read, and, most importantly, hard to maintain. If a bug is found in that repeated code, it must be fixed in every single place it was copied.

A Function is the primary mechanism in programming languages designed to solve this exact problem. It is the process of encapsulating a block of code that performs a specific task, giving it a name, and allowing us to call it for reuse. This is one of the most powerful forms of abstraction.

### 2. Anatomy of a Function

A function is a named, self-contained block of code that performs a specific task. Its main components are:

-   Function Signature: This defines the "interface" of the function.
    -   Function Name: The name used to call the function.
    -   Parameters: Special variables that act as "placeholders" for the input data the function needs to work.
-   Function Body: The block of code (often inside `{}` or indented) that contains the set of instructions to be executed when the function is called.
-   Return Statement: The `return` keyword is used to send the "result" of the function's work back to the code that called it.

```
+-----------------------+
| Signature:            |
|  name(parameter)      |
+-----------------------+
| {                     |
|   Body:               |
|     Instructions...   |
|     return result;    |
| }                     |
+-----------------------+
```

### 3. The Mechanism of a Function Call

The process involves two key steps: definition and calling.

1.  Function Definition: This is where you create the function and specify what it does.
2.  Function Call: This is where you execute the code inside the function by using its name and providing arguments, which are the actual values you want to pass into the function's parameters.

Example (Python-like syntax):

```python
# 1. Function Definition
# 'width' and 'height' are the PARAMETERS.
def calculate_rectangle_area(width, height):
    area = width * height
    return area  # Send the calculated area back

# 2. Function Call
# 10 and 5 are the ARGUMENTS being passed.
result = calculate_rectangle_area(10, 5)

# 3. 'result' now holds the value 50.
print(result)
```

### 4. Function vs. Method

In practice, you will hear these two terms used frequently. They have a slight conceptual difference:

-   Function: An independent block of code that is not tied to any object. It is common in procedural and functional programming paradigms.
    -   Example: `print("Hello")`

-   Method: A special type of function that belongs to an object or a class. It is called on an object (using dot notation) and often operates on the data contained within that object. This is a core concept in Object-Oriented Programming (OOP).
    -   Example:
        ```python
        my_name = "Alice"
        # .upper() is a METHOD of the string object.
        uppercase_name = my_name.upper()
        ```

---

## 📋 Comprehensive Summary & Practical Exercise

### Comprehensive Summary

A function is a named, reusable block of code and is the primary tool for creating abstraction and following the DRY (Don't Repeat Yourself) principle. It consists of a name, parameters (inputs), and can have a return value (output). A method is simply a function that belongs to an object in the world of OOP.

### Practical Exercise

You need to write code that checks if a given number is an "even number".

1.  Design a function named `is_even` that accepts one number as a parameter.
2.  Inside the function, what logic is needed to check if the number is even? (Hint: use the modulus operator `%`).
3.  What data type should this function return?

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
