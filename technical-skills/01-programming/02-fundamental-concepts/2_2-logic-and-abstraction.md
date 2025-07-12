# 📖 Topic: Logic and Abstraction

## 💡 Basic knowledge required

An understanding of Computational Thinking concepts (from lesson 2.1).

## 🎯 Learning Objectives

- To be able to define and explain the role of "logic" in creating clear program conditions.
- To be able to define and explain the role of "abstraction" in managing complexity.
- To understand the complementary relationship between logic and abstraction in software development.

---

### 1. Logic: The Foundation of Reasoning

In computer science, logic is a formal system for reasoning and drawing conclusions from existing assumptions. It is the "grammar" of decision-making in programs, based on Propositional Logic, where every condition has a truth value of either True or False.

Programmers constantly use logic through logical connectives:

-   **AND**: All conditions must be true for the result to be true.
-   **OR**: If any one condition is true, the result is true.
-   **NOT**: Reverses the truth value from true to false, and false to true.

Logic is what guarantees that a program will behave correctly and predictably according to the conditions we set. Every if-else statement or while loop is controlled by these logical rules.

### 2. Abstraction: The Art of Selective Ignorance

Abstraction is the intellectual process of filtering and "hiding" unnecessary details to focus on the essential aspects of a concept or system. It is the most powerful tool for managing complexity.

A great example is a subway map. It is an "abstraction" of a city. It hides all the details of buildings, streets, and alleys, showing only the information necessary for passengers: stations and connecting routes.

In programming, we use abstraction to create "black boxes" or APIs (Application Programming Interfaces) that other programmers can use without needing to know how the complex mechanisms inside work.

### 3. Synergy: Logic and Abstraction in Software Development

Logic and abstraction work together to build complex systems. We use logic to create small, correct components, and then use abstraction to wrap those components behind simple interfaces.

**Example: The "Pay" button on an E-commerce Website**

#### Logic (The Internal Mechanism)
When a user clicks the button, a complex set of logic is executed:
```
IF (user is logged in AND all items are in stock AND shipping address is valid) THEN
    Connect to payment system
    IF (credit card is approved) THEN
        Update inventory
        Send confirmation email
        Show "Order Successful" page
    ELSE
        Show "Payment Failed" page
    END IF
END IF
```

#### Abstraction (What Other Programmers See)
A programmer working on the website's user interface doesn't need to know all that logic. They might just call a single function prepared by the backend team:
```javascript
checkout();
```
The `checkout()` function is an abstraction that hides all the complex logic inside, making the overall system development simpler and more modular.

---

## 📋 Comprehensive Summary & Practical Exercise

### Comprehensive Summary

Logic provides the rules that guarantee the "correctness" of a program, while abstraction is the tool that helps "manage complexity." Modern software is built by layering abstractions on top of components that have been verified with correct logic.

### Practical Exercise

Consider an air conditioner.

-   Use **logic** to describe its operating conditions (e.g., IF room_temperature > set_temperature THEN the compressor turns on).
-   Use **abstraction** to describe which components "hide" complexity from the user (e.g., you just press a button on the remote control without needing to know how the internal circuitry works).
  
---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.