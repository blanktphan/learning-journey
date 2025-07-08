# 📖 Control Flow: Conditional Statements and Loops

## 💡 Basic knowledge required:

Understanding of variables and especially comparison and logical operators that produce Boolean results (covered in lessons 3.1-3.2)

## 🎯 Learning Objectives

Upon completion of this topic, you will be able to:

- Define "Control Flow" and explain its importance in creating programs that execute non-linearly
- Understand and write conditional statements using if, else if, and else to create decision branches
- Understand and write loop statements using while and for to make code execute repeatedly
- Distinguish appropriate use cases for while loops versus for loops

---

## 1. Introduction to Control Flow

By default, computers process our programs sequentially - executing commands from the top line down to the bottom line, one instruction at a time. Control Flow is a set of statements in programming languages that allows us to change this execution order. It enables our programs to "make decisions" to skip certain instructions or "loop back" to repeat certain sets of instructions multiple times. This is what makes programs intelligent and responsive to different situations.

### Understanding Program Execution Flow

```
Sequential vs Control Flow Execution
====================================

Sequential Execution (Default):
┌─────────────────────────────────────────┐
│ Line 1: int x = 10;                     │
│ Line 2: int y = 20;          ▼          │
│ Line 3: int sum = x + y;     ▼          │
│ Line 4: print(sum);          ▼          │
│ Line 5: // End program       ▼          │
└─────────────────────────────────────────┘
Always executes: 1 → 2 → 3 → 4 → 5

Control Flow Execution:
┌──────────────────────────────────────────┐
│ Line 1: int score = 85;                  │
│ Line 2: if (score >= 80) {    ◄─┐        │
│ Line 3:     print("Pass");       │       │
│ Line 4: } else {                 │       │
│ Line 5:     print("Fail");    ◄─┘ (skip) │
│ Line 6: }                                │
└──────────────────────────────────────────┘
Conditional execution: 1 → 2 → 3 → 6 (skip 5)
```

### Why Control Flow Matters

```
Real-World Control Flow Examples
================================

Banking System Logic:
┌───────────────────────────────────────────┐
│ if (balance >= withdrawal_amount) {       │
│     // Process withdrawal                 │
│     balance = balance - withdrawal_amount;│
│ } else {                                  │
│     // Deny transaction                   │
│     print("Insufficient funds");          │
│ }                                         │
└───────────────────────────────────────────┘

Game Character Movement:
┌─────────────────────────────────────────┐
│ while (player_is_alive) {               │
│     // Get player input                 │
│     // Update player position           │
│     // Check for collisions             │
│     // Render game frame                │
│ }                                       │
└─────────────────────────────────────────┘

Data Processing:
┌─────────────────────────────────────────┐
│ for (each student in class_roster) {    │
│     // Calculate individual grade       │
│     // Add to total for class average   │
│     // Check if grade meets requirements│
│ }                                       │
└─────────────────────────────────────────┘
```

## 2. Conditional Statements: The Power of Decision Making

Conditional statements create "branches" or "choices" in your program, executing different blocks of code depending on whether a condition evaluates to true or false.

### Basic if Statement

The simplest form of decision making - execute code only when a condition is true.

```
if Statement Structure
======================

Syntax:
┌─────────────────────────────────────────┐
│ if (condition) {                        │
│     // Code block executed only         │
│     // when condition is true           │
│ }                                       │
└─────────────────────────────────────────┘

Flow Diagram:
         condition
         true/false?
            │
     ┌──────┴────────┐
   true           false
     │               │
     ▼               │
 Execute Code        │
 Block               │
     │               │
     └───────┬───────┘
             ▼
      Continue Program
```

#### Practical if Examples

```
Real-World if Statement Applications
====================================

Weather Decision:
┌──────────────────────────────────────────┐
│ boolean isRaining = true;                │
│ if (isRaining == true) {                 │
│     System.out.println("Bring umbrella");│
│ }                                        │
│ // Program continues regardless          │
└──────────────────────────────────────────┘

Security Check:
┌───────────────────────────────────────────┐
│ boolean hasPermission = checkUserAccess();│
│ if (hasPermission) {                      │
│     // Allow access to sensitive data     │
│     loadSecretFiles();                    │
│ }                                         │
│ // Continue with normal operation         │
└───────────────────────────────────────────┘

Input Validation:
┌─────────────────────────────────────────┐
│ int age = getUserInput();               │
│ if (age < 0 || age > 150) {             │
│     System.out.println("Invalid age");  │
│     // Request input again              │
│ }                                       │
└─────────────────────────────────────────┘
```

### if-else Statement

Creates a clear two-way choice - one path for true, another for false.

```
if-else Structure
=================

Syntax:
┌─────────────────────────────────────────┐
│ if (condition) {                        │
│     // Code executed when condition     │
│     // is true                          │
│ } else {                                │
│     // Code executed when condition     │
│     // is false                         │
│ }                                       │
└─────────────────────────────────────────┘

Flow Diagram:
         condition
         true/false?
            │
     ┌──────┴────────┐
   true           false
     │               │
     ▼               ▼
Execute if         Execute else
Block              Block
     │               │
     └───────┬───────┘
             ▼
      Continue Program
```

#### Practical if-else Examples

```
Binary Decision Making
======================

Weather Decision:
┌───────────────────────────────────────────┐
│ boolean isRaining = true;                 │
│ if (isRaining == true) {                  │
│     System.out.println("Bring umbrella"); │
│ } else {                                  │
│     System.out.println("Wear sunglasses");│
│ }                                         │
└───────────────────────────────────────────┘

Access Control:
┌───────────────────────────────────────────┐
│ boolean isAuthorized = checkCredentials();│
│ if (isAuthorized) {                       │
│     System.out.println("Access granted"); │
│     openMainMenu();                       │
│ } else {                                  │
│     System.out.println("Access denied");  │
│     redirectToLogin();                    │
│ }                                         │
└───────────────────────────────────────────┘

Number Classification:
┌─────────────────────────────────────────┐
│ int number = 7;                         │
│ if (number % 2 == 0) {                  │
│     System.out.println("Even number");  │
│ } else {                                │
│     System.out.println("Odd number");   │
│ }                                       │
└─────────────────────────────────────────┘
```

### if-else if-else Statement

Creates multiple decision branches for complex scenarios with more than two possibilities.

```
Multi-way Conditional Structure
===============================

Syntax:
┌─────────────────────────────────────────┐
│ if (condition1) {                       │
│     // Execute if condition1 is true    │
│ } else if (condition2) {                │
│     // Execute if condition2 is true    │
│ } else if (condition3) {                │
│     // Execute if condition3 is true    │
│ } else {                                │
│     // Execute if all conditions false  │
│ }                                       │
└─────────────────────────────────────────┘

Evaluation Flow:
condition1? ──true──> Execute Block 1 ──┐
    │                                   │
  false                                 │
    ▼                                   │
condition2? ──true──> Execute Block 2 ──┤
    │                                   │
  false                                 │
    ▼                                   │
condition3? ──true──> Execute Block 3 ──┤
    │                                   │
  false                                 │
    ▼                                   │
Execute else Block ─────────────────────┘
    │
    ▼
Continue Program

Important: Only ONE block executes, then program continues
```

#### Grade Classification Example

```
Complex Decision Making
=======================

Student Grade Assignment:
┌─────────────────────────────────────────────┐
│ int score = 85;                             │
│ char grade;                                 │
│                                             │
│ if (score >= 90) {                          │
│     grade = 'A';                            │
│     System.out.println("Excellent!");       │
│ } else if (score >= 80) {                   │
│     grade = 'B';  // <── Executes here      │
│     System.out.println("Good job!");        │
│ } else if (score >= 70) {                   │
│     grade = 'C';  // <── Skipped            │
│     System.out.println("Satisfactory");     │
│ } else if (score >= 60) {                   │
│     grade = 'D';  // <── Skipped            │
│     System.out.println("Needs improvement");│
│ } else {                                    │
│     grade = 'F';  // <── Skipped            │
│     System.out.println("Failed");           │
│ }                                           │
│ // grade = 'B' and program continues        │
└─────────────────────────────────────────────┘

Traffic Light System:
┌───────────────────────────────────────────┐
│ String lightColor = "yellow";             │
│                                           │
│ if (lightColor.equals("red")) {           │
│     System.out.println("Stop");           │
│ } else if (lightColor.equals("yellow")) { │
│     System.out.println("Prepare to stop");│
│ } else if (lightColor.equals("green")) {  │
│     System.out.println("Go");             │
│ } else {                                  │
│     System.out.println("Invalid signal"); │
│ }                                         │
└───────────────────────────────────────────┘
```

## 3. Loop Statements: The Art of Repetition

Loops allow programs to execute a block of code repeatedly, which is essential for automation and processing collections of data.

### while Loop: Condition-Based Repetition

A while loop continues executing as long as a specified condition remains true. The condition is checked before each iteration.

```
while Loop Structure
====================

Syntax:
┌─────────────────────────────────────────┐
│ while (condition) {                     │
│     // Code block that executes         │
│     // repeatedly while condition       │
│     // remains true                     │
│                                         │
│     // IMPORTANT: Must modify condition │
│     // variable to avoid infinite loop  │
│ }                                       │
└─────────────────────────────────────────┘

Flow Diagram:
    Start
      │
      ▼
  Check condition ◄─────┐
      │                 │
   true/false?          │
      │                 │
  ┌───┴─────┐           │
true     false          │
  │         │           │
  ▼         ▼           │
Execute   Exit Loop     │
Code Block    │         │
  │           │         │
  └───────────┘         │
      │                 │
      └─────────────────┘
```

#### Use Cases and Examples

```
while Loop Applications
=======================

Use Case: Unknown number of iterations, condition-dependent

Password Validation:
┌─────────────────────────────────────────────┐
│ String correctPassword = "secret123";       │
│ String userInput = "";                      │
│                                             │
│ while (!userInput.equals(correctPassword)) {│
│     System.out.println("Enter password:");  │
│     userInput = scanner.nextLine();         │
│     // Loop continues until correct         │
│     // password is entered                  │
│ }                                           │
│ System.out.println("Access granted!");      │
└─────────────────────────────────────────────┘

Countdown Timer:
┌─────────────────────────────────────────┐
│ int countdown = 10;                     │
│                                         │
│ while (countdown > 0) {                 │
│     System.out.println(countdown);      │
│     countdown--;  // Modify condition   │
│     // Sleep for 1 second               │
│ }                                       │
│ System.out.println("Launch!");          │
└─────────────────────────────────────────┘

Game Main Loop:
┌─────────────────────────────────────────┐
│ boolean gameRunning = true;             │
│                                         │
│ while (gameRunning) {                   │
│     // Get player input                 │
│     processInput();                     │
│     // Update game state                │
│     updateGame();                       │
│     // Render frame                     │
│     drawScreen();                       │
│     // Check if player wants to quit    │
│     gameRunning = !playerWantsToQuit(); │
│ }                                       │
└─────────────────────────────────────────┘
```

### for Loop: Count-Based or Collection-Based Repetition

A for loop is designed to execute a specific number of times or to iterate through each element in a collection.

```
for Loop Structure
==================

Traditional for Loop (Count-based):
┌──────────────────────────────────────────┐
│ for (initialization; condition; update) {│
│     // Code block executed each          │
│     // iteration                         │
│ }                                        │
│                                          │
│ Example:                                 │
│ for (int i = 0; i < 5; i++) {            │
│     System.out.println("Count: " + i);   │
│ }                                        │
└──────────────────────────────────────────┘

Enhanced for Loop (Collection-based):
┌─────────────────────────────────────────┐
│ for (dataType variable : collection) {  │
│     // Code block executed for each     │
│     // element in collection            │
│ }                                       │
│                                         │
│ Example:                                │
│ String[] fruits = {"Apple", "Banana"};  │
│ for (String fruit : fruits) {           │
│     System.out.println(fruit);          │
│ }                                       │
└─────────────────────────────────────────┘

Traditional for Loop Flow:
┌─────────────────────────────────────────┐
│ Initialize counter variable             │
│         │                               │
│         ▼                               │
│    Check condition ◄────────────┐       │
│         │                       │       │
│      true/false?                │       │
│         │                       │       │
│    ┌────┴──────┐                │       │
│  true       false               │       │
│    │           │                │       │
│    ▼           ▼                │       │
│ Execute     Exit Loop           │       │
│ Code Block     │                │       │
│    │           │                │       │
│    ▼           │                │       │
│ Update counter │                │       │
│    │           │                │       │
│    └───────────┘                │       │
│         │                       │       │
│         └───────────────────────┘       │
└─────────────────────────────────────────┘
```

#### for Loop Applications

```
for Loop Use Cases
==================

Use Case: Known number of iterations or processing collections

Counting and Calculations:
┌─────────────────────────────────────────┐
│ // Print numbers 1 to 10                │
│ for (int i = 1; i <= 10; i++) {         │
│     System.out.println("Number: " + i); │
│ }                                       │
│                                         │
│ // Calculate factorial                  │
│ int factorial = 1;                      │
│ for (int i = 1; i <= 5; i++) {          │
│     factorial = factorial * i;          │
│ }                                       │
│ // factorial = 120 (5!)                 │
└─────────────────────────────────────────┘

Array Processing:
┌──────────────────────────────────────────┐
│ int[] scores = {85, 92, 78, 96, 88};     │
│ int total = 0;                           │
│                                          │
│ // Traditional for loop                  │
│ for (int i = 0; i < scores.length; i++) {│
│     total += scores[i];                  │
│ }                                        │
│                                          │
│ // Enhanced for loop (cleaner)           │
│ for (int score : scores) {               │
│     total += score;                      │
│ }                                        │
│ double average = total / scores.length;  │
└──────────────────────────────────────────┘

String Processing:
┌─────────────────────────────────────────────────┐
│ String[] fruits = {"Apple", "Banana", "Cherry"};│
│                                                 │
│ for (String fruit : fruits) {                   │
│     System.out.println("Fruit: " + fruit);      │
│ }                                               │
│                                                 │
│ // Output:                                      │
│ // Fruit: Apple                                 │
│ // Fruit: Banana                                │
│ // Fruit: Cherry                                │
└─────────────────────────────────────────────────┘
```

## 4. Choosing Between while and for Loops

Understanding when to use each type of loop is crucial for writing clear and efficient code.

### Decision Framework

```
Loop Selection Guide
====================

Use while loop when:
┌─────────────────────────────────────────┐
│ ✓ Number of iterations is UNKNOWN       │
│ ✓ Loop depends on external conditions   │
│ ✓ Loop continues until specific event   │
│ ✓ User input determines when to stop    │
│                                         │
│ Examples:                               │
│ • Reading file until end reached        │
│ • Getting user input until valid        │
│ • Game running until player quits       │
│ • Server running until shutdown signal  │
└─────────────────────────────────────────┘

Use for loop when:
┌─────────────────────────────────────────┐
│ ✓ Number of iterations is KNOWN         │
│ ✓ Processing all items in collection    │
│ ✓ Counting through range of numbers     │
│ ✓ Repeating action specific number times│
│                                         │
│ Examples:                               │
│ • Process all students in class         │
│ • Count from 1 to 100                   │
│ • Initialize array with default values  │
│ • Generate multiplication table         │
└─────────────────────────────────────────┘
```

### Comparative Examples

```
Same Task, Different Approaches
===============================

Task: Print numbers 1 to 5

Using for loop (Natural choice):
┌─────────────────────────────────────────┐
│ for (int i = 1; i <= 5; i++) {          │
│     System.out.println(i);              │
│ }                                       │
│ // Clear, concise, obvious intent       │
└─────────────────────────────────────────┘

Using while loop (Possible but awkward):
┌─────────────────────────────────────────┐
│ int i = 1;                              │
│ while (i <= 5) {                        │
│     System.out.println(i);              │
│     i++;  // Easy to forget!            │
│ }                                       │
│ // More verbose, error-prone            │
└─────────────────────────────────────────┘

Task: Read user input until "quit"

Using while loop (Natural choice):
┌──────────────────────────────────────────┐
│ String input = "";                       │
│ while (!input.equals("quit")) {          │
│     System.out.println("Enter command:");│
│     input = scanner.nextLine();          │
│     processCommand(input);               │
│ }                                        │
│ // Clear intent, appropriate structure   │
└──────────────────────────────────────────┘

Using for loop (Impossible/inappropriate):
┌─────────────────────────────────────────┐
│ // Cannot use for loop effectively      │
│ // because we don't know how many       │
│ // commands user will enter             │
└─────────────────────────────────────────┘
```

## 5. Common Control Flow Patterns and Best Practices

### Nested Control Structures

```
Combining Control Flow Elements
===============================

Nested if Statements:
┌─────────────────────────────────────────┐
│ if (userLoggedIn) {                     │
│     if (hasPermission) {                │
│         if (accountActive) {            │
│             // Allow operation          │
│         } else {                        │
│             // Account suspended        │
│         }                               │
│     } else {                            │
│         // Insufficient permissions     │
│     }                                   │
│ } else {                                │
│     // Redirect to login                │
│ }                                       │
└─────────────────────────────────────────┘

Loops with Conditionals:
┌──────────────────────────────────────────────────┐
│ for (int i = 0; i < students.length; i++) {      │
│     if (students[i].getGrade() >= 90) {          │
│         System.out.println(students[i].getName() │
│                          + " - Excellent");      │
│     } else if (students[i].getGrade() >= 60) {   │
│         System.out.println(students[i].getName() │
│                          + " - Passed");         │
│     } else {                                     │
│         System.out.println(students[i].getName() │
│                          + " - Failed");         │
│     }                                            │
│ }                                                │
└──────────────────────────────────────────────────┘

Nested Loops:
┌──────────────────────────────────────────┐
│ // Multiplication table                  │
│ for (int i = 1; i <= 10; i++) {          │
│     for (int j = 1; j <= 10; j++) {      │
│         System.out.print((i * j) + "\t");│
│     }                                    │
│     System.out.println(); // New line    │
│ }                                        │
└──────────────────────────────────────────┘
```

### Common Mistakes and How to Avoid Them

```
Control Flow Pitfalls
=====================

1. Infinite Loops:
┌─────────────────────────────────────────────┐
│ // WRONG - Never changes condition          │
│ int count = 0;                              │
│ while (count < 10) {                        │
│     System.out.println("Hello");            │
│     // Missing count++; causes infinite loop│
│ }                                           │
│                                             │
│ // CORRECT - Always modify condition        │
│ int count = 0;                              │
│ while (count < 10) {                        │
│     System.out.println("Hello");            │
│     count++;  // Essential!                 │
│ }                                           │
└─────────────────────────────────────────────┘ 

2. Off-by-One Errors:
┌─────────────────────────────────────────────┐
│ // WRONG - Misses last element              │
│ for (int i = 0; i < array.length - 1; i++) {│
│     // Processes n-1 elements               │
│ }                                           │
│                                             │
│ // CORRECT - Processes all elements         │
│ for (int i = 0; i < array.length; i++) {    │
│     // Processes all n elements             │
│ }                                           │
└─────────────────────────────────────────────┘

3. Assignment vs Comparison:
┌────────────────────────────────────────────┐
│ // WRONG - Assignment instead of comparison│
│ if (x = 5) {  // Always true!              │
│     // This assigns 5 to x                 │
│ }                                          │
│                                            │
│ // CORRECT - Comparison                    │
│ if (x == 5) {  // Tests if x equals 5      │
│     // This compares x with 5              │
│ }                                          │
└────────────────────────────────────────────┘
```

---

## 📋 Summary & Practical Exercise

### Comprehensive Summary

Control Flow is the foundation that transforms simple sequential programs into intelligent, responsive applications. It enables programs to make decisions and repeat operations, which are essential capabilities for solving real-world problems.

Key Concepts:

Decision Making:
- if statements execute code conditionally based on Boolean expressions
- if-else statements provide binary choices between two alternatives
- if-else if-else chains handle multiple exclusive conditions
- Only one branch executes in conditional chains

Repetition Control:
- while loops continue based on conditions, ideal for unknown iteration counts
- for loops execute a specific number of times or iterate through collections
- Loop choice depends on whether iteration count is known or condition-dependent
- Proper loop design prevents infinite loops and off-by-one errors

Control Flow Principles:
- Conditions must evaluate to Boolean values (true/false)
- Loop conditions must eventually become false to prevent infinite execution
- Nested structures allow complex logic but should remain readable
- Clear condition logic prevents bugs and improves maintainability

Essential Insight: Control Flow transforms static instruction lists into dynamic, interactive programs capable of handling varying inputs and conditions. Mastering these structures is crucial for implementing algorithms and creating responsive software applications.

### Practical Exercise

Apply control flow concepts to solve real-world programming scenarios that require decision making and repetition.

#### Exercise Steps:

Step 1: ATM System Analysis
Design control flow for an ATM system as mentioned in the lesson:

```
ATM System Design Challenge
===========================

Problem 1: PIN Verification
┌─────────────────────────────────────────┐
│ Task: Design logic for PIN verification │
│                                         │
│ Requirements:                           │
│ • Allow 3 attempts maximum              │
│ • Lock account after failed attempts    │
│ • Grant access on correct PIN           │
│                                         │
│ Question: Which control structure?      │
│ □ if-else (decision making)             │
│ □ while loop (condition-based)          │
│ □ for loop (count-based)                │
│                                         │
│ Your answer: ________________           │
│ Reasoning: ___________________          │
└─────────────────────────────────────────┘

Problem 2: Main ATM Operation
┌─────────────────────────────────────────┐
│ Task: Design main ATM operation loop    │
│                                         │
│ Requirements:                           │
│ • Show menu continuously                │
│ • Process user selections               │
│ • Exit only when user chooses "Quit"    │
│                                         │
│ Question: Which loop type?              │
│ □ while loop (condition-based)          │
│ □ for loop (count-based)                │
│                                         │
│ Your answer: ________________           │
│ Reasoning: ___________________          │
└─────────────────────────────────────────┘
```

Step 2: Code Implementation
Write actual code for the ATM scenarios:

```
Implementation Framework
========================

PIN Verification Code:
┌─────────────────────────────────────────┐
│ // Your code here:                      │
│ String correctPIN = "1234";             │
│ int attempts = 0;                       │
│ boolean accessGranted = false;          │
│                                         │
│ // Implement your solution              │
│                                         │
│                                         │
│                                         │
│                                         │
└─────────────────────────────────────────┘

Main ATM Loop Code:
┌─────────────────────────────────────────┐
│ // Your code here:                      │
│ boolean systemRunning = true;           │
│                                         │
│ // Implement your solution              │
│                                         │
│                                         │
│                                         │
│                                         │
└─────────────────────────────────────────┘
```

Step 3: Complex Scenario Design
Create control flow for a student grade processing system:

```
Grade Processing System
=======================

Requirements:
┌─────────────────────────────────────────┐
│ 1. Process grades for multiple students │
│ 2. Classify each grade (A, B, C, D, F)  │
│ 3. Calculate class average              │
│ 4. Count students in each grade category│
│ 5. Identify honor roll students (≥90)   │
│                                         │
│ Design questions:                       │
│ • What loops do you need?               │
│ • What conditionals are required?       │
│ • How do you handle invalid grades?     │
│                                         │
│ Your design approach:                   │
│ _____________________________________   │
│ _____________________________________   │
│ _____________________________________   │
└─────────────────────────────────────────┘
```

#### Analysis Questions:

1. Control Structure Selection:
   - How do you decide between if-else and switch statements?
   - When might nested conditionals become problematic?
   - What factors influence your choice between while and for loops?

2. Loop Design Considerations:
   - How do you ensure loops will eventually terminate?
   - What are the risks of infinite loops in user-facing applications?
   - How do you handle edge cases in loop conditions?

3. Code Clarity and Maintainability:
   - How do you balance complex logic with readable code?
   - When should you break complex conditions into separate variables?
   - How do commenting and naming conventions help with control flow?

#### Extension Challenge:

Advanced Control Flow Applications:

1. Interactive Menu System:
   - Design a multi-level menu system with sub-menus
   - Implement input validation and error recovery
   - Add features like "go back" and "main menu"

2. Data Validation Pipeline:
   - Create a system that validates user input through multiple checks
   - Implement different validation rules for different data types
   - Design error reporting that guides users to correct input

3. Game Logic Implementation:
   - Design turn-based game logic with multiple players
   - Implement win condition checking
   - Add replay functionality and score tracking

This exercise demonstrates how control flow structures form the logical backbone of interactive applications, enabling programs to respond dynamically to user input and changing conditions while maintaining predictable and reliable behavior.

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
