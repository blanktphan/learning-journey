# 📖 Topic: Object-Oriented Programming (OOP)

## 💡 Basic knowledge required

- An understanding of the limitations of procedural programming, especially the problem of separated data and functions (from lesson 5.1).

## 🎯 Learning Objectives

- Define OOP as a paradigm focused on "objects" that encapsulate data and behavior together.
- Define and differentiate between a "class" (blueprint) and an "object" (instance).
- Explain the four fundamental principles of OOP: Encapsulation, Abstraction, Inheritance, and Polymorphism.
- Analyze how OOP addresses the shortcomings of procedural programming.

---

### 1. The Paradigm Shift: From "Verbs" to "Nouns"

While procedural programming focuses on "actions" or "procedures" (verbs), Object-Oriented Programming (OOP) shifts the perspective to modeling the real world by focusing on "objects" (nouns).

Instead of having scattered data and separate functions, OOP **encapsulates** data (attributes) and the behaviors (methods) that operate on that data into a single unit called an "object."

### 2. Class and Object: The Blueprint and the Product

-   **Class**: A "blueprint" or "template" for creating objects. It is the code that defines the attributes and methods that an object of that type will have. A class itself does not exist in memory.
-   **Object**: An "instance" or "real entity" created from a class. Each object has its own set of attributes and is stored in memory.

**Analogy**:
-   A `Car` is a **class**. It's a blueprint specifying that a car must have a `color` and an `accelerate()` method.
-   "Mr. Smith's red Honda Civic" is an **object**. It is an instance created from the `Car` class, with its `color` attribute set to "red."

```
      +-----------------+
      |   Class: Car    |
      |-----------------|
      | Attributes:     |
      |   - color       |
      |   - model       |
      |-----------------|
      | Methods:        |
      |   - accelerate()|
      |   - brake()     |
      +-----------------+
              |
              | (is a blueprint for)
              v
+--------------------------+      +--------------------------+
| Object: myCar            |      | Object: yourCar          |
|--------------------------|      |--------------------------|
| color: "Red"             |      | color: "Blue"            |
| model: "Honda Civic"     |      | model: "Toyota Camry"    |
+--------------------------+      +--------------------------+
```

### 3. The Four Pillars of OOP

#### A. Encapsulation

-   **Definition**: The bundling of data (attributes) and the methods that operate on that data into a single object. It also includes "hiding" the internal implementation details and protecting data from direct external modification.
-   **Analogy**: A car's engine. All complex parts are "encapsulated" under the hood. The driver interacts with it through a simple "interface" like the accelerator pedal (`accelerate()`) without needing to know how the internal mechanics work.

#### B. Abstraction

-   **Definition**: A result of good encapsulation. It involves hiding complex implementation details and exposing only the necessary functionalities to the user.
-   **Analogy**: A "steering wheel" is an abstraction for directional control. We just turn it left or right without dealing with the complex mechanics of the steering column, control arms, or the power steering system.

#### C. Inheritance

-   **Definition**: A mechanism that allows a new class (subclass or child class) to acquire all the properties and behaviors of an existing class (superclass or parent class).
-   **Purpose**: To promote code reusability and create a hierarchy of classes with an "is-a" relationship.
-   **Analogy**: We can create an `ElectricCar` class that "inherits" from the `Car` class. The `ElectricCar` automatically gets the `accelerate()` method and `color` attribute, and then adds its own unique properties, like `battery_level`, and methods, like `charge()`.

#### D. Polymorphism

-   **Definition**: From the Greek words "Poly" (many) and "Morph" (form), it means "many forms." It is the ability of different objects to respond to the **same method call** in different, type-specific ways.
-   **Purpose**: To create flexible and extensible programs.
-   **Analogy**: Consider a `move()` method:
    -   When called on a `Car` object -> `move()` means "wheels spin."
    -   When called on a `Boat` object -> `move()` means "propeller turns."
    -   When called on a `Plane` object -> `move()` means "jet engine fires."
    We can command all vehicles to `move()` with a single command, but each type moves in its own way.

---

## 📋 Comprehensive Summary & Practical Exercise

### Comprehensive Summary

OOP is a paradigm that organizes code by modeling the real world through "objects," which encapsulate data and behavior. Its four main principles—Encapsulation, Abstraction, Inheritance, and Polymorphism—solve the complex state management problems of procedural programming.

### Practical Exercise

Try to design a "class" for a `BankAccount`.
1.  What "attributes" should this class have? (e.g., account number, owner's name, balance)
2.  What "methods" should it have? (e.g., `deposit()`, `withdraw()`)
3.  The fact that you cannot directly modify the "balance" but must go through the `deposit()` or `withdraw()` methods is an application of which OOP principle?

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
