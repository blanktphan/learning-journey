# 📖 Topic: Operators

## 💡 Basic knowledge required

- An understanding of Variables and Data Types (from Lesson 3.1).

## 🎯 Learning Objectives

- Define "operator" as a symbol that acts on data (operands).
- Identify and classify the main types of operators (Arithmetic, Assignment, Comparison, Logical).
- Understand the concepts of Precedence and Associativity for evaluating complex expressions.

---

### 1. Introduction to Operators

If variables are the "nouns" (the data) in a programming language, then **operators** are the "verbs" (the actions). An operator is a symbol used to perform mathematical, assignment, comparison, or logical operations on one or more pieces of data, which are called **operands**.

The combination of values, variables, and operators forms an **expression**, which can be evaluated to produce a single value.

```
      Operand    Operator   Operand
         |          |          |
         ▼          ▼          ▼
      (  x    +     5    )     *     2
      \__________________/
                 |
Expression (evaluates to a value)
```

### 2. Main Types of Operators

#### A. Arithmetic Operators
Used for performing basic mathematical calculations.

- `+` (Addition)
- `-` (Subtraction)
- `*` (Multiplication)
- `/` (Division)
- `%` (Modulo): Returns the remainder of a division.

```java
int score = 100 / 3;  // result is 33 (integer division)
int remainder = 100 % 3; // result is 1 (the remainder)
```

#### B. Assignment Operators
Used to assign values to variables.

- `=` (Basic Assignment): Assigns the value on the right to the variable on the left.
- `+=`, `-=`, `*=`, `/=`, `%=` (Compound Assignment): Performs a mathematical operation and assigns the result back to the original variable in one step.

```java
int level = 10;
level += 5; // Equivalent to: level = level + 5;
// level is now 15
```

#### C. Comparison / Relational Operators
Used to compare two values. The result is always a Boolean value (`true` or `false`).

- `==` (Equal to)
- `!=` (Not equal to)
- `>` (Greater than)
- `<` (Less than)
- `>=` (Greater than or equal to)
- `<=` (Less than or equal to)

```java
int userAge = 20;
boolean canVote = (userAge >= 18); // canVote will be true
```

#### D. Logical Operators
Used to combine two or more Boolean expressions or to invert a truth value.

- `&&` (AND): Result is `true` only if both expressions are `true`.
- `||` (OR): Result is `true` if at least one expression is `true`.
- `!` (NOT): Inverts the truth value (from `true` to `false`, and `false` to `true`).

```java
boolean hasKey = true;
boolean isAuthorized = false;
boolean canOpenDoor = hasKey && isAuthorized; // canOpenDoor will be false
```

### 3. Precedence and Associativity

To evaluate complex expressions like `a + b * c`, programming languages have clear rules to ensure a consistent result.

#### Precedence
This is the rule that defines which operators are evaluated first. It's similar to the order of operations in mathematics. Generally, `*`, `/`, and `%` have higher precedence than `+` and `-`.

`10 + 5 * 2` is evaluated as `10 + (5 * 2)`, resulting in `20`.

#### Associativity
This is the rule that defines the direction of evaluation for operators that have the same level of precedence.

- **Left-to-Right**: Most operators, like `+`, `-`, `*`, `/`, are evaluated from left to right.
  `100 - 10 + 5` is evaluated as `(100 - 10) + 5`, resulting in `95`.

- **Right-to-Left**: The assignment operator (`=`) is a clear example.
  `x = y = 5;` first assigns `5` to `y`, and then assigns the value of `y` (which is now 5) to `x`.

---

## 📋 Comprehensive Summary & Practical Exercise

### Comprehensive Summary

Operators are symbols that perform actions on data. They are classified into major types: arithmetic, assignment, comparison, and logical. The evaluation of complex expressions is controlled by clear rules of operator precedence and associativity.

### Practical Exercise

What is the final value of the following expression, and why?
(General Precedence Order: `()` > `!` > `* / %` > `+ -` > `> < >= <=` > `== !=` > `&&` > `||`)

```java
boolean result = (10 > 5) && !(7 == 7) || (10 % 3 == 1);
```

**Answer Breakdown:**
1.  Parentheses are evaluated first:
    - `(10 > 5)` becomes `true`.
    - `(7 == 7)` becomes `true`.
    - `(10 % 3 == 1)` becomes `(1 == 1)`, which is `true`.
2.  The expression is now: `true && !true || true`.
3.  `!` (NOT) has the next highest precedence: `!true` becomes `false`.
4.  The expression is now: `true && false || true`.
5.  `&&` (AND) has higher precedence than `||` (OR): `true && false` becomes `false`.
6.  The expression is now: `false || true`.
7.  Finally, `||` (OR) is evaluated: `false || true` becomes `true`.
8.  The final value of `result` is `true`.

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
