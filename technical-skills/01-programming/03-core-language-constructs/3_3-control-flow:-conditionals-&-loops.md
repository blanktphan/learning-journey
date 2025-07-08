# 📖 Control Flow: Conditionals & Loops

## 💡 Basic knowledge required:

Understanding of variables and especially comparison and logical operators that produce Boolean results (from Lessons 3.1-3.2)

## 🎯 Learning Objectives

Upon completion of this topic, you will be able to:

- Define "Control Flow" and explain its importance in creating programs that work non-linearly
- Understand and write conditional statements using if, else if, and else to create decision branches in program execution
- Understand and write loop statements using while and for to make code execute repeatedly
- Distinguish appropriate use cases for while loops versus for loops

---

## 1. Introduction to Control Flow

By default, computers process our programs sequentially - executing commands from the top line down to the bottom line, one command at a time. Control Flow is a set of statements in programming languages that allows us to change this execution order. It enables our programs to "make decisions" to skip certain parts of code or "go back" to repeat certain sets of commands multiple times. This is what makes programs intelligent and responsive to different situations.

```
Program Execution Flow:

Sequential Flow (Default):          Control Flow (Advanced):
┌─────────────────┐                ┌─────────────────┐
│ Step 1          │                │ Step 1          │
│       ↓         │                │       ↓         │
│ Step 2          │                │ Decision?       │
│       ↓         │                │    /     \      │
│ Step 3          │                │   /       \     │
│       ↓         │                │  ↓         ↓    │
│ Step 4          │                │ Step A   Step B │
│       ↓         │                │   \       /     │
│ End             │                │    \     /      │
└─────────────────┘                │     ↓   ↓       │
                                   │   Continue      │
                                   │     ↓           │
                                   │   Loop?         │
                                   │    / \          │
                                   │   /   \         │
                                   │  ↓     ↓        │
                                   │ Repeat  End     │
                                   │  ↑              │
                                   │  └──────┘       │
                                   └─────────────────┘
```

### Why Control Flow Matters

Without control flow, programs would be extremely limited:

```
Program Capability Comparison:

Without Control Flow:               With Control Flow:
┌─────────────────────────┐        ┌──────────────────────────┐
│ Linear & Rigid          │        │ Dynamic & Intelligent    │
│                         │        │                          │
│ ┌─ Get input            │        │ ┌─ Get input             │
│ │                       │        │ │  ↓                     │
│ ├─ Process              │        │ ├─ Valid? ──No──┐        │
│ │                       │        │ │  ↓ Yes         │       │
│ ├─ Display result       │        │ ├─ Process       │       │
│ │                       │        │ │  ↓             │       │
│ └─ End                  │        │ ├─ Display       │       │
│                         │        │ │  ↓             │       │
│ No flexibility          │        │ ├─ Continue?     │       │
│ Can't handle errors     │        │ │  ↓ Yes    No   │       │
│ No user interaction     │        │ │  └─────┐   ↓   │       │
│                         │        │ │        │  End  │       │
└─────────────────────────┘        │ └────────┼───────┘       │
                                   │          ↑               │
                                   │     ┌────┘               │
                                   │     │ Show error ←───────┘
                                   └──────────────────────────┘
```

Linear Execution (Without Control Flow):
```
Step 1: Get user input
Step 2: Process input
Step 3: Display result
Step 4: End program
```

Dynamic Execution (With Control Flow):
```
Step 1: Get user input
Step 2: IF input is valid
          Process input
        ELSE
          Show error message
          Go back to Step 1
Step 3: Display result
Step 4: Ask if user wants to continue
Step 5: IF user says yes
          Go back to Step 1
        ELSE
          End program
```

### Types of Control Flow

Control flow structures can be categorized into three main types:

```
Control Flow Categories:

┌─────────────────────────────────────────────────────────────────┐
│                    Control Flow Types                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. Sequential Flow       2. Conditional Flow     3. Iterative  │
│  ┌─────────────────┐     ┌─────────────────┐     Flow           │
│  │ Statement 1     │     │ Condition?      │     ┌───────────┐  │
│  │       ↓         │     │    /     \      │     │ Loop      │  │
│  │ Statement 2     │     │   /       \     │     │ Condition │  │
│  │       ↓         │     │  ↓         ↓    │     │    ↓      │  │
│  │ Statement 3     │     │ True    False   │     │ Execute   │  │
│  │       ↓         │     │  ↓         ↓    │     │ Block     │  │
│  │ Statement 4     │     │ Block A  Block B│     │    ↓      │  │
│  └─────────────────┘     │  \       /      │     │ Repeat? ──┘  │
│                          │   \     /       │     └───────────┘  │
│  Default behavior        │    ↓   ↓        │                    │
│  Top-to-bottom           │   Continue      │     while, for     │
│  One command at time     │                 │     do-while       │
│                          │ if-else, switch │                    │
└─────────────────────────────────────────────────────────────────┘
```

Sequential Flow:
- Normal top-to-bottom execution
- Default behavior of programs

Conditional Flow (Branching):
- Making decisions based on conditions
- Creating different execution paths
- Examples: if-else statements, switch statements

Iterative Flow (Looping):
- Repeating blocks of code multiple times
- Based on conditions or fixed iterations
- Examples: while loops, for loops

## 2. Conditional Statements: The Power of Decision Making

Conditional statements are structures used to create "branches" or "choices" for programs. They execute different blocks of code depending on whether condition expressions evaluate to true or false.

```
Conditional Statement Flow:

                    Program Flow
                         │
                         ▼
                   ┌─────────────┐
                   │ Condition?  │
                   │ (boolean)   │
                   └─────────────┘
                      /       \
                     /         \
                  True         False
                   /             \
                  ▼               ▼
         ┌─────────────────┐ ┌─────────────────┐
         │ Execute Block A │ │ Execute Block B │
         │ (if condition   │ │ (else condition │
         │  is true)       │ │  is false)      │
         └─────────────────┘ └─────────────────┘
                  \             /
                   \           /
                    \         /
                     ▼       ▼
              ┌─────────────────────┐
              │   Continue Program  │
              └─────────────────────┘
```

### Basic if Statement

The if statement executes a block of code only when the condition is true.

Syntax and Structure:
```java
if (condition) {
    // Code block executed only if condition is true
}
```

Example:
```java
if (isRaining == true) {
    System.out.println("Take an umbrella");
}
```

Real-world Application:
```java
int temperature = 35;
if (temperature > 30) {
    System.out.println("It's hot today, drink more water");
}
```

### if-else Statement

The if-else statement creates a clear two-way choice between alternatives.

Syntax and Structure:
```java
if (condition) {
    // Code block executed if condition is true
} else {
    // Code block executed if condition is false
}
```

Example:
```java
if (isRaining == true) {
    System.out.println("Take an umbrella");
} else {
    System.out.println("Wear sunglasses");
}
```

More Complex Example:
```java
int age = 17;
if (age >= 18) {
    System.out.println("You can vote");
} else {
    System.out.println("You cannot vote yet");
}
```

### if-else if-else Statement

Used for creating complex decision structures with more than two alternatives. Conditions are checked in order from top to bottom.

```
Multiple Condition Flow:

                Program Flow
                     │
                     ▼
           ┌─────────────────┐
           │   Condition 1?  │
           └─────────────────┘
               True │        False
                    ▼          │
           ┌─────────────────┐ │
           │   Execute       │ │
           │   Block 1       │ │
           └─────────────────┘ │
                    │          │
                    ▼          │
              ┌─────────────────┴─────┐
              │                       ▼
              │              ┌─────────────────┐
              │              │   Condition 2?  │
              │              └─────────────────┘
              │                  True │        False
              │                       ▼          │
              │              ┌─────────────────┐ │
              │              │   Execute       │ │
              │              │   Block 2       │ │
              │              └─────────────────┘ │
              │                       │          │
              │                       ▼          │
              │                 ┌─────────────────┴─────┐
              │                 │                       ▼
              │                 │              ┌─────────────────┐
              │                 │              │   Condition 3?  │
              │                 │              └─────────────────┘
              │                 │                  True │        False
              │                 │                       ▼          │
              │                 │              ┌─────────────────┐ │
              │                 │              │   Execute       │ │
              │                 │              │   Block 3       │ │
              │                 │              └─────────────────┘ │
              │                 │                       │          │
              ▼                 ▼                       ▼          ▼
         ┌──────────────────────────────────────────────────────────────┐
         │                    Continue Program                          │
         └──────────────────────────────────────────────────────────────┘

Key Points:
• Only ONE block executes (first true condition)
• Remaining conditions are NOT checked after match
• else block executes if NO conditions are true
```

Syntax and Structure:
```java
if (condition1) {
    // Code block 1
} else if (condition2) {
    // Code block 2
} else if (condition3) {
    // Code block 3
} else {
    // Default code block (optional)
}
```

Example:
```java
int score = 85;
char grade;

if (score >= 90) {
    grade = 'A';
} else if (score >= 80) {
    grade = 'B'; // Program will execute this block and exit the if-else chain
} else if (score >= 70) {
    grade = 'C';
} else {
    grade = 'F';
}
```

Extended Example - Temperature Advisory System:
```java
int temperature = 25;
String advice;

if (temperature >= 35) {
    advice = "Extremely hot - stay indoors with AC";
} else if (temperature >= 30) {
    advice = "Hot - drink plenty of water";
} else if (temperature >= 20) {
    advice = "Pleasant weather - perfect for outdoor activities";
} else if (temperature >= 10) {
    advice = "Cool - wear a light jacket";
} else {
    advice = "Cold - dress warmly";
}

System.out.println("Weather advice: " + advice);
```

### Important Characteristics of Conditional Statements

Exclusive Execution:
- Only one block in an if-else if-else chain will execute
- Once a condition is true, remaining conditions are not checked
- This is called "short-circuit evaluation" for conditionals

Boolean Context:
- Conditions must evaluate to boolean values (true or false)
- Non-boolean values may be automatically converted in some languages

Nested Conditionals:
```java
if (hasAccount) {
    if (passwordCorrect) {
        if (accountActive) {
            System.out.println("Login successful");
        } else {
            System.out.println("Account is suspended");
        }
    } else {
        System.out.println("Invalid password");
    }
} else {
    System.out.println("Please create an account first");
}
```

### Best Practices for Conditionals

Use Clear Conditions:
```java
// Poor
if (x == 1) {
    // ...
}

// Better
if (userIsLoggedIn) {
    // ...
}
```

Avoid Deep Nesting:
```java
// Poor (deeply nested)
if (condition1) {
    if (condition2) {
        if (condition3) {
            // deeply nested code
        }
    }
}

// Better (early return pattern)
if (!condition1) return;
if (!condition2) return;
if (!condition3) return;
// main logic here
```

## 3. Loops: The Art of Repetition

Loops are structures used to make programs execute a block of code repeatedly. They are essential for automation and processing collections of data.

```
Loop Types Comparison:

while Loop (Condition-Based):      for Loop (Count-Based):
┌─────────────────────────────┐   ┌─────────────────────────────┐
│          Start              │   │          Start              │
│             │               │   │             │               │
│             ▼               │   │             ▼               │
│     ┌───────────────┐       │   │   ┌─────────────────┐       │
│  ┌─►│ Condition?    │       │   │   │ Initialize      │       │
│  │  │ (boolean)     │       │   │   │ Counter = 0     │       │
│  │  └───────────────┘       │   │   └─────────────────┘       │
│  │    True │    False       │   │             │               │
│  │         ▼        │       │   │             ▼               │
│  │  ┌─────────────┐ │       │   │     ┌───────────────┐       │
│  │  │ Execute     │ │       │   │  ┌─►│ Counter <     │       │
│  │  │ Code Block  │ │       │   │  │  │ Limit?        │       │
│  │  └─────────────┘ │       │   │  │  └───────────────┘       │
│  │         │        │       │   │  │    True │    False       │
│  └─────────┘        │       │   │  │         ▼        │       │
│                     ▼       │   │  │  ┌─────────────┐ │       │
│            Continue Program │   │  │  │ Execute     │ │       │
└─────────────────────────────┘   │  │  │ Code Block  │ │       │
                                  │  │  └─────────────┘ │       │
Use when:                         │  │         │        │       │
• Unknown iterations              │  │         ▼        │       │
• Condition-dependent             │  │  ┌─────────────┐ │       │
• User input validation           │  │  │ Increment   │ │       │
• Game loops                      │  │  │ Counter++   │ │       │
                                  │  │  └─────────────┘ │       │
                                  │  │         │        │       │
                                  │  └─────────┘        │       │
                                  │                     ▼       │
                                  │            Continue Program │
                                  └─────────────────────────────┘

                                  Use when:
                                  • Known iterations
                                  • Processing arrays
                                  • Counting operations
                                  • Range-based tasks
```

### while Loop (Condition-Based Iteration)

Structure: Executes a block of code repeatedly as long as a specified condition remains true. The condition is checked before each iteration.

Use Cases: Ideal when you don't know the exact number of iterations needed, but you know the stopping condition.

Syntax:
```java
while (condition) {
    // Code block to repeat
    // Must include code that eventually makes condition false
}
```

Example - Password Validation:
```java
Scanner scanner = new Scanner(System.in);
String password;
boolean isCorrect = false;

while (!isCorrect) {
    System.out.print("Enter password: ");
    password = scanner.nextLine();
    
    if (password.equals("secret123")) {
        isCorrect = true;
        System.out.println("Access granted!");
    } else {
        System.out.println("Incorrect password. Try again.");
    }
}
```

Example - Reading User Input Until Valid:
```java
Scanner scanner = new Scanner(System.in);
int number = -1;

while (number < 1 || number > 10) {
    System.out.print("Enter a number between 1 and 10: ");
    number = scanner.nextInt();
    
    if (number < 1 || number > 10) {
        System.out.println("Invalid input. Please try again.");
    }
}

System.out.println("You entered: " + number);
```

#### Common while Loop Patterns

Counter-Based while Loop:
```java
int count = 1;
while (count <= 5) {
    System.out.println("Count: " + count);
    count++; // Important: increment to avoid infinite loop
}
```

Sentinel-Controlled while Loop:
```java
Scanner scanner = new Scanner(System.in);
String input = "";

while (!input.equals("quit")) {
    System.out.print("Enter command (or 'quit' to exit): ");
    input = scanner.nextLine();
    
    if (!input.equals("quit")) {
        System.out.println("You entered: " + input);
    }
}
```

### for Loop (Count-Based/Collection-Based Iteration)

Structure: Designed to repeat for a specific number of times or to iterate through every item in a collection.

Use Cases: Ideal when you know the exact number of iterations needed or when processing every element in a data collection.

#### Traditional for Loop

Syntax:
```java
for (initialization; condition; increment) {
    // Code block to repeat
}
```

Example - Counting:
```java
for (int i = 1; i <= 5; i++) {
    System.out.println("Iteration: " + i);
}
```

Example - Processing Array Elements:
```java
int[] numbers = {10, 20, 30, 40, 50};

for (int i = 0; i < numbers.length; i++) {
    System.out.println("Element " + i + ": " + numbers[i]);
}
```

#### Enhanced for Loop (for-each)

Syntax:
```java
for (dataType variable : collection) {
    // Code block using variable
}
```

Example:
```java
String[] fruits = {"Apple", "Banana", "Cherry"};

for (String fruit : fruits) {
    System.out.println(fruit);
}
```

Python Example:
```python
fruits = ["Apple", "Banana", "Cherry"]
for fruit in fruits:
    print(fruit)
```

#### for Loop Variations

Counting Backwards:
```java
for (int i = 10; i >= 1; i--) {
    System.out.println("Countdown: " + i);
}
```

Custom Increments:
```java
for (int i = 0; i <= 20; i += 5) {
    System.out.println("Value: " + i); // Prints 0, 5, 10, 15, 20
}
```

Multiple Variables:
```java
for (int i = 0, j = 10; i < 5; i++, j--) {
    System.out.println("i: " + i + ", j: " + j);
}
```

### Comparing while and for Loops

When to Use while Loops:
- Unknown number of iterations
- Condition-dependent termination
- Reading input until specific value
- Waiting for external events
- Game loops that run until game over

When to Use for Loops:
- Known number of iterations
- Processing arrays or collections
- Counting operations
- Mathematical calculations with sequences
- Iterating through ranges of values

Example Comparison:
```java
// Using while loop for unknown iterations
Scanner scanner = new Scanner(System.in);
String command = "";
while (!command.equals("exit")) {
    command = scanner.nextLine();
    processCommand(command);
}

// Using for loop for known iterations
int[] scores = {85, 92, 78, 96, 88};
for (int i = 0; i < scores.length; i++) {
    System.out.println("Student " + (i+1) + " score: " + scores[i]);
}
```

### Loop Control Statements

break Statement:
- Immediately exits the loop
- Useful for early termination

continue Statement:
- Skips the rest of current iteration
- Continues with next iteration

```
Loop Control Flow:

Normal Loop Flow:              With break:                With continue:
┌─────────────────┐           ┌─────────────────┐        ┌─────────────────┐
│      Start      │           │      Start      │        │      Start      │
│        │        │           │        │        │        │        │        │
│        ▼        │           │        ▼        │        │        ▼        │
│ ┌─────────────┐ │           │ ┌─────────────┐ │        │ ┌─────────────┐ │
│ │i=1: Execute │ │           │ │i=1: Execute │ │        │ │i=1: Execute │ │
│ └─────────────┘ │           │ └─────────────┘ │        │ └─────────────┘ │
│        │        │           │        │        │        │        │        │
│        ▼        │           │        ▼        │        │        ▼        │
│ ┌─────────────┐ │           │ ┌─────────────┐ │        │ ┌─────────────┐ │
│ │i=2: Execute │ │           │ │i=2: Execute │ │        │ │i=2: Execute │ │
│ └─────────────┘ │           │ └─────────────┘ │        │ └─────────────┘ │
│        │        │           │        │        │        │        │        │
│        ▼        │           │        ▼        │        │        ▼        │
│ ┌─────────────┐ │           │ ┌─────────────┐ │        │ ┌─────────────┐ │
│ │i=3: Execute │ │           │ │i=3: break   │ │        │ │i=3: continue│ │
│ └─────────────┘ │           │ └─────────────┘ │        │ │(skip rest)  │ │
│        │        │           │        │        │        │ └─────────────┘ │
│        ▼        │           │        ▼        │        │        │        │
│ ┌─────────────┐ │           │   Exit Loop  ───┼──────► │        ▼        │
│ │i=4: Execute │ │           │                 │        │ ┌─────────────┐ │
│ └─────────────┘ │           │                 │        │ │i=4: Execute │ │
│        │        │           │                 │        │ └─────────────┘ │
│        ▼        │           │                 │        │        │        │
│ ┌─────────────┐ │           │                 │        │        ▼        │
│ │i=5: Execute │ │           │                 │        │ ┌─────────────┐ │
│ └─────────────┘ │           │                 │        │ │i=5: Execute │ │
│        │        │           │                 │        │ └─────────────┘ │
│        ▼        │           │                 │        │        │        │
│   End Loop      │           │                 │        │        ▼        │
└─────────────────┘           └─────────────────┘        │   End Loop      │
                                                         └─────────────────┘

Output: 1,2,3,4,5             Output: 1,2                Output: 1,2,4,5
```

```java
for (int i = 1; i <= 10; i++) {
    if (i == 5) {
        break; // Exit loop when i equals 5
    }
    System.out.println(i); // Prints 1, 2, 3, 4
}
```

continue Statement:
- Skips the rest of current iteration
- Continues with next iteration

```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) {
        continue; // Skip printing when i equals 3
    }
    System.out.println(i); // Prints 1, 2, 4, 5
}
```

### Common Loop Pitfalls

Infinite Loops:
```java
// DANGEROUS - Infinite loop
while (true) {
    System.out.println("This will run forever!");
    // Missing condition to break out
}

// SAFE - Properly controlled loop
boolean keepRunning = true;
while (keepRunning) {
    // ... some logic
    if (someCondition) {
        keepRunning = false; // Ensures loop will end
    }
}
```

Off-by-One Errors:
```java
// Wrong - misses last element
for (int i = 0; i < array.length - 1; i++) {
    // Process array[i]
}

// Correct - processes all elements
for (int i = 0; i < array.length; i++) {
    // Process array[i]
}
```

## 4. Practical Applications and Examples

### Example 1: Grade Processing System

```java
import java.util.Scanner;

public class GradeProcessor {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Enter number of students: ");
        int numStudents = scanner.nextInt();
        
        int totalScore = 0;
        int passCount = 0;
        
        // for loop - we know exactly how many students
        for (int i = 1; i <= numStudents; i++) {
            int score = -1;
            
            // while loop - keep asking until valid score
            while (score < 0 || score > 100) {
                System.out.print("Enter score for student " + i + " (0-100): ");
                score = scanner.nextInt();
                
                if (score < 0 || score > 100) {
                    System.out.println("Invalid score! Please enter 0-100.");
                }
            }
            
            totalScore += score;
            
            // Conditional statement - determine pass/fail
            if (score >= 60) {
                passCount++;
                System.out.println("Student " + i + ": PASS");
            } else {
                System.out.println("Student " + i + ": FAIL");
            }
        }
        
        double average = (double) totalScore / numStudents;
        System.out.println("\nClass Statistics:");
        System.out.println("Average score: " + average);
        System.out.println("Students passed: " + passCount + "/" + numStudents);
    }
}
```

### Example 2: Simple Menu System

```java
import java.util.Scanner;

public class MenuSystem {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        boolean running = true;
        
        // while loop - continue until user chooses to exit
        while (running) {
            System.out.println("\n=== Main Menu ===");
            System.out.println("1. View Profile");
            System.out.println("2. Edit Settings");
            System.out.println("3. Help");
            System.out.println("4. Exit");
            System.out.print("Choose an option: ");
            
            int choice = scanner.nextInt();
            
            // Conditional statements - handle different menu choices
            if (choice == 1) {
                System.out.println("Displaying user profile...");
            } else if (choice == 2) {
                System.out.println("Opening settings...");
            } else if (choice == 3) {
                System.out.println("Displaying help information...");
            } else if (choice == 4) {
                System.out.println("Thank you for using our system!");
                running = false; // This will end the while loop
            } else {
                System.out.println("Invalid option! Please choose 1-4.");
            }
        }
    }
}
```

### Example 3: Number Guessing Game

```java
import java.util.Random;
import java.util.Scanner;

public class GuessingGame {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Random random = new Random();
        
        int targetNumber = random.nextInt(100) + 1; // Random number 1-100
        int attempts = 0;
        boolean hasWon = false;
        
        System.out.println("Welcome to the Number Guessing Game!");
        System.out.println("I'm thinking of a number between 1 and 100.");
        
        // while loop - continue until player wins
        while (!hasWon) {
            System.out.print("Enter your guess: ");
            int guess = scanner.nextInt();
            attempts++;
            
            // Conditional statements - provide feedback
            if (guess == targetNumber) {
                hasWon = true;
                System.out.println("Congratulations! You won in " + attempts + " attempts!");
            } else if (guess < targetNumber) {
                System.out.println("Too low! Try again.");
            } else {
                System.out.println("Too high! Try again.");
            }
        }
    }
}
```

## 5. Advanced Control Flow Concepts

### Nested Loops

Loops can be placed inside other loops for processing multi-dimensional data:

```java
// Multiplication table
for (int i = 1; i <= 5; i++) {
    for (int j = 1; j <= 5; j++) {
        System.out.print((i * j) + "\t");
    }
    System.out.println(); // New line after each row
}
```

Pattern Printing:
```java
// Print a triangle pattern
for (int i = 1; i <= 5; i++) {
    for (int j = 1; j <= i; j++) {
        System.out.print("* ");
    }
    System.out.println();
}
```

### Loop Labels and Control

For complex nested loops, labels can be used with break and continue:

```java
outer: for (int i = 1; i <= 3; i++) {
    inner: for (int j = 1; j <= 3; j++) {
        if (i == 2 && j == 2) {
            break outer; // Breaks out of both loops
        }
        System.out.println("i=" + i + ", j=" + j);
    }
}
```

### do-while Loop

Executes at least once, then checks condition:

```java
int number;
Scanner scanner = new Scanner(System.in);

do {
    System.out.print("Enter a positive number: ");
    number = scanner.nextInt();
    
    if (number <= 0) {
        System.out.println("Please enter a positive number!");
    }
} while (number <= 0);

System.out.println("You entered: " + number);
```

---

## 📋 Summary & Practical Exercise

### Comprehensive Summary

Control Flow enables programs to work non-linearly and respond intelligently to different situations. The main categories are:

Conditional Statements (if-else):
- Create decision branches in program execution
- Enable programs to respond differently based on conditions
- if executes code only when condition is true
- if-else provides two-way choices
- if-else if-else creates multiple-choice decision structures
- Only one block executes in an if-else chain

Loop Statements (while, for):
- Enable repetitive execution of code blocks
- Essential for automation and data processing
- while loops are condition-based, ideal for unknown iteration counts
- for loops are count-based, ideal for known iterations or collection processing
- Both can be controlled with break and continue statements

Choosing the Right Structure:
- Use if-else for decision making and branching logic
- Use while loops when iteration depends on conditions
- Use for loops when iterating a specific number of times or through collections
- Consider nested structures for complex logic, but avoid excessive nesting

Key Principles:
- Always ensure loops have proper termination conditions
- Use meaningful variable names and clear conditions
- Structure code to be readable and maintainable
- Test edge cases and boundary conditions
- Be aware of common pitfalls like infinite loops and off-by-one errors

### Practical Exercise

You are writing a program for an ATM system. Analyze the following scenarios and determine which Control Flow structure to use:

```
ATM System Analysis:

Scenario 1: PIN Validation          Scenario 2: ATM Main Loop
┌─────────────────────────────┐     ┌─────────────────────────────┐
│ User enters PIN             │     │ User interacts with ATM     │
│          │                  │     │          │                  │
│          ▼                  │     │          ▼                  │
│   ┌─────────────┐           │     │   ┌─────────────┐           │
│   │ PIN correct?│           │     │   │ Show menu   │           │
│   └─────────────┘           │     │   └─────────────┘           │
│    True │   False           │     │          │                  │
│         ▼      ▼            │     │          ▼                  │
│   ┌─────────────────────┐   │     │   ┌─────────────┐           │
│   │ Grant │ Block       │   │     │   │User chooses │           │
│   │Access │Access       │   │     │   │option       │           │
│   └─────────────────────┘   │     │   └─────────────┘           │
│                             │     │          │                  │
│ Decision: if-else           │     │          ▼                  │
│ Reason: Binary choice       │     │   ┌─────────────┐           │
│                             │     │   │ Process     │           │
│                             │     │   │ transaction │           │
│                             │     │   └─────────────┘           │
│                             │     │          │                  │
│                             │     │          ▼                  │
│                             │     │   ┌─────────────┐           │
│                             │     │   │Continue?    │───No──┐   │
│                             │     │   └─────────────┘       │   │
│                             │     │       Yes │             │   │
│                             │     │           └─────────────┼─► │
│                             │     │                         ▼   │
│                             │     │ Decision: while loop        │
│                             │     │ Reason: Unknown iterations  │
│                             │     │                             │
└─────────────────────────────┘     └─────────────────────────────┘

Control Flow Decision Tree:
┌─────────────────────────────────────────────────────────────────┐
│                 When to Use What?                               │
│                                                                 │
│     Need to make a decision?                                    │
│              │                                                  │
│              ▼                                                  │
│        ┌──────────────┐                                         │
│        │ Yes   │   No │                                         │
│        ▼       ▼      ▼                                         │
│   Use if-else    Need repetition?                               │
│                       │                                         │
│                 ┌─────┴─────┐                                   │
│                 ▼           ▼                                   │
│          Known count?   Unknown count?                          │
│                 │           │                                   │
│                 ▼           ▼                                   │
│            Use for     Use while                                │
│             loop        loop                                    │
└─────────────────────────────────────────────────────────────────┘
```

1) Checking if the user entered the correct PIN:
   Should you use if-else or a loop?

2) The ATM needs to keep accepting user commands until the user selects "Exit":
   Should you use a for loop or while loop? Why?

#### Detailed Analysis:

Scenario 1: PIN Validation
```java
// Analysis: This is a decision-making situation
// We need to check one condition and respond accordingly

String enteredPIN = getUserInput();
String correctPIN = "1234";

if (enteredPIN.equals(correctPIN)) {
    System.out.println("Access granted");
    // Proceed to main menu
} else {
    System.out.println("Invalid PIN");
    // Block access or allow retry
}
```

Answer: Use if-else
Reasoning: PIN checking is a binary decision (correct or incorrect). We're not repeating an action; we're making a one-time comparison and branching based on the result.

Scenario 2: ATM Main Operation Loop
```java
// Analysis: This requires repetitive operation with uncertain duration
// We don't know how many transactions the user will perform

Scanner scanner = new Scanner(System.in);
boolean keepRunning = true;

while (keepRunning) {
    System.out.println("1. Check Balance");
    System.out.println("2. Withdraw Money");
    System.out.println("3. Deposit Money");
    System.out.println("4. Exit");
    System.out.print("Choose option: ");
    
    int choice = scanner.nextInt();
    
    if (choice == 1) {
        checkBalance();
    } else if (choice == 2) {
        withdrawMoney();
    } else if (choice == 3) {
        depositMoney();
    } else if (choice == 4) {
        keepRunning = false; // Exit condition
        System.out.println("Thank you for using our ATM");
    } else {
        System.out.println("Invalid option");
    }
}
```

Answer: Use while loop
Reasoning: 
- We don't know how many operations the user will perform
- The loop should continue based on a condition (user hasn't chosen to exit)
- A for loop wouldn't be appropriate because we don't have a fixed number of iterations
- The termination depends on user choice, not a predetermined count

Extended Scenarios:

3) Allowing 3 attempts for PIN entry:
```java
int attempts = 0;
boolean accessGranted = false;

while (attempts < 3 && !accessGranted) {
    String enteredPIN = getUserInput();
    attempts++;
    
    if (enteredPIN.equals(correctPIN)) {
        accessGranted = true;
        System.out.println("Access granted");
    } else {
        System.out.println("Invalid PIN. Attempts remaining: " + (3 - attempts));
    }
}

if (!accessGranted) {
    System.out.println("Card blocked due to too many failed attempts");
}
```

This combines both conditional logic and looping - demonstrating how control flow structures work together in real applications.

4) Processing a batch of transactions from a file:
```java
String[] transactions = loadTransactionsFromFile();

for (int i = 0; i < transactions.length; i++) {
    String transaction = transactions[i];
    processTransaction(transaction);
    
    if (hasError(transaction)) {
        System.out.println("Error in transaction " + (i + 1));
    }
}
```

Answer: Use for loop
Reasoning: We have a known collection of transactions to process. Each transaction needs to be handled exactly once, making for loop the ideal choice.

Understanding when to use each control flow structure is crucial for writing efficient, readable, and maintainable code.

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
