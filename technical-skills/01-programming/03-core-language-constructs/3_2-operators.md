# 📖 Operators

## 💡 Basic knowledge required:

Understanding of variables and data types concepts (covered in lesson 3.1)

## 🎯 Learning Objectives

Upon completion of this topic, you will be able to:

- Define "operator" as a symbol used to perform operations on data (operands)
- Identify and classify the main types of operators (Arithmetic, Assignment, Comparison, Logical)
- Understand the concepts of precedence and associativity for evaluating complex expressions

---

## 1. Introduction to Operators

If variables are like "nouns" (data) in programming languages, then operators are like "verbs" (actions). An operator is a symbol used to perform mathematical operations, assign values, compare values, or perform logical operations on one or more pieces of data. The data being operated on is called operands.

### Understanding Operators and Expressions

```
Operator Anatomy
================

Expression: x + 5 * 2
            │   │   │
            │   │   └─ Operand (literal value)
            │   └───── Operator (multiplication)
            └───────── Operand (variable)

Complete Expression Structure:
┌────────────────────────────────────────────────────┐
│ Operand  Operator  Operand  Operator   Operand     │
│    x        +        5        *            2       │
│    │        │        │        │            │       │
│    └─ Data  └─ Action └─ Data  └─ Action   └─ Data │
└────────────────────────────────────────────────────┘
                    │
                    ▼
              Single Result Value
```

The combination of values, variables, and operators forms expressions, which can be evaluated to produce a single value, such as (x + 5) * 2.

### Expression Evaluation Process

```
Expression Evaluation
=====================

Input Expression: (score + bonus) * multiplier
                      │
                      ▼
Step 1: Resolve Variables
        (85 + 15) * 2.0
                      │
                      ▼
Step 2: Apply Operators
        100 * 2.0
                      │
                      ▼
Step 3: Final Result
        200.0

Expressions transform multiple values into single results
```

## 2. Main Types of Operators

Programming languages provide several categories of operators, each serving specific purposes in data manipulation and program logic.

### A. Arithmetic Operators

Arithmetic operators perform basic mathematical calculations on numeric operands.

```
Arithmetic Operators
====================

Operator │ Name          │ Example    │ Result
─────────┼───────────────┼────────────┼────────
    +    │ Addition      │ 7 + 3      │   10
    -    │ Subtraction   │ 7 - 3      │    4
    *    │ Multiplication│ 7 * 3      │   21
    /    │ Division      │ 7 / 3      │ 2.33 (or 2 if integer)
    %    │ Modulo        │ 7 % 3      │    1 (remainder)

Special Cases:
┌─────────────────────────────────────────┐
│ Integer Division:                       │
│   int result = 100 / 3;  // Result: 33  │
│   (Fractional part discarded)           │
│                                         │
│ Modulo Usage:                           │
│   int remainder = 100 % 3;  // Result: 1│
│   (Remainder after division)            │
└─────────────────────────────────────────┘
```

#### Practical Applications of Arithmetic Operators

```
Real-World Arithmetic Examples
==============================

Financial Calculations:
┌─────────────────────────────────────────┐
│ double price = 19.99;                   │
│ double tax_rate = 0.08;                 │
│ double tax = price * tax_rate;          │
│ double total = price + tax;             │
│ // total = 21.59                        │
└─────────────────────────────────────────┘

Time and Date Calculations:
┌───────────────────────────────────────────┐
│ int total_seconds = 3665;                 │
│ int hours = total_seconds / 3600;         │
│ int minutes = (total_seconds % 3600) / 60;│
│ int seconds = total_seconds % 60;         │
│ // 1 hour, 1 minute, 5 seconds            │
└───────────────────────────────────────────┘

Modulo for Patterns:
┌─────────────────────────────────────────┐
│ // Check if number is even              │
│ bool is_even = (number % 2 == 0);       │
│                                         │
│ // Cycle through values 0, 1, 2         │
│ int cycle_position = counter % 3;       │
└─────────────────────────────────────────┘
```

### B. Assignment Operators

Assignment operators are used to assign values to variables, with basic and compound forms available.

```
Assignment Operators
====================

Basic Assignment:
┌─────────────────────────────────────────┐
│ = (Assignment)                          │
│   Assigns value from right to left      │
│   int x = 10;  // x now contains 10     │
└─────────────────────────────────────────┘

Compound Assignment:
┌─────────────────────────────────────────┐
│ Operator │ Example     │ Equivalent     │
│ ─────────┼─────────────┼─────────────── │
│    +=    │ x += 5      │ x = x + 5      │
│    -=    │ x -= 3      │ x = x - 3      │
│    *=    │ x *= 2      │ x = x * 2      │
│    /=    │ x /= 4      │ x = x / 4      │
│    %=    │ x %= 3      │ x = x % 3      │
└─────────────────────────────────────────┘

Example Usage:
┌─────────────────────────────────────────┐
│ int level = 10;                         │
│ level += 5;   // level is now 15        │
│ level *= 2;   // level is now 30        │
│ level /= 3;   // level is now 10        │
└─────────────────────────────────────────┘
```

#### Assignment Flow and Memory Updates

```
Assignment Process
==================

Memory Before: level = 10
┌─────────────────────────────────────────┐
│ Variable: level                         │
│ Address:  0x1000                        │
│ Value:    10                            │
└─────────────────────────────────────────┘
                    │
                    ▼ level += 5
Calculation: 10 + 5 = 15
                    │
                    ▼
Memory After: level = 15
┌─────────────────────────────────────────┐
│ Variable: level                         │
│ Address:  0x1000                        │
│ Value:    15                            │
└─────────────────────────────────────────┘

Compound assignment = Arithmetic + Assignment in one step
```

### C. Comparison/Relational Operators

Comparison operators compare two values and always return a Boolean result (true or false).

```
Comparison Operators
====================

Operator │ Name                    │ Example     │ Result
─────────┼─────────────────────────┼─────────────┼────────
   ==    │ Equal to                │ 5 == 5      │  true
   !=    │ Not equal to            │ 5 != 3      │  true
   >     │ Greater than            │ 7 > 3       │  true
   <     │ Less than               │ 3 < 7       │  true
   >=    │ Greater than or equal   │ 5 >= 5      │  true
   <=    │ Less than or equal      │ 3 <= 7      │  true

Important Notes:
┌─────────────────────────────────────────┐
│ Comparison vs Assignment:               │
│   x = 5     // Assignment (sets value)  │
│   x == 5    // Comparison (tests value) │
│                                         │
│ Common Mistake:                         │
│   if (x = 5)    // Wrong! Assignment    │
│   if (x == 5)   // Correct! Comparison  │
└─────────────────────────────────────────┘
```

#### Practical Comparison Examples

```
Real-World Comparisons
======================

Age Verification:
┌─────────────────────────────────────────┐
│ int user_age = 20;                      │
│ bool can_vote = (user_age >= 18);       │
│ bool is_senior = (user_age >= 65);      │
│ bool is_teenager = (user_age >= 13 &&   │
│                     user_age <= 19);    │
└─────────────────────────────────────────┘

Grade Classification:
┌─────────────────────────────────────────┐
│ double score = 87.5;                    │
│ bool passed = (score >= 60.0);          │
│ bool excellent = (score >= 90.0);       │
│ bool needs_improvement = (score < 70.0);│
└─────────────────────────────────────────┘

String Comparisons:
┌──────────────────────────────────────────┐
│ string username = "admin";               │
│ bool is_admin = (username == "admin");   │
│ bool is_guest = (username != "admin");   │
└──────────────────────────────────────────┘
```

### D. Logical Operators

Logical operators connect two or more Boolean expressions or invert Boolean values.

```
Logical Operators
=================

Operator │ Name │ Description                    │ Symbol
─────────┼──────┼────────────────────────────────┼────────
   &&    │ AND  │ True if both operands are true │   ∧
   ||    │ OR   │ True if either operand is true │   ∨
   !     │ NOT  │ Inverts the Boolean value      │   ¬

Truth Tables:
┌─────────────────────────────────────────┐
│ AND (&&) Truth Table:                   │
│ A     │ B     │ A && B                  │
│ ──────┼───────┼────────                 │
│ true  │ true  │ true                    │
│ true  │ false │ false                   │
│ false │ true  │ false                   │
│ false │ false │ false                   │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│ OR (||) Truth Table:                    │
│ A     │ B     │ A || B                  │
│ ──────┼───────┼────────                 │
│ true  │ true  │ true                    │
│ true  │ false │ true                    │
│ false │ true  │ true                    │
│ false │ false │ false                   │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│ NOT (!) Truth Table:                    │
│ A     │ !A                              │
│ ──────┼────                             │
│ true  │ false                           │
│ false │ true                            │
└─────────────────────────────────────────┘
```

#### Logical Operator Applications

```
Complex Logical Conditions
===========================

Access Control:
┌─────────────────────────────────────────┐
│ bool has_key = true;                    │
│ bool is_authorized = false;             │
│ bool is_emergency = true;               │
│                                         │
│ bool can_enter = (has_key && is_authorized) ||│
│                  is_emergency;          │
│ // Result: true (emergency access)      │
└─────────────────────────────────────────┘

Input Validation:
┌─────────────────────────────────────────────┐
│ int age = 25;                               │
│ string email = "user@domain.com";           │
│ bool email_valid = (email.length() > 0 &&   │
│                     email.contains("@"));   │
│ bool age_valid = (age >= 0 && age <= 120);  │
│ bool form_valid = email_valid && age_valid; │
└─────────────────────────────────────────────┘

Game Logic:
┌─────────────────────────────────────────────┐
│ bool has_ammo = true;                       │
│ bool enemy_in_range = false;                │
│ bool weapon_ready = true;                   │
│                                             │
│ bool can_shoot = has_ammo && enemy_in_range │
│                  && weapon_ready;           │
│ // Result: false (no enemy in range)        │
└─────────────────────────────────────────────┘
```

## 3. Operator Precedence and Associativity

When evaluating complex expressions like a + b * c, programming languages have clear rules to ensure consistent results.

### Understanding Precedence

```
Operator Precedence Hierarchy
==============================

High Precedence (Evaluated First):
┌─────────────────────────────────────────┐
│ 1. Parentheses          ()              │
│ 2. Unary operators      ! - +           │
│ 3. Multiplicative       * / %           │
│ 4. Additive             + -             │
│ 5. Relational           < > <= >=       │
│ 6. Equality             == !=           │
│ 7. Logical AND          &&              │
│ 8. Logical OR           ||              │
│ 9. Assignment           = += -= *= /=   │
└─────────────────────────────────────────┘
Low Precedence (Evaluated Last)

Example: 10 + 5 * 2
Step 1: 5 * 2 = 10 (multiplication first)
Step 2: 10 + 10 = 20 (then addition)
```

### Precedence Examples

```
Precedence in Action
====================

Mathematical Expression:
┌─────────────────────────────────────────┐
│ int result = 10 + 5 * 2;                │
│                                         │
│ Without precedence: (10 + 5) * 2 = 30   │
│ With precedence: 10 + (5 * 2) = 20      │
│                                         │
│ Actual result: 20                       │
└─────────────────────────────────────────┘

Logical Expression:
┌───────────────────────────────────────────┐
│ bool result = true || false && false;     │
│                                           │
│ Step 1: false && false = false (AND first)│
│ Step 2: true || false = true (then OR)    │
│                                           │
│ Actual result: true                       │
└───────────────────────────────────────────┘

Mixed Expression:
┌─────────────────────────────────────────┐
│ bool result = 10 > 5 && 3 < 7;          │
│                                         │
│ Step 1: 10 > 5 = true (comparison first)│
│ Step 2: 3 < 7 = true (comparison first) │
│ Step 3: true && true = true (then AND)  │
│                                         │
│ Actual result: true                     │
└─────────────────────────────────────────┘
```

### Understanding Associativity

```
Associativity Rules
===================

Left-to-Right Associativity (Most operators):
┌─────────────────────────────────────────┐
│ Expression: 100 - 10 + 5                │
│                                         │
│ Step 1: 100 - 10 = 90 (leftmost first)  │
│ Step 2: 90 + 5 = 95 (then next)         │
│                                         │
│ Result: 95                              │
│                                         │
│ NOT: 100 - (10 + 5) = 85                │
└─────────────────────────────────────────┘

Right-to-Left Associativity (Assignment):
┌─────────────────────────────────────────┐
│ Expression: x = y = z = 5               │
│                                         │
│ Step 1: z = 5 (rightmost first)         │
│ Step 2: y = z (which is 5)              │
│ Step 3: x = y (which is 5)              │
│                                         │
│ Result: x = y = z = 5                   │
└─────────────────────────────────────────┘

Chain of Operations:
┌─────────────────────────────────────────┐
│ Expression: a = b += c *= 2             │
│                                         │
│ Step 1: c *= 2 (rightmost assignment)   │
│ Step 2: b += c (middle assignment)      │
│ Step 3: a = b (leftmost assignment)     │
└─────────────────────────────────────────┘
```

## 4. Complex Expression Evaluation

### Step-by-Step Expression Analysis

```
Complex Expression Breakdown
============================

Expression: (score + bonus) * 1.1 > passing_grade && attempts < 3

Given Values:
score = 85, bonus = 10, passing_grade = 90, attempts = 2

Step-by-Step Evaluation:
┌─────────────────────────────────────────┐
│ 1. Parentheses first:                   │
│    (85 + 10) = 95                       │
│                                         │
│ 2. Multiplication:                      │
│    95 * 1.1 = 104.5                     │
│                                         │
│ 3. Comparisons (left to right):         │
│    104.5 > 90 = true                    │
│    2 < 3 = true                         │
│                                         │
│ 4. Logical AND:                         │
│    true && true = true                  │
│                                         │
│ Final Result: true                      │
└─────────────────────────────────────────┘
```

### Using Parentheses for Clarity

```
Parentheses for Explicit Ordering
==================================

Ambiguous Expression:
┌─────────────────────────────────────────┐
│ result = a + b * c + d;                 │
│ // Relies on operator precedence        │
│ // Hard to read and verify              │
└─────────────────────────────────────────┘

Clear Expression:
┌─────────────────────────────────────────┐
│ result = a + (b * c) + d;               │
│ // Explicit about multiplication first  │
│ // Easy to understand intention         │
└─────────────────────────────────────────┘

Complex Logical Expression:
┌─────────────────────────────────────────────┐
│ // Ambiguous                                │
│ if (age >= 18 && has_license || is_adult)   │
│                                             │
│ // Clear                                    │
│ if ((age >= 18 && has_license) || is_adult) │
│                                             │
│ // Very clear                               │
│ bool eligible = (age >= 18 && has_license); │
│ if (eligible || is_adult)                   │
└─────────────────────────────────────────────┘
```

## 5. Common Operator Mistakes and Best Practices

### Frequent Pitfalls

```
Common Operator Errors
======================

1. Assignment vs Comparison:
┌─────────────────────────────────────────┐
│ // WRONG - Assignment in condition      │
│ if (x = 5) {  // Always true!           │
│     // This assigns 5 to x              │
│ }                                       │
│                                         │
│ // CORRECT - Comparison in condition    │
│ if (x == 5) {  // Tests if x equals 5   │
│     // This compares x with 5           │
│ }                                       │
└─────────────────────────────────────────┘

2. Integer Division Precision Loss:
┌─────────────────────────────────────────┐
│ // WRONG - Loses decimal precision      │
│ int average = (a + b + c) / 3;          │
│ // If sum is 10, result is 3 (not 3.33) │
│                                         │
│ // CORRECT - Preserves precision        │
│ double average = (a + b + c) / 3.0;     │
│ // Result includes decimal places       │
└─────────────────────────────────────────┘

3. Logical Operator Confusion:
┌─────────────────────────────────────────┐
│ // WRONG - Missing logical operator     │
│ if (x > 0 && < 10) {  // Syntax error   │
│                                         │
│ // CORRECT - Complete comparisons       │
│ if (x > 0 && x < 10) {                  │
└─────────────────────────────────────────┘
```

### Best Practices

```
Operator Best Practices
=======================

1. Use Parentheses for Clarity:
┌─────────────────────────────────────────┐
│ // Good - Clear intention               │
│ total = (price * quantity) + tax;       │
│ valid = (age >= 18) && (has_id);        │
└─────────────────────────────────────────┘

2. Break Complex Expressions:
┌────────────────────────────────────────────┐
│ // Instead of:                             │
│ if ((a > b && c < d) || (x == y && z != w))│
│                                            │
│ // Use:                                    │
│ bool condition1 = (a > b && c < d);        │
│ bool condition2 = (x == y && z != w);      │
│ if (condition1 || condition2) {            │
└────────────────────────────────────────────┘

3. Consistent Spacing:
┌─────────────────────────────────────────┐
│ // Good - Readable spacing              │
│ result = (a + b) * (c - d);             │
│ valid = (x >= 0) && (x <= 100);         │
│                                         │
│ // Avoid - Cramped or inconsistent      │
│ result=(a+b)*(c-d);                     │
│ valid = (x>=0)&&(x<=100);               │
└─────────────────────────────────────────┘
```

---

## 📋 Summary & Practical Exercise

### Comprehensive Summary

Operators are the fundamental symbols that enable computation, comparison, and logical reasoning in programming. They serve as the "verbs" that act upon data (operands) to create expressions that can be evaluated to produce results. Understanding operators and their behavior is essential for writing correct and efficient programs.

Key Concepts:

Operator Categories:
- Arithmetic operators perform mathematical calculations (+, -, *, /, %)
- Assignment operators store values in variables (=, +=, -=, *=, /=, %=)
- Comparison operators test relationships between values (==, !=, >, <, >=, <=)
- Logical operators combine Boolean expressions (&&, ||, !)

Expression Evaluation:
- Precedence determines which operators are evaluated first
- Associativity determines the order for operators of equal precedence
- Parentheses can override default precedence for explicit control
- Complex expressions should be broken down for clarity and maintainability

Type Considerations:
- Operators must be compatible with their operand types
- Integer division may lose decimal precision
- Comparison operators always return Boolean values
- Logical operators work specifically with Boolean values

Essential Insight: Mastering operators and expression evaluation is crucial for translating mathematical and logical thinking into working code. Clear understanding of precedence and associativity prevents bugs and makes code predictable and maintainable.

### Practical Exercise

Analyze and evaluate complex expressions to understand operator precedence, associativity, and type interactions in realistic programming scenarios.

#### Exercise Steps:

Step 1: Expression Analysis
Given the following complex expression, trace through its evaluation step by step:

```
Expression Evaluation Challenge
===============================

Expression: 
bool result = (10 > 5) && !(7 == 7) || (10 % 3 == 1);

Given precedence order:
() > ! > * / % > + - > > < >= <= > == != > && > ||

Your task:
1. Identify all operators and their precedence levels
2. Show the step-by-step evaluation process
3. Determine the final result
```

Step 2: Create Your Own Expressions
Design expressions that demonstrate different operator interactions:

```
Expression Design Framework
===========================

Arithmetic Expression:
┌──────────────────────────────────────────────────┐
│ Create an expression that:                       │
│ • Uses at least 3 different arithmetic operators │
│ • Includes parentheses                           │
│ • Tests mathematical precedence                  │
│                                                  │
│ Your expression: _________________               │
│ Expected result: _________________               │
└──────────────────────────────────────────────────┘

Logical Expression:
┌─────────────────────────────────────────────┐
│ Create an expression that:                  │
│ • Combines comparison and logical operators │
│ • Uses both && and || operators             │
│ • Tests a real-world condition              │
│                                             │
│ Your expression: _________________          │
│ Expected result: _________________          │
└─────────────────────────────────────────────┘
```

Step 3: Debug Common Mistakes
Identify and fix errors in problematic expressions:

```
Error Detection Exercise
========================

Find and explain the problems:

1. if (x = 10 && y > 5) { ... }
   Error: ________________________
   Fix: __________________________

2. double average = sum / count;
   (where sum=10, count=3, expecting 3.333...)
   Error: ________________________
   Fix: __________________________

3. bool valid = age >= 18 && <= 65;
   Error: ________________________
   Fix: __________________________
```

Step 4: Real-World Application
Design expressions for practical programming scenarios:

#### Analysis Questions:

1. Precedence Understanding:
   - How does operator precedence affect the reliability of your code?
   - When should you use parentheses even if they're not required?
   - What strategies help you remember precedence rules?

2. Type Safety:
   - How do different data types affect operator behavior?
   - What unexpected results can occur from type mismatches?
   - How can you prevent precision loss in calculations?

3. Code Clarity:
   - How do you balance concise expressions with readable code?
   - When should complex expressions be broken into multiple statements?
   - How do naming conventions help with expression clarity?

#### Extension Challenge:

Advanced Exercise: Expression optimization and validation

1. Performance Considerations:
   - Analyze how operator choice affects execution speed
   - Design expressions that minimize unnecessary calculations
   - Consider short-circuit evaluation in logical expressions

2. Robust Expression Design:
   - Create expressions that handle edge cases gracefully
   - Design validation expressions for user input
   - Build expressions that are resilient to unexpected data types

3. Expression Patterns:
   - Identify common expression patterns in your problem domain
   - Create reusable expression templates
   - Design expressions that scale well with changing requirements

This exercise demonstrates how operators form the foundation of computational thinking in code, enabling the translation of mathematical and logical concepts into working programs while emphasizing the importance of clarity and correctness in expression design.

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
