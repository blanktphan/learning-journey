# 📖 Object-Oriented Programming

## 💡 Basic knowledge required:

Understanding the limitations of procedural programming, especially the issue of data and functions being separated (from lesson 5.1)

## 🎯 Learning Objectives

Upon completion of this topic, you will be able to:

- Define OOP as a paradigm that focuses on "objects" which encapsulate data and behavior together
- Define and distinguish between "class" (blueprint) and "object" (instance)
- Explain the four fundamental principles of OOP: Encapsulation, Abstraction, Inheritance, and Polymorphism
- Analyze how OOP addresses the deficiencies of procedural programming

---

## 1. Paradigm Shift: From "Verbs" to "Nouns"

While procedural programming focuses on "actions" or "procedures" (verbs), Object-Oriented Programming (OOP) shifts the perspective to modeling the real world by focusing on "objects" which are like "nouns."

Instead of having scattered data and separated functions, OOP "encapsulates" data (attributes) and behavior (methods) that work with that data together into a single unit called an "object."

### Conceptual Transformation

```
Programming Paradigm Comparison
===============================

Procedural Programming (Verb-Focused):
┌─────────────────────────────────────────┐
│ Global Data:                            │
│ • accountBalance = 1000                 │
│ • accountNumber = "12345"               │
│ • ownerName = "John Doe"                │
│                                         │
│ Procedures (Actions):                   │
│ • withdraw(amount)                      │
│ • deposit(amount)                       │
│ • checkBalance()                        │
│ • printStatement()                      │
│                                         │
│ Problems:                               │
│ • Data exposed globally                 │
│ • Functions can modify any data         │
│ • No logical grouping                   │
│ • Difficult to manage multiple accounts │
└─────────────────────────────────────────┘

Object-Oriented Programming (Noun-Focused):
┌─────────────────────────────────────────┐
│ BankAccount Object:                     │
│ ┌─────────────────────────────────────┐ │
│ │ Data (Attributes):                  │ │
│ │ • balance = 1000                    │ │
│ │ • accountNumber = "12345"           │ │
│ │ • ownerName = "John Doe"            │ │
│ │                                     │ │
│ │ Behavior (Methods):                 │ │
│ │ • withdraw(amount)                  │ │
│ │ • deposit(amount)                   │ │
│ │ • getBalance()                      │ │
│ │ • printStatement()                  │ │
│ └─────────────────────────────────────┘ │
│                                         │
│ Benefits:                               │
│ • Data and behavior grouped together    │
│ • Controlled access to data             │
│ • Natural real-world modeling           │
│ • Easy to create multiple accounts      │
└─────────────────────────────────────────┘

Real-World Modeling Philosophy:
┌─────────────────────────────────────────┐
│ Physical World → Object Model           │
│                                         │
│ Car in Real Life:                       │
│ • Has properties: color, speed, fuel    │
│ • Has capabilities: accelerate, brake   │
│ • Self-contained unit                   │
│                                         │
│ Car Object in Code:                     │
│ • Attributes: color, speed, fuelLevel   │
│ • Methods: accelerate(), brake()        │
│ • Encapsulated entity                   │
│                                         │
│ Thinking Process:                       │
│ • What things exist in this problem?    │
│ • What properties do they have?         │
│ • What can they do?                     │
│ • How do they interact?                 │
└─────────────────────────────────────────┘
```

## 2. Classes and Objects: Blueprints and Products

### Understanding the Relationship

**Class**: A "blueprint" or "template" used to create objects. It defines what attributes and methods objects of that type will have. A class has no physical existence in memory.

**Object**: An "instance" or "actual entity" created from a class. Each object has its own set of attribute values and is stored in memory.

```
Class vs Object Relationship
============================

Blueprint Analogy:
┌─────────────────────────────────────────┐
│ House Blueprint (Class):                │
│ ┌─────────────────────────────────────┐ │
│ │ Specifications:                     │ │
│ │ • numberOfRooms                     │ │
│ │ • squareFootage                     │ │
│ │ • color                             │ │
│ │                                     │ │
│ │ Capabilities:                       │ │
│ │ • openDoor()                        │ │
│ │ • turnOnLights()                    │ │
│ │ • adjustTemperature()               │ │
│ └─────────────────────────────────────┘ │
│                                         │
│ Actual Houses (Objects):                │
│ ┌─────────────┐ ┌─────────────┐         │
│ │ House #1    │ │ House #2    │         │
│ │ rooms: 3    │ │ rooms: 4    │         │
│ │ sqft: 1200  │ │ sqft: 1800  │         │
│ │ color: blue │ │ color: red  │         │
│ └─────────────┘ └─────────────┘         │
│                                         │
│ Key Points:                             │
│ • One blueprint, many houses            │
│ • Each house has unique property values │
│ • All houses can perform same actions   │
│ • Blueprint exists only on paper        │
│ • Houses exist in physical world        │
└─────────────────────────────────────────┘

Car Example Implementation:
┌─────────────────────────────────────────┐
│ CLASS Car                               │
│     ATTRIBUTES:                         │
│         color                           │
│         speed                           │
│         fuelLevel                       │
│                                         │
│     METHODS:                            │
│         accelerate()                    │
│         brake()                         │
│         refuel()                        │
│         getCurrentSpeed()               │
│ END CLASS                               │
│                                         │
│ Creating Objects from Class:            │
│ myCar = new Car()                       │
│ myCar.color = "red"                     │
│ myCar.speed = 0                         │
│ myCar.fuelLevel = 50                    │
│                                         │
│ friendsCar = new Car()                  │
│ friendsCar.color = "blue"               │
│ friendsCar.speed = 0                    │
│ friendsCar.fuelLevel = 75               │
│                                         │
│ Both objects can:                       │
│ myCar.accelerate()                      │
│ friendsCar.accelerate()                 │
│                                         │
│ But they maintain separate state:       │
│ myCar.speed might be 60                 │
│ friendsCar.speed might be 45            │
└─────────────────────────────────────────┘

Memory Representation:
┌─────────────────────────────────────────┐
│ Class Car (in code, not memory):        │
│ • Template definition                   │
│ • Method implementations                │
│ • Attribute specifications              │
│                                         │
│ Object myCar (in memory):               │
│ Memory Address: 0x1000                  │
│ • color: "red"                          │
│ • speed: 60                             │
│ • fuelLevel: 45                         │
│                                         │
│ Object friendsCar (in memory):          │
│ Memory Address: 0x2000                  │
│ • color: "blue"                         │
│ • speed: 45                             │
│ • fuelLevel: 70                         │
│                                         │
│ Each object is independent but follows  │
│ the same blueprint (class definition)   │
└─────────────────────────────────────────┘
```

## 3. The Four Pillars of OOP

### A. Encapsulation

**Definition**: The bundling of data (attributes) and methods that work with that data into a single object, including "hiding" internal implementation details and preventing external code from directly modifying data.

```
Encapsulation in Practice
=========================

Car Engine Analogy:
┌─────────────────────────────────────────┐
│ External Interface (Public):            │
│ ┌─────────────────────────────────────┐ │
│ │ Gas Pedal → accelerate()            │ │
│ │ Brake Pedal → brake()               │ │
│ │ Steering Wheel → turn()             │ │
│ │ Speedometer → getCurrentSpeed()     │ │
│ └─────────────────────────────────────┘ │
│                                         │
│ Internal Implementation (Private):      │
│ ┌─────────────────────────────────────┐ │
│ │ • Fuel injection system             │ │
│ │ • Transmission mechanics            │ │
│ │ • Engine timing control             │ │
│ │ • Hydraulic brake system            │ │
│ │ (Hidden from driver)                │ │
│ └─────────────────────────────────────┘ │
│                                         │
│ Benefits:                               │
│ • Driver doesn't need engine expertise  │
│ • Internal changes don't affect driver  │
│ • Safety through controlled access      │
│ • Simplified user experience            │
└─────────────────────────────────────────┘

Code Implementation Example:
┌─────────────────────────────────────────┐
│ CLASS BankAccount                       │
│     PRIVATE ATTRIBUTES:                 │
│         balance                         │
│         accountNumber                   │
│         pin                             │
│                                         │
│     PUBLIC METHODS:                     │
│         deposit(amount)                 │
│             IF amount > 0 THEN          │
│                 balance = balance + amount
│                 RETURN true             │
│             ELSE                        │
│                 RETURN false            │
│             END IF                      │
│                                         │
│         withdraw(amount, userPin)       │
│             IF validatePin(userPin) AND amount <= balance THEN
│                 balance = balance - amount
│                 RETURN true             │
│             ELSE                        │
│                 RETURN false            │
│             END IF                      │
│                                         │
│         getBalance(userPin)             │
│             IF validatePin(userPin) THEN│
│                 RETURN balance          │
│             ELSE                        │
│                 RETURN "Access Denied"  │
│             END IF                      │
│                                         │
│     PRIVATE METHODS:                    │
│         validatePin(userPin)            │
│             RETURN userPin == pin       │
│ END CLASS                               │
│                                         │
│ Usage (External Code):                  │
│ account = new BankAccount()             │
│ account.deposit(100)        // Allowed  │
│ account.withdraw(50, "1234") // Allowed │
│ account.balance = 1000000   // NOT ALLOWED!
│ account.pin = "0000"        // NOT ALLOWED!
│                                         │
│ Encapsulation Benefits:                 │
│ • Data integrity protection             │
│ • Controlled access mechanisms          │
│ • Implementation flexibility            │
│ • Error prevention                      │
└─────────────────────────────────────────┘
```

### B. Abstraction

**Definition**: The result of good encapsulation. It hides implementation complexity and shows only the essential functionality needed by users.

```
Abstraction Levels
==================

Steering Wheel Abstraction:
┌─────────────────────────────────────────┐
│ User Interface (Abstract):              │
│ ┌─────────────────────────────────────┐ │
│ │ "Turn steering wheel left/right"    │ │
│ │ Simple, intuitive action            │ │
│ └─────────────────────────────────────┘ │
│                                         │
│ Hidden Complexity (Concrete):           │
│ ┌─────────────────────────────────────┐ │
│ │ • Steering column rotation          │ │
│ │ • Rack and pinion mechanism         │ │
│ │ • Tie rod connections               │ │
│ │ • Wheel alignment calculations      │ │
│ │ • Power steering fluid pressure     │ │
│ │ • Electronic steering assistance    │ │
│ └─────────────────────────────────────┘ │
│                                         │
│ Abstraction Benefits:                   │
│ • User focuses on what, not how         │
│ • Complexity managed internally         │
│ • Interface remains stable              │
│ • Implementation can change freely      │
└─────────────────────────────────────────┘

Software Abstraction Example:
┌─────────────────────────────────────────┐
│ Email Service Abstraction:              │
│                                         │
│ Public Interface:                       │
│ ┌─────────────────────────────────────┐ │
│ │ sendEmail(recipient, subject, body) │ │
│ │ • Simple method call                │ │
│ │ • Clear purpose                     │ │
│ │ • Easy to use                       │ │
│ └─────────────────────────────────────┘ │
│                                         │
│ Hidden Implementation:                  │
│ ┌─────────────────────────────────────┐ │
│ │ • SMTP protocol handling            │ │
│ │ • Server authentication             │ │
│ │ • Message formatting (MIME)         │ │
│ │ • Attachment encoding               │ │
│ │ • Error handling and retries        │ │
│ │ • Security and encryption           │ │
│ │ • Delivery status tracking          │ │
│ └─────────────────────────────────────┘ │
│                                         │
│ Usage:                                  │
│ emailService.sendEmail(                 │
│     "friend@example.com",               │
│     "Hello",                            │
│     "How are you?"                      │
│ )                                       │
│                                         │
│ User doesn't need to know:              │
│ • How SMTP works                        │
│ • Email server configurations           │
│ • Network protocols                     │
│ • Error recovery mechanisms             │
└─────────────────────────────────────────┘

Abstraction Design Principles:
┌─────────────────────────────────────────┐
│ Good Abstraction Characteristics:       │
│ • Hides unnecessary complexity          │
│ • Provides clear, intuitive interface   │
│ • Remains stable over time              │
│ • Allows implementation changes         │
│ • Focuses on essential features         │
│                                         │
│ Abstraction Layers Example:             │
│ ┌─────────────────────────────────────┐ │
│ │ User Application                    │ │
│ │         ↓                           │ │
│ │ High-Level API                      │ │
│ │         ↓                           │ │
│ │ Service Layer                       │ │
│ │         ↓                           │ │
│ │ Data Access Layer                   │ │
│ │         ↓                           │ │
│ │ Database                            │ │
│ └─────────────────────────────────────┘ │
│                                         │
│ Each layer abstracts complexity from    │
│ the layer above it                      │
└─────────────────────────────────────────┘
```

### C. Inheritance

**Definition**: A mechanism that allows a new class (subclass or child class) to acquire all properties and capabilities from an existing class (superclass or parent class).

**Purpose**: To promote code reusability and create class hierarchies with "is-a" relationships.

```
Inheritance Hierarchy
=====================

Vehicle Inheritance Example:
┌─────────────────────────────────────────┐
│                Vehicle                  │
│            (Parent Class)               │
│ ┌─────────────────────────────────────┐ │
│ │ Attributes:                         │ │
│ │ • speed                             │ │
│ │ • color                             │ │
│ │ • manufacturer                      │ │
│ │                                     │ │
│ │ Methods:                            │ │
│ │ • start()                           │ │
│ │ • stop()                            │ │
│ │ • accelerate()                      │ │
│ │ • getSpeed()                        │ │
│ └─────────────────────────────────────┘ │
│                    ↓                    │
│          ┌─────────┴─────────┐          │
│          ↓                   ↓          │
│    ┌─────────┐         ┌─────────┐      │
│    │   Car   │         │  Boat   │      │
│    │(Child)  │         │(Child)  │      │
│    └─────────┘         └─────────┘      │
│          ↓                   ↓          │
│ ┌─────────────────┐ ┌─────────────────┐ │
│ │ Inherits from   │ │ Inherits from   │ │
│ │ Vehicle:        │ │ Vehicle:        │ │
│ │ • speed         │ │ • speed         │ │
│ │ • color         │ │ • color         │ │
│ │ • start()       │ │ • start()       │ │
│ │ • accelerate()  │ │ • accelerate()  │ │
│ │                 │ │                 │ │
│ │ Adds:           │ │ Adds:           │ │
│ │ • numWheels     │ │ • displacement  │ │
│ │ • fuelType      │ │ • anchor()      │ │
│ │ • honk()        │ │ • sail()        │ │
│ └─────────────────┘ └─────────────────┘ │
└─────────────────────────────────────────┘

Specialized Inheritance:
┌─────────────────────────────────────────┐
│              Car                        │
│         (Parent Class)                  │
│ ┌─────────────────────────────────────┐ │
│ │ All Vehicle attributes + methods    │ │
│ │ Plus:                               │ │
│ │ • numWheels                         │ │
│ │ • fuelType                          │ │
│ │ • honk()                            │ │
│ │ • openTrunk()                       │ │
│ └─────────────────────────────────────┘ │
│                    ↓                    │
│          ┌─────────┴─────────┐          │
│          ↓                   ↓          |
│   ┌─────────────┐     ┌─────────────┐   │
│   │ElectricCar  │     │ SportsCar   │   │
│   │  (Child)    │     │  (Child)    │   │
│   └─────────────┘     └─────────────┘   │
│          ↓                   ↓          │
│ ┌─────────────────┐ ┌─────────────────┐ │
│ │ Inherits from   │ │ Inherits from   │ │
│ │ Car:            │ │ Car:            │ │
│ │ • All Vehicle   │ │ • All Vehicle   │ │
│ │   features      │ │   features      │ │
│ │ • All Car       │ │ • All Car       │ │
│ │   features      │ │   features      │ │
│ │                 │ │                 │ │
│ │ Adds:           │ │ Adds:           │ │
│ │ • batteryLevel  │ │ • turboMode     │ │
│ │ • charge()      │ │ • activateTurbo() │
│ │ • plugIn()      │ │ • shiftGear()   │ │
│ └─────────────────┘ └─────────────────┘ │
└─────────────────────────────────────────┘

Implementation Example:
┌─────────────────────────────────────────┐
│ CLASS Vehicle                           │
│     ATTRIBUTES:                         │
│         speed = 0                       │
│         color                           │
│         manufacturer                    │
│                                         │
│     METHODS:                            │
│         start()                         │
│             PRINT "Vehicle started"     │
│                                         │
│         accelerate()                    │
│             speed = speed + 10          │
│                                         │
│         getSpeed()                      │
│             RETURN speed                │
│ END CLASS                               │
│                                         │
│ CLASS ElectricCar EXTENDS Vehicle       │
│     ATTRIBUTES:                         │
│         batteryLevel = 100              │
│         // Inherits: speed, color, manufacturer
│                                         │
│     METHODS:                            │
│         charge()                        │
│             batteryLevel = 100          │
│             PRINT "Battery charged"     │
│                                         │
│         accelerate() // Override        │
│             IF batteryLevel > 0 THEN    │
│                 speed = speed + 15      │
│                 batteryLevel = batteryLevel - 1
│             ELSE                        │
│                 PRINT "Battery empty"   │
│             END IF                      │
│         // Inherits: start(), getSpeed()
│ END CLASS                               │
│                                         │
│ Usage:                                  │
│ myElectricCar = new ElectricCar()       │
│ myElectricCar.color = "white"           │
│ myElectricCar.start()      // From Vehicle
│ myElectricCar.accelerate() // Overridden│
│ myElectricCar.charge()     // New method│
└─────────────────────────────────────────┘
```

### D. Polymorphism

**Definition**: From Greek "Poly" (many) and "Morph" (forms), meaning "having many forms." It's the ability of objects of different types to respond to the "same method name" with different behaviors according to their specific type.

**Purpose**: To create flexible and extensible programs.

```
Polymorphism in Action
======================

Vehicle Movement Example:
┌─────────────────────────────────────────┐
│ Same Method, Different Behaviors:       │
│                                         │
│ Car.move() → "Wheels rolling on road"   │
│ Boat.move() → "Propeller spinning in water"
│ Plane.move() → "Jet engines thrusting"  │
│ Bicycle.move() → "Pedals turning wheels"│
│                                         │
│ Polymorphic Usage:                      │
│ vehicles = [car, boat, plane, bicycle]  │
│ FOR each vehicle IN vehicles DO         │
│     vehicle.move()  // Each responds differently
│ END FOR                                 │
│                                         │
│ Benefits:                               │
│ • Single interface for multiple types   │
│ • Easy to add new vehicle types         │
│ • Code that works with any vehicle      │
│ • Flexible and extensible design        │
└─────────────────────────────────────────┘

Shape Drawing Example:
┌─────────────────────────────────────────┐
│ CLASS Shape                             │
│     METHODS:                            │
│         draw()  // Abstract method      │
│             PRINT "Drawing a shape"     │
│                                         │
│         area()  // Abstract method      │
│             RETURN 0                    │
│ END CLASS                               │
│                                         │
│ CLASS Circle EXTENDS Shape              │
│     ATTRIBUTES:                         │
│         radius                          │
│                                         │
│     METHODS:                            │
│         draw()  // Override             │
│             PRINT "Drawing a circle with radius", radius
│                                         │
│         area()  // Override             │
│             RETURN 3.14159 * radius * radius
│ END CLASS                               │
│                                         │
│ CLASS Rectangle EXTENDS Shape           │
│     ATTRIBUTES:                         │
│         width, height                   │
│                                         │
│     METHODS:                            │
│         draw()  // Override             │
│             PRINT "Drawing rectangle", width, "x", height
│                                         │
│         area()  // Override             │
│             RETURN width * height       │
│ END CLASS                               │
│                                         │
│ CLASS Triangle EXTENDS Shape            │
│     ATTRIBUTES:                         │
│         base, height                    │
│                                         │
│     METHODS:                            │
│         draw()  // Override             │
│             PRINT "Drawing triangle base:", base
│                                         │
│         area()  // Override             │
│             RETURN 0.5 * base * height  │
│ END CLASS                               │
└─────────────────────────────────────────┘

Polymorphic Processing:
┌─────────────────────────────────────────┐
│ // Creating different shape objects     │
│ circle = new Circle()                   │
│ circle.radius = 5                       │
│                                         │
│ rectangle = new Rectangle()             │
│ rectangle.width = 10                    │
│ rectangle.height = 6                    │
│                                         │
│ triangle = new Triangle()               │
│ triangle.base = 8                       │
│ triangle.height = 4                     │
│                                         │
│ // Polymorphic collection               │
│ shapes = [circle, rectangle, triangle]  │
│                                         │
│ // Same code works for all shapes       │
│ totalArea = 0                           │
│ FOR each shape IN shapes DO             │
│     shape.draw()     // Calls appropriate version
│     totalArea = totalArea + shape.area() // Calls appropriate version
│ END FOR                                 │
│                                         │
│ PRINT "Total area of all shapes:", totalArea
│                                         │
│ Output:                                 │
│ Drawing a circle with radius 5          │
│ Drawing rectangle 10 x 6                │
│ Drawing triangle base: 8                │
│ Total area of all shapes: 163.54        │
│                                         │
│ Key Benefits:                           │
│ • Code works with current AND future shapes
│ • Adding new shapes doesn't break existing code
│ • Uniform interface for different implementations
│ • Runtime method resolution             │
└─────────────────────────────────────────┘

Real-World Application:
┌─────────────────────────────────────────┐
│ Media Player Example:                   │
│                                         │
│ AudioFile.play() → "Playing audio"      │
│ VideoFile.play() → "Playing video"      │
│ ImageFile.play() → "Displaying image"   │
│                                         │
│ Playlist Processing:                    │
│ files = [song.mp3, movie.mp4, photo.jpg]│
│ FOR each file IN files DO               │
│     file.play()  // Appropriate behavior│
│ END FOR                                 │
│                                         │
│ Benefits:                               │
│ • Media player doesn't need to know file types
│ • Easy to add new media formats         │
│ • Consistent user interface             │
│ • Extensible architecture               │
└─────────────────────────────────────────┘
```

---

## 💡 How OOP Solves Procedural Programming Problems

### Problem Resolution Analysis

```
Procedural vs OOP Problem Solutions
===================================

Problem 1: Data Exposure and Modification
┌─────────────────────────────────────────┐
│ Procedural Problem:                     │
│ • Global variables accessible everywhere│
│ • Any function can modify any data      │
│ • Accidental data corruption            │
│ • Difficult to trace data changes       │
│                                         │
│ OOP Solution: Encapsulation             │
│ • Data hidden inside objects            │
│ • Controlled access through methods     │
│ • Data integrity protection             │
│ • Clear ownership and responsibility    │
│                                         │
│ Example:                                │
│ Procedural: accountBalance = 0 (global) │
│ OOP: account.withdraw(amount) (controlled)
└─────────────────────────────────────────┘

Problem 2: Code Organization and Reusability
┌─────────────────────────────────────────┐
│ Procedural Problem:                     │
│ • Functions scattered across files      │
│ • No logical grouping                   │
│ • Difficult code reuse                  │
│ • Copy-paste programming                │
│                                         │
│ OOP Solution: Classes and Inheritance   │
│ • Related data and functions grouped    │
│ • Clear organizational structure        │
│ • Code reuse through inheritance        │
│ • Extensible design patterns            │
│                                         │
│ Example:                                │
│ Procedural: Many banking functions      │
│ OOP: BankAccount class with methods     │
└─────────────────────────────────────────┘

Problem 3: Complexity Management
┌─────────────────────────────────────────┐
│ Procedural Problem:                     │
│ • Spaghetti code with complex dependencies
│ • Difficult to understand large systems │
│ • Changes affect multiple areas         │
│ • Hard to test individual components    │
│                                         │
│ OOP Solution: Abstraction and Modularity│
│ • Clear interfaces between components   │
│ • Hidden implementation details         │
│ • Independent object testing            │
│ • Modular system architecture           │
│                                         │
│ Example:                                │
│ Procedural: Complex function interactions
│ OOP: Objects with clear responsibilities│
└─────────────────────────────────────────┘

Problem 4: Flexibility and Extensibility
┌─────────────────────────────────────────┐
│ Procedural Problem:                     │
│ • Adding features requires code changes │
│ • Difficult to support multiple variants│
│ • Tight coupling between components     │
│ • Brittle system architecture           │
│                                         │
│ OOP Solution: Polymorphism and Inheritance
│ • New features through new classes      │
│ • Multiple implementations of interfaces│
│ • Loose coupling through abstraction    │
│ • Extensible and maintainable design    │
│                                         │
│ Example:                                │
│ Procedural: if-else chains for types    │
│ OOP: Polymorphic method calls           │
└─────────────────────────────────────────┘
```

### Banking System Transformation

```
Complete System Comparison
==========================

Procedural Banking System:
┌─────────────────────────────────────────┐
│ // Global state                         │
│ account1_balance = 1000                 │
│ account1_number = "12345"               │
│ account1_owner = "John"                 │
│                                         │
│ account2_balance = 500                  │
│ account2_number = "67890"               │
│ account2_owner = "Jane"                 │
│                                         │
│ PROCEDURE withdraw_account1(amount)     │
│     IF account1_balance >= amount THEN  │
│         account1_balance = account1_balance - amount
│     END IF                              │
│ END                                     │
│                                         │
│ PROCEDURE withdraw_account2(amount)     │
│     IF account2_balance >= amount THEN  │
│         account2_balance = account2_balance - amount
│     END IF                              │
│ END                                     │
│                                         │
│ Problems:                               │
│ • Duplicate code for each account       │
│ • Global variables can be modified anywhere
│ • Adding accounts requires new variables│
│ • No data protection                    │
└─────────────────────────────────────────┘

OOP Banking System:
┌─────────────────────────────────────────┐
│ CLASS BankAccount                       │
│     PRIVATE ATTRIBUTES:                 │
│         balance                         │
│         accountNumber                   │
│         ownerName                       │
│                                         │
│     PUBLIC METHODS:                     │
│         constructor(number, owner, initialBalance)
│             accountNumber = number      │
│             ownerName = owner           │
│             balance = initialBalance    │
│                                         │
│         withdraw(amount)                │
│             IF amount > 0 AND amount <= balance THEN
│                 balance = balance - amount
│                 RETURN true             │
│             ELSE                        │
│                 RETURN false            │
│             END IF                      │
│                                         │
│         deposit(amount)                 │
│             IF amount > 0 THEN          │
│                 balance = balance + amount
│                 RETURN true             │
│             ELSE                        │
│                 RETURN false            │
│             END IF                      │
│                                         │
│         getBalance()                    │
│             RETURN balance              │
│                                         │
│         getAccountInfo()                │
│             RETURN "Account: " + accountNumber + 
│                    ", Owner: " + ownerName +
│                    ", Balance: " + balance
│ END CLASS                               │
│                                         │
│ Usage:                                  │
│ account1 = new BankAccount("12345", "John", 1000)
│ account2 = new BankAccount("67890", "Jane", 500)
│                                         │
│ account1.withdraw(200)                  │
│ account2.deposit(100)                   │
│                                         │
│ Benefits:                               │
│ • No code duplication                   │
│ • Protected data access                 │
│ • Easy to create new accounts           │
│ • Clear object boundaries               │
│ • Reusable and maintainable code        │
└─────────────────────────────────────────┘
```

---

## 📋 Summary & Practical Exercise

### Comprehensive Summary

Object-Oriented Programming represents a paradigm shift from action-focused procedural programming to entity-focused modeling. OOP organizes code around objects that encapsulate both data and behavior, addressing key limitations of procedural programming through four fundamental principles.

The four pillars of OOP provide comprehensive solutions:
- Encapsulation bundles data and methods while protecting internal state
- Abstraction hides complexity and provides clear interfaces
- Inheritance enables code reuse and hierarchical relationships
- Polymorphism allows flexible behavior through uniform interfaces

Classes serve as blueprints for creating objects, with each object maintaining its own state while sharing common behavior. This approach enables better data protection, code organization, reusability, and system extensibility compared to procedural programming.

OOP's strength lies in modeling real-world entities and relationships, making complex systems more manageable and maintainable through proper abstraction and encapsulation.

### Practical Exercise

Apply OOP principles to design a comprehensive banking system using the example mentioned in the lesson conclusion.

#### Exercise Steps:

**Scenario**: Design a complete BankAccount class that demonstrates all four OOP principles.

```
BankAccount Class Design Challenge
==================================

Step 1: Class Structure Definition
┌─────────────────────────────────────────┐
│ Design a BankAccount class with:        │
│                                         │
│ Required Attributes:                    │
│ • Account number                        │
│ • Owner name                            │
│ • Current balance                       │
│ • Account type (checking/savings)       │
│ • Transaction history                   │
│                                         │
│ Your attribute list:                    │
│ 1. ___________________________________  │
│ 2. ___________________________________  │
│ 3. ___________________________________  │
│ 4. ___________________________________  │
│ 5. ___________________________________  │
│                                         │
│ Required Methods:                       │
│ • deposit(amount)                       │
│ • withdraw(amount)                      │
│ • getBalance()                          │
│ • getTransactionHistory()               │
│ • transferTo(otherAccount, amount)      │
│                                         │
│ Your method list:                       │
│ 1. ___________________________________  │
│ 2. ___________________________________  │
│ 3. ___________________________________  │
│ 4. ___________________________________  │
│ 5. ___________________________________  │
└─────────────────────────────────────────┘

Step 2: Encapsulation Analysis
┌─────────────────────────────────────────┐
│ Identify access levels for your design: │
│                                         │
│ Private (Hidden from outside):          │
│ • Which attributes should be private?   │
│   _____________________________________ │
│   _____________________________________ │
│ • Which methods should be private?      │
│   _____________________________________ │
│   _____________________________________ │
│                                         │
│ Public (Available to users):            │
│ • Which methods should be public?       │
│   _____________________________________ │
│   _____________________________________ │
│                                         │
│ Encapsulation Benefits Question:        │
│ Why can't external code directly modify │
│ the balance? What OOP principle does    │
│ this demonstrate?                       │
│                                         │
│ Your answer: __________________________ │
│ ______________________________________  │
│ ______________________________________  │
└─────────────────────────────────────────┘
```

#### Analysis Questions:

1. **Four Pillars Application**:
   - How does your BankAccount design demonstrate Encapsulation?
   - What aspects of banking complexity does your class abstract away?
   - How could you use Inheritance to create different account types?
   - Where would Polymorphism be useful in a banking system?

2. **Real-World Modeling**:
   - How does your object design reflect real bank account behavior?
   - What real-world constraints did you incorporate into your methods?
   - How does OOP make the banking system more intuitive than procedural code?

3. **Comparison with Procedural Approach**:
   - How would this system look in procedural programming?
   - What problems would arise with multiple accounts in procedural style?
   - Why is OOP better suited for this type of system?

#### Implementation Challenge:

```
Complete Implementation
=======================

Implement Your BankAccount Class:
┌─────────────────────────────────────────┐
│ CLASS BankAccount                       │
│                                         │
│     PRIVATE ATTRIBUTES:                 │
│     [Fill in your private attributes]   │
│                                         │
│     PUBLIC METHODS:                     │
│     constructor(parameters)             │
│         [Your initialization code]      │
│                                         │
│     deposit(amount)                     │
│         [Your implementation]           │
│                                         │
│     withdraw(amount)                    │
│         [Your implementation]           │
│                                         │
│     getBalance()                        │
│         [Your implementation]           │
│                                         │
│     [Additional methods]                │
│                                         │
│     PRIVATE METHODS:                    │
│     [Helper methods if needed]          │
│                                         │
│ END CLASS                               │
│                                         │
│ Test Your Implementation:               │
│ account1 = new BankAccount(...)         │
│ account2 = new BankAccount(...)         │
│                                         │
│ [Write test cases for all methods]      │
└─────────────────────────────────────────┘

Inheritance Extension:
┌─────────────────────────────────────────┐
│ Design specialized account types:       │
│                                         │
│ CLASS SavingsAccount EXTENDS BankAccount│
│     Additional features:                │
│     • Interest rate                     │
│     • Interest calculation              │
│     • Withdrawal limits                 │
│                                         │
│ CLASS CheckingAccount EXTENDS BankAccount
│     Additional features:                │
│     • Overdraft limit                   │
│     • Check writing capability          │
│     • Transaction fees                  │
│                                         │
│ How do these demonstrate inheritance?   │
│ ______________________________________  │
│ ______________________________________  │
└─────────────────────────────────────────┘

Polymorphism Demonstration:
┌─────────────────────────────────────────┐
│ Create a polymorphic banking system:    │
│                                         │
│ accounts = [                            │
│     new SavingsAccount(...),            │
│     new CheckingAccount(...),           │
│     new BankAccount(...)                │
│ ]                                       │
│                                         │
│ FOR each account IN accounts DO         │
│     account.deposit(100)                │
│     account.withdraw(50)                │
│     PRINT account.getBalance()          │
│ END FOR                                 │
│                                         │
│ How does this demonstrate polymorphism? │
│ ______________________________________  │
│ ______________________________________  │
└─────────────────────────────────────────┘
```

#### Extension Challenge:

**Advanced OOP Banking System**:

1. **Multi-Class System Design**:
   - Design Bank class that manages multiple accounts
   - Create Customer class with personal information
   - Implement Transaction class for detailed history
   - Show how objects collaborate

2. **Design Pattern Application**:
   - Research and apply the Observer pattern for account notifications
   - Implement Strategy pattern for different interest calculation methods
   - Use Factory pattern for creating different account types

3. **Real-World Integration**:
   - Design interfaces for ATM systems
   - Plan integration with external payment systems
   - Consider security and authentication mechanisms
   - Address concurrent access scenarios

This exercise demonstrates how OOP principles work together to create robust, maintainable, and extensible software systems that closely model real-world entities and relationships.

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.