# 📖 Operators

## 💡 Basic knowledge required:

Understanding of Variables and Data Types concepts (from Lesson 3.1)

## 🎯 Learning Objectives

Upon completion of this topic, you will be able to:

- Define "operators" as symbols used to perform operations on data (operands)
- Identify and classify the main types of operators (Arithmetic, Assignment, Comparison, Logical)
- Understand the concepts of precedence and associativity of operators for evaluating complex expressions

---

## 1. Introduction to Operators

If variables are like "nouns" (data) in programming languages, operators are like "verbs" (actions). They are symbols used to perform mathematical operations, assign values, compare values, or perform logical operations on one or more pieces of data. The data being operated on are called operands.

The combination of values, variables, and operators forms expressions, which can be evaluated to produce a single value. For example: (x + 5) * 2

### Understanding Expressions

An expression is any combination of values, variables, and operators that can be evaluated to produce a result. Every expression has a data type that matches the type of value it produces when evaluated.

Simple Expressions:
```
5 + 3                    // Arithmetic expression, evaluates to 8
x                        // Variable expression, evaluates to x's value
"Hello"                  // Literal expression, evaluates to the string "Hello"
```

Complex Expressions:
```
(x + 5) * 2             // Mixed arithmetic expression
(age >= 18) && hasID    // Boolean expression with logical operators
name + " " + surname    // String concatenation expression
```

### The Operator-Operand Relationship

Understanding how operators work with operands:

```
Structure: Operand Operator Operand = Result
Examples:
   5       +       3     =   8
   x       *       2     =   (depends on x value)
  true     &&     false  =   false
 "Hi"      +      " "    =   "Hi "
```

This relationship forms the foundation of all computational expressions in programming.

## 2. Main Types of Operators

### A. Arithmetic Operators

Used for basic mathematical calculations:

- + (Addition)
- - (Subtraction)
- * (Multiplication)
- / (Division)
- % (Modulus): Returns the remainder after division

Examples in different programming languages:

Java:
```java
int score = 100 / 3;        // Result is 33 (integer division)
int remainder = 100 % 3;    // Result is 1 (remainder from division)
double precise = 100.0 / 3; // Result is 33.333... (floating-point division)
```

Python:
```python
score = 100 // 3      # Floor division: 33
remainder = 100 % 3   # Modulus: 1
precise = 100 / 3     # True division: 33.333...
```

C:
```c
int score = 100 / 3;        // Result is 33 (integer division)
int remainder = 100 % 3;    // Result is 1 (remainder from division)
float precise = 100.0 / 3;  // Result is 33.333... (floating-point division)
```

#### Division Behavior

Understanding different types of division:

Integer Division:
- When both operands are integers, the result is an integer
- The decimal portion is truncated, not rounded
- Example: 7 / 3 = 2 (not 2.333...)

Floating-Point Division:
- When at least one operand is a floating-point number, the result includes decimals
- Example: 7.0 / 3 = 2.333...

#### Practical Applications of Modulus

The modulus operator has many useful applications:

Determining Even or Odd:
```java
if (number % 2 == 0) {
    System.out.println("Even number");
} else {
    System.out.println("Odd number");
}
```

Creating Cycling Patterns:
```java
// Cycle through values 0, 1, 2, 0, 1, 2...
int cycleValue = counter % 3;

// Wrap array indices
int safeIndex = index % arrayLength;
```

Time Calculations:
```java
int totalSeconds = 125;
int minutes = totalSeconds / 60;        // 2 minutes
int seconds = totalSeconds % 60;        // 5 seconds remaining
```

Extracting Digits:
```java
int number = 1234;
int lastDigit = number % 10;           // 4
int secondLastDigit = (number / 10) % 10; // 3
```

### B. Assignment Operators

Used to assign values to variables:

- = (Basic assignment): Assigns the value from the right to the variable on the left
- +=, -=, *=, /=, %= (Compound assignment): Performs the operation and assigns the result back to the variable

Basic Assignment:
```java
int level = 10;  // Initial assignment
level = 15;      // Reassignment
```

Compound Assignment:
```java
int level = 10;
level += 5;  // Equivalent to: level = level + 5; Now level is 15
level *= 2;  // Equivalent to: level = level * 2; Now level is 30
level /= 3;  // Equivalent to: level = level / 3; Now level is 10
level %= 7;  // Equivalent to: level = level % 7; Now level is 3
```

#### Assignment vs Initialization

Understanding the distinction:

```java
// Declaration and initialization (first time assigning a value)
int age = 25;

// Assignment (changing existing value)
age = 26;           // Direct assignment
age = age + 1;      // Calculation then assignment
age += 1;           // Compound assignment (shorthand)
```

#### Assignment Return Values

Assignment operations return the assigned value, enabling chaining:

```java
int x, y, z;
x = y = z = 5;  // All variables become 5
// Evaluation: z = 5 returns 5, y = 5 returns 5, x = 5 returns 5
```

### C. Comparison/Relational Operators

Used to compare two values. The result is always a Boolean value (true or false):

- == (Equal to)
- != (Not equal to)
- > (Greater than)
- < (Less than)
- >= (Greater than or equal to)
- <= (Less than or equal to)

Examples:
```java
int userAge = 20;
boolean canVote = (userAge >= 18);  // canVote will be true
boolean isTeenager = (userAge >= 13) && (userAge <= 19); // true
boolean isChild = (userAge < 13);   // false
```

Python allows chained comparisons:
```python
user_age = 20
is_teenager = 13 <= user_age <= 19  # Equivalent to (13 <= user_age) && (user_age <= 19)
```

#### Common Mistake: Assignment vs Comparison

Be careful not to confuse = (assignment) with == (comparison):

```java
// WRONG - This assigns 5 to x, doesn't compare
if (x = 5) {  // This will cause a compilation error in Java
    // This assigns 5 to x and may use the result as condition
}

// CORRECT - This compares x with 5
if (x == 5) {
    // This checks if x equals 5
}
```

#### Comparing Different Data Types

Numeric Comparisons:
```java
5 > 3           // true
3.14 == 3.14    // true
2.0 == 2        // true (automatic type conversion)
```

String Comparisons:
```java
// In Java, use .equals() for string content comparison
"apple".equals("apple")     // true
"Apple".equals("apple")     // false (case sensitive)

// Lexicographic comparison (dictionary order)
"apple".compareTo("banana") // negative number (apple comes before banana)
```

#### Floating-Point Comparison Challenges

Comparing floating-point numbers requires special consideration:

```java
// PROBLEMATIC
double result = 0.1 + 0.2;
if (result == 0.3) {  // May be false due to floating-point precision
    System.out.println("Equal");
}

// BETTER APPROACH
double epsilon = 1e-10;
if (Math.abs(result - 0.3) < epsilon) {
    System.out.println("Close enough to equal");
}
```

### D. Logical Operators

Used to connect two or more Boolean expressions or invert Boolean values:

- && (AND): Result is true only when both expressions are true
- || (OR): Result is true when at least one expression is true
- ! (NOT): Inverts the Boolean value (true becomes false, false becomes true)

Examples:
```java
boolean hasKey = true;
boolean isAuthorized = false;
boolean canOpenDoor = hasKey && isAuthorized;  // canOpenDoor will be false

boolean canEnter = hasKey || isAuthorized;     // canEnter will be true
boolean isLocked = !canOpenDoor;               // isLocked will be true
```

#### Truth Tables

Understanding logical operators through truth tables:

AND (&&) Truth Table:
```
A     | B     | A && B
------|-------|-------
true  | true  | true
true  | false | false
false | true  | false
false | false | false
```

OR (||) Truth Table:
```
A     | B     | A || B
------|-------|-------
true  | true  | true
true  | false | true
false | true  | true
false | false | false
```

NOT (!) Truth Table:
```
A     | !A
------|------
true  | false
false | true
```

#### Short-Circuit Evaluation

Logical operators use short-circuit evaluation for efficiency and safety:

AND (&&) Short-Circuit:
- If the first operand is false, the second operand is not evaluated
- The result is already determined to be false

OR (||) Short-Circuit:
- If the first operand is true, the second operand is not evaluated
- The result is already determined to be true

Practical examples:
```java
// Safe division - if x is 0, division won't be attempted
boolean result = (x != 0) && (100 / x > 5);

// Efficient search - if found in database, cache won't be searched
boolean found = searchDatabase() || searchCache();

// Null safety - if object is null, method won't be called
boolean isValid = (object != null) && object.isValid();
```

## 3. Precedence and Associativity

When evaluating complex expressions like a + b * c, programming languages follow clear rules to ensure consistent results.

### Precedence (Order of Operations)

Precedence determines which operators are evaluated first, similar to mathematical rules:

```
Higher precedence (evaluated first):
  ()                Parentheses
  !                 Logical NOT
  * / %             Multiplication, Division, Modulus
  + -               Addition, Subtraction
  > < >= <=         Relational operators
  == !=             Equality operators
  &&                Logical AND
  ||                Logical OR
Lower precedence (evaluated last):
  = += -= *= /= %=  Assignment operators
```

Examples demonstrating precedence:
```java
int result1 = 10 + 5 * 2;        // Evaluated as: 10 + (5 * 2) = 20
boolean result2 = 5 > 3 && 2 < 4; // Evaluated as: (5 > 3) && (2 < 4) = true
int result3 = 20 / 4 + 2 * 3;    // Evaluated as: (20 / 4) + (2 * 3) = 5 + 6 = 11
```

### Associativity (Direction of Evaluation)

Associativity determines the direction of evaluation for operators with the same precedence:

Left-to-Right Associativity (Most operators):
```java
int result = 100 - 10 + 5;  // Evaluated as: ((100 - 10) + 5) = 95
int result = 20 / 4 * 2;    // Evaluated as: ((20 / 4) * 2) = 10
```

Right-to-Left Associativity (Assignment operators):
```java
int x, y, z;
x = y = z = 5;  // Evaluated as: x = (y = (z = 5)); All become 5
```

### Using Parentheses for Clarity

When operator precedence might be unclear, use parentheses:

```java
// Force different evaluation order
int result1 = (10 + 5) * 2;      // Forces addition first: 30
int result2 = 10 + (5 * 2);      // Standard precedence: 20

// Clear logical grouping
boolean canProceed = (userLoggedIn && accountVerified) || 
                    (guestMode && termsAccepted);
```

### Complex Expression Evaluation Example

Let's analyze this step by step:
```java
boolean result = (10 > 5) && !(7 == 7) || (10 % 3 == 1);
```

Step-by-step evaluation:

1. Evaluate parentheses first:
   - (10 > 5) = true
   - (7 == 7) = true
   - (10 % 3 == 1): First 10 % 3 = 1, then 1 == 1 = true

2. Apply NOT operator (higher precedence than &&):
   - !(7 == 7) = !true = false

3. Apply AND operator (higher precedence than ||):
   - (10 > 5) && !(7 == 7) = true && false = false

4. Apply OR operator (lowest precedence):
   - false || (10 % 3 == 1) = false || true = true

Final result: true

## 4. Practical Applications

### Example 1: Grade Calculator

```java
public class GradeCalculator {
    public static void main(String[] args) {
        int totalPoints = 85;
        int maxPoints = 100;
        
        // Calculate percentage using arithmetic operators
        double percentage = (double) totalPoints / maxPoints * 100;
        
        // Determine letter grade using comparison operators
        char grade;
        if (percentage >= 90) {
            grade = 'A';
        } else if (percentage >= 80) {
            grade = 'B';
        } else if (percentage >= 70) {
            grade = 'C';
        } else if (percentage >= 60) {
            grade = 'D';
        } else {
            grade = 'F';
        }
        
        System.out.println("Score: " + percentage + "% - Grade: " + grade);
    }
}
```

### Example 2: Input Validation

```java
public class UserValidator {
    public static boolean validateUser(String email, String password, int age) {
        // Email validation using logical operators
        boolean validEmail = (email != null) && 
                            (email.length() > 0) && 
                            email.contains("@");
        
        // Password validation
        boolean validPassword = (password != null) && 
                               (password.length() >= 8);
        
        // Age validation
        boolean validAge = (age >= 13) && (age <= 120);
        
        // All conditions must be true
        return validEmail && validPassword && validAge;
    }
}
```

### Example 3: Mathematical Operations

```python
def demonstrate_operators():
    # Arithmetic operations
    a = 15
    b = 4
    
    print(f"Addition: {a} + {b} = {a + b}")           # 19
    print(f"Subtraction: {a} - {b} = {a - b}")        # 11
    print(f"Multiplication: {a} * {b} = {a * b}")     # 60
    print(f"Division: {a} / {b} = {a / b}")           # 3.75
    print(f"Floor Division: {a} // {b} = {a // b}")   # 3
    print(f"Modulus: {a} % {b} = {a % b}")            # 3
    
    # Compound assignment
    x = 10
    x += 5   # x = x + 5, now x is 15
    x *= 2   # x = x * 2, now x is 30
    print(f"After compound assignments: x = {x}")
```

## 5. Common Mistakes and Best Practices

### Mistake 1: Floating-Point Precision

Problem:
```java
double result = 0.1 + 0.2;
if (result == 0.3) {  // This may fail
    System.out.println("Equal");
}
```

Solution:
```java
double result = 0.1 + 0.2;
double epsilon = 1e-10;
if (Math.abs(result - 0.3) < epsilon) {
    System.out.println("Close enough");
}
```

### Mistake 2: Integer Division

Problem:
```java
double average = (5 + 7) / 2;  // Result: 6.0 (integer division)
```

Solution:
```java
double average = (5 + 7) / 2.0;  // Result: 6.0 (floating-point division)
```

### Mistake 3: Assignment vs Comparison

Problem:
```java
if (x = 5) {  // Assignment, not comparison
    // This assigns 5 to x
}
```

Solution:
```java
if (x == 5) {  // Comparison
    // This checks if x equals 5
}
```

### Best Practice 1: Use Meaningful Variable Names

Poor:
```java
boolean a = (b > 18) && (c == true);
```

Better:
```java
boolean canVote = (age > 18) && (hasValidId == true);
```

### Best Practice 2: Break Complex Expressions

Hard to read:
```java
if ((userAge >= 18) && (hasLicense == true) && (hasInsurance == true)) {
    // Allow driving
}
```

Easier to read:
```java
boolean isAdult = userAge >= 18;
boolean hasValidDocuments = hasLicense && hasInsurance;

if (isAdult && hasValidDocuments) {
    // Allow driving
}
```

### Best Practice 3: Use Parentheses for Clarity

```java
// Less clear
int result = a + b * c - d / e;

// More clear
int result = a + (b * c) - (d / e);
```

---

## 📋 Summary & Practical Exercise

### Comprehensive Summary

Operators are symbols that perform operations on data (operands). The main categories are:

Arithmetic Operators (+, -, *, /, %):
- Perform mathematical calculations
- Include considerations for integer vs floating-point division
- Modulus operator useful for remainders and cycling patterns

Assignment Operators (=, +=, -=, *=, /=, %=):
- Assign values to variables
- Compound assignment operators provide shorthand notation
- Assignment operations return values, enabling chaining

Comparison Operators (==, !=, >, <, >=, <=):
- Compare values and return Boolean results
- Be careful with floating-point comparisons due to precision issues
- Distinguish between assignment (=) and equality comparison (==)

Logical Operators (&&, ||, !):
- Combine and manipulate Boolean expressions
- Use short-circuit evaluation for efficiency and safety
- Follow truth table rules for predictable results

Precedence and Associativity:
- Precedence determines order of operations (similar to mathematics)
- Associativity determines direction for operators of equal precedence
- Use parentheses to clarify intentions and override default precedence
- Complex expressions should be broken down for readability

Essential principles:
- Understand operator precedence to predict expression evaluation
- Use parentheses when expression logic is not immediately clear
- Be aware of common pitfalls like floating-point precision and integer division
- Break complex expressions into simpler, more readable parts
- Leverage short-circuit evaluation for both performance and error prevention

### Practical Exercise

Analyze the following expression step by step. What will be the final result and why?

Precedence order for reference: () > ! > * / % > + - > > < >= <= > == != > && > ||

```java
boolean result = (10 > 5) && !(7 == 7) || (10 % 3 == 1);
```

Step-by-Step Solution:

Step 1: Evaluate expressions in parentheses first
- (10 > 5) = true (10 is greater than 5)
- (7 == 7) = true (7 equals 7)
- (10 % 3 == 1): First calculate 10 % 3 = 1, then 1 == 1 = true

Step 2: Apply NOT operator (higher precedence than &&)
- !(7 == 7) = !true = false

Step 3: Apply AND operator (higher precedence than ||)
- (10 > 5) && !(7 == 7) = true && false = false

Step 4: Apply OR operator (lowest precedence)
- false || (10 % 3 == 1) = false || true = true

Final result: true

Analysis Questions:
1. Why does the modulus operation get evaluated before the equality comparison?
2. How does operator precedence affect the overall evaluation order?
3. What would happen if we changed the && to || in the expression?
4. How would adding different parentheses change the result?

Additional Practice:
Try evaluating these expressions step by step:
- boolean test1 = 5 + 3 * 2 > 10 && !(false || true);
- int calc = 20 / 4 + 3 * 2 - 1;
- boolean access = true || false && !true;

Understanding operator precedence and associativity is fundamental to writing correct expressions and debugging code effectively.

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.