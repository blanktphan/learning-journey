# 📖 Topic: Software Testing

## 💡 Basic knowledge required

- An understanding of the concept of errors or bugs in programs (from lesson 6.4).

## 🎯 Learning Objectives

- Define "Software Testing" and its main goals in verification and validation.
- Differentiate between Manual and Automated testing.
- Explain the different levels of testing according to the Testing Pyramid (Unit, Integration, System Testing).
- Understand the concept of Test-Driven Development (TDD).

---

### 1. Introduction: The Discipline of Quality Assurance

Software Testing is a systematic process of evaluating and verifying whether a software or application works as it should. The goal of testing is not just to find bugs, but to build confidence in the quality of the software.

In software engineering, we divide this verification into two concepts:

-   Verification: Answers the question, "Are we building the product right?" (Does the software meet its technical specifications and design?)
-   Validation: Answers the question, "Are we building the right product?" (Does the software meet the actual needs of the user?)

```
+---------------------+ +---------------------+
|    Verification     | |     Validation      |
|---------------------| |---------------------|
| Building the        | | Building the        |
| product RIGHT       | | RIGHT product       |
| (Meets specs)       | | (Meets user needs)  |
+---------------------+ +---------------------+
```

Good testing is not a final step but an activity that should be integrated throughout the development lifecycle.

### 2. Testing Approaches: Manual vs. Automated

-   Manual Testing: A human tester interacts with the application according to a test plan to find defects. It is suitable for tasks requiring creativity, such as exploratory testing or usability evaluation.
-   Automated Testing: Uses software or scripts to run tests and compare results against expectations automatically. It is fast, repeatable, and reliable, making it essential for modern, high-speed software development.

### 3. Testing Levels: The Testing Pyramid

This is a concept for structuring automated tests to be efficient and cost-effective.

```
      /---------\
     /    E2E    \      (Few, Slow)
    /-------------\
   /  Integration  \    (Some, Medium)
  /-----------------\
 /       Unit        \  (Many, Fast)
+---------------------+
```

#### A. Unit Testing

-   Scope: Tests the "smallest unit" of code, such as a single function, in isolation. It forms the base of the pyramid and should be the most numerous type of test.
-   Goal: To verify that each piece of code works correctly on its own. These tests are very fast.

#### B. Integration Testing

-   Scope: Tests the interaction "between" multiple units or modules. This is the middle of the pyramid.
-   Goal: To find errors that occur at the "interfaces" or points of interaction between components.

#### C. End-to-End (E2E) Testing

-   Scope: Tests the "entire workflow" of an application from start to finish, from a user's perspective. This is the top of the pyramid and should be the least numerous.
-   Goal: To confirm that the system as a whole can meet business requirements. These tests are slow and expensive.

### 4. Test-Driven Development (TDD)

TDD is a software development methodology that reverses the traditional workflow, using a cycle called "Red-Green-Refactor":

```
+------------------+
| 1. Red           |
| (Write a failing |
|  test)           |
+------------------+
        |
        v
+------------------+
| 2. Green         |
| (Write minimal   |
|  code to pass)   |
+------------------+
        |
        v
+------------------+
| 3. Refactor      |
| (Improve the     |
|  code)           |
+------------------+
```

1.  Red: First, write an automated unit test for a new feature that does not yet exist. Naturally, this test will fail.
2.  Green: Write the absolute minimum amount of feature code necessary to make the failing test pass.
3.  Refactor: Improve the structure of the code you just wrote, making it cleaner and more efficient, while ensuring all tests still pass.

The benefit of TDD is that it guarantees every piece of code is covered by a test and forces the programmer to think clearly about requirements before writing code.

---

## 📋 Comprehensive Summary & Practical Exercise

### Comprehensive Summary

Software testing is a quality assurance discipline for systematically finding bugs. It includes various levels, from Unit to System testing, with automation being essential in the modern era. TDD is a methodology that uses tests to drive development.

### Practical Exercise

You are adding a "shopping cart" feature to an e-commerce website:
1.  Testing the `addItemToCart(item, quantity)` function by itself is what level of testing?
2.  Testing that when an item is added to the cart, the stock quantity in the database is correctly reduced is what level of testing?
3.  Testing a simulation of a user searching for a product, adding it to the cart, and completing the payment successfully is what level of testing?

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.