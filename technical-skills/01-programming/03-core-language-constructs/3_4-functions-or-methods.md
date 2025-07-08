# 📖 Functions and Methods

## 💡 Basic knowledge required:

Understanding of variables, data types, and control flow structures (from Lessons 3.1-3.3)

## 🎯 Learning Objectives

Upon completion of this topic, you will be able to:

- Define "function" and explain its role in code organization, abstraction, and code reusability
- Identify and explain the main components of a function: signature (name, parameters) and body
- Understand the concept of passing "arguments" to "parameters" and returning values
- Explain the basic differences between "functions" and "methods" in the context of object-oriented programming

---

## 1. Introduction: Principles of Abstraction and Reusability

As programs grow larger, we often find ourselves writing the same or similar blocks of code repeatedly in multiple places. This violates the DRY (Don't Repeat Yourself) principle, making code unnecessarily long, difficult to read, and most importantly, "difficult to maintain" (if there's an error in that code block, we have to track down and fix it everywhere it was copied).

Functions are the primary mechanism in programming languages created specifically to solve this problem. They "encapsulate" blocks of code that serve specific purposes, giving them names so we can call and reuse them repeatedly. This is one of the most powerful forms of abstraction.

### Why Functions Matter

Without Functions:
```java
// Calculating areas in different parts of the program
int area1 = length1 * width1;
System.out.println("Area 1: " + area1);

// Later in the code...
int area2 = length2 * width2;
System.out.println("Area 2: " + area2);

// Even later...
int area3 = length3 * width3;
System.out.println("Area 3: " + area3);
```

With Functions:
```java
// Define once
public static int calculateArea(int length, int width) {
    return length * width;
}

// Use multiple times
int area1 = calculateArea(length1, width1);
int area2 = calculateArea(length2, width2);
int area3 = calculateArea(length3, width3);
```

### Benefits of Functions

Code Reusability:
- Write once, use many times
- Reduces code duplication
- Consistent behavior across the program

Maintainability:
- Bug fixes only need to be made in one place
- Changes to logic only require updating the function
- Easier to test individual components

Readability:
- Well-named functions serve as documentation
- Complex operations can be broken into understandable parts
- Code becomes more self-explanatory

Modularity:
- Programs can be broken into smaller, manageable pieces
- Different team members can work on different functions
- Functions can be tested independently

## 2. Anatomy of a Function

A function is a named block of code that operates independently to perform a specific task. It consists of several key components:

### Function Signature

The function signature defines the "interface" of the function, consisting of:

Function Name:
- A unique identifier used to call the function
- Should be descriptive and follow naming conventions
- Examples: calculateArea, getUserInput, validateEmail

Parameters:
- Special variables that act as "input slots"
- Receive data that the function needs to perform its task
- Define what type of data the function expects

Return Type (in statically-typed languages):
- Specifies what type of data the function will return
- Can be void (returns nothing) or any data type

### Function Body

The function body is the block of code (usually enclosed in {...} or defined by indentation) that contains the set of instructions executed when the function is called.

### Return Statement

The return statement sends the "result" of the function's work back to the code that called the function.

### Function Structure Examples

Java Example:
```java
// Return type  Function name    Parameters
public static int calculateSum(int a, int b) {
    // Function body starts here
    int result = a + b;
    return result;  // Return statement
}
```

Python Example:
```python
# Function name    Parameters
def calculate_sum(a, b):
    # Function body (indented)
    result = a + b
    return result  # Return statement
```

C Example:
```c
// Return type  Function name    Parameters
int calculateSum(int a, int b) {
    // Function body starts here
    int result = a + b;
    return result;  // Return statement
}
```

### Detailed Component Analysis

Function Name Guidelines:
```java
// Good function names
public static double calculateCircleArea(double radius)
public static boolean isValidEmail(String email)
public static void displayWelcomeMessage()

// Poor function names
public static double calc(double r)
public static boolean check(String s)
public static void doStuff()
```

Parameter Types:
```java
// Multiple parameters with different types
public static String formatName(String firstName, String lastName, boolean uppercase) {
    String fullName = firstName + " " + lastName;
    return uppercase ? fullName.toUpperCase() : fullName;
}

// No parameters
public static double getCurrentTimestamp() {
    return System.currentTimeMillis();
}

// Array parameter
public static double calculateAverage(int[] numbers) {
    int sum = 0;
    for (int num : numbers) {
        sum += num;
    }
    return (double) sum / numbers.length;
}
```

Return Types:
```java
// Returns an integer
public static int findMaximum(int a, int b) {
    return (a > b) ? a : b;
}

// Returns a boolean
public static boolean isPrime(int number) {
    if (number < 2) return false;
    for (int i = 2; i <= Math.sqrt(number); i++) {
        if (number % i == 0) return false;
    }
    return true;
}

// Returns nothing (void)
public static void printGreeting(String name) {
    System.out.println("Hello, " + name + "!");
}

// Returns a string
public static String reverseString(String input) {
    return new StringBuilder(input).reverse().toString();
}
```

## 3. Function Call Mechanism

The process of working with functions involves two main steps: "definition" and "invocation":

### Function Definition

Function definition is creating the function and specifying its behavior. This is where we write the code that will be executed when the function is called.

### Function Call (Invocation)

Function call is instructing the code in the function to execute by calling its name, along with sending arguments (actual data values) that we want the function's parameters to use.

### Parameter vs Argument

Parameters:
- Variables defined in the function signature
- Act as placeholders for incoming data
- Exist only within the function scope

Arguments:
- Actual values passed to the function when called
- Can be literals, variables, or expressions
- Must match the parameter types and order

### Detailed Example

```java
// Function Definition
public static double calculateRectangleArea(double width, double height) {
    // width and height are "parameters"
    double area = width * height;
    return area;  // Return the area as the result
}

public static void main(String[] args) {
    // Function Call
    // 10.0 and 5.0 are "arguments" that get passed in
    // The value 10.0 will be assigned to parameter width
    // The value 5.0 will be assigned to parameter height
    double result = calculateRectangleArea(10.0, 5.0);
    
    // The variable result will store the value returned by the function (50.0)
    System.out.println("Area: " + result);
    
    // Using variables as arguments
    double roomWidth = 12.5;
    double roomHeight = 8.0;
    double roomArea = calculateRectangleArea(roomWidth, roomHeight);
    
    // Using expressions as arguments
    double totalArea = calculateRectangleArea(width1 + width2, height1);
}
```

### Function Execution Flow

```java
public static int multiply(int x, int y) {
    System.out.println("Inside multiply function");
    int product = x * y;
    System.out.println("Calculated product: " + product);
    return product;
}

public static void main(String[] args) {
    System.out.println("Before function call");
    int result = multiply(4, 5);  // Execution jumps to multiply function
    System.out.println("After function call, result: " + result);
}

// Output:
// Before function call
// Inside multiply function
// Calculated product: 20
// After function call, result: 20
```

### Advanced Parameter Concepts

Variable Number of Parameters (Varargs in Java):
```java
public static int sum(int... numbers) {
    int total = 0;
    for (int num : numbers) {
        total += num;
    }
    return total;
}

// Can be called with different numbers of arguments
int result1 = sum(1, 2, 3);
int result2 = sum(10, 20, 30, 40, 50);
```

Default Parameters (Python example):
```python
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}!"

# Can be called with or without the second argument
message1 = greet("Alice")          # Uses default: "Hello, Alice!"
message2 = greet("Bob", "Hi")      # Uses provided: "Hi, Bob!"
```

## 4. Functions vs Methods

In practice, we often hear these two terms, which have subtle conceptual differences:

### Functions

Functions are independent blocks of code that operate standalone, not dependent on any object. They are commonly found in procedural and functional programming paradigms.

Characteristics:
- Independent and self-contained
- Called directly by name
- Don't belong to any object or class
- Take all necessary data as parameters

Examples:
```java
// Java static methods (function-like)
public static void main(String[] args)
public static int parseInt(String s)
public static double sqrt(double a)

// C functions
printf("Hello, World!");
scanf("%d", &number);
strlen(string);
```

```python
# Python built-in functions
print("Hello")
len("Hello")
max(1, 2, 3)

# User-defined functions
def calculate_tax(income, rate):
    return income * rate
```

### Methods

Methods are special types of functions that "belong to" objects or classes. They must be called through an object and typically work with data contained within that object. This is a core concept of object-oriented programming (OOP).

Characteristics:
- Belong to objects or classes
- Called using dot notation (object.method())
- Often work with object's internal data
- Can access object's properties and other methods

Examples:
```java
// Java object methods
String text = "Hello";
String upperText = text.toUpperCase();  // toUpperCase() is a method of String
int length = text.length();             // length() is a method of String

List<String> list = new ArrayList<>();
list.add("item");                       // add() is a method of List
int size = list.size();                 // size() is a method of List
```

```python
# Python object methods
my_name = "Alice"
uppercase_name = my_name.upper()        # upper() is a method of string object
lowercase_name = my_name.lower()        # lower() is a method of string object

my_list = [1, 2, 3]
my_list.append(4)                       # append() is a method of list object
count = my_list.count(2)                # count() is a method of list object
```

### Comparison Table

| Aspect | Functions | Methods |
|--------|-----------|---------|
| Independence | Standalone, independent | Belong to objects/classes |
| Calling | Direct by name | Through object (object.method()) |
| Data Access | Only through parameters | Can access object's data |
| Programming Paradigm | Procedural, Functional | Object-Oriented |
| Example | `print("Hello")` | `text.upper()` |

### When to Use Each

Use Functions When:
- Performing utility operations
- Mathematical calculations
- Operations that don't depend on object state
- Working in procedural or functional paradigms

Use Methods When:
- Operating on object data
- Behavior specific to a type of object
- Working in object-oriented paradigms
- Need to maintain object state

## 5. Practical Examples and Applications

### Example 1: Mathematical Utility Functions

```java
public class MathUtils {
    
    // Function to calculate factorial
    public static long factorial(int n) {
        if (n < 0) return -1;  // Error case
        if (n == 0 || n == 1) return 1;  // Base case
        
        long result = 1;
        for (int i = 2; i <= n; i++) {
            result *= i;
        }
        return result;
    }
    
    // Function to check if a number is prime
    public static boolean isPrime(int number) {
        if (number < 2) return false;
        if (number == 2) return true;
        if (number % 2 == 0) return false;
        
        for (int i = 3; i <= Math.sqrt(number); i += 2) {
            if (number % i == 0) return false;
        }
        return true;
    }
    
    // Function to find greatest common divisor
    public static int gcd(int a, int b) {
        while (b != 0) {
            int temp = b;
            b = a % b;
            a = temp;
        }
        return a;
    }
    
    public static void main(String[] args) {
        // Using the functions
        System.out.println("5! = " + factorial(5));           // 120
        System.out.println("Is 17 prime? " + isPrime(17));    // true
        System.out.println("GCD(48, 18) = " + gcd(48, 18));   // 6
    }
}
```

### Example 2: String Processing Functions

```java
public class StringProcessor {
    
    // Function to count vowels in a string
    public static int countVowels(String text) {
        if (text == null) return 0;
        
        int count = 0;
        String vowels = "aeiouAEIOU";
        
        for (int i = 0; i < text.length(); i++) {
            if (vowels.indexOf(text.charAt(i)) != -1) {
                count++;
            }
        }
        return count;
    }
    
    // Function to reverse words in a sentence
    public static String reverseWords(String sentence) {
        if (sentence == null || sentence.trim().isEmpty()) {
            return sentence;
        }
        
        String[] words = sentence.split(" ");
        StringBuilder reversed = new StringBuilder();
        
        for (int i = words.length - 1; i >= 0; i--) {
            reversed.append(words[i]);
            if (i > 0) reversed.append(" ");
        }
        
        return reversed.toString();
    }
    
    // Function to capitalize first letter of each word
    public static String titleCase(String text) {
        if (text == null || text.isEmpty()) return text;
        
        StringBuilder result = new StringBuilder();
        boolean capitalizeNext = true;
        
        for (char c : text.toCharArray()) {
            if (Character.isLetter(c)) {
                if (capitalizeNext) {
                    result.append(Character.toUpperCase(c));
                    capitalizeNext = false;
                } else {
                    result.append(Character.toLowerCase(c));
                }
            } else {
                result.append(c);
                capitalizeNext = true;
            }
        }
        
        return result.toString();
    }
    
    public static void main(String[] args) {
        String text = "hello world programming";
        
        System.out.println("Original: " + text);
        System.out.println("Vowel count: " + countVowels(text));
        System.out.println("Reversed words: " + reverseWords(text));
        System.out.println("Title case: " + titleCase(text));
    }
}
```

### Example 3: Input Validation Functions

```java
import java.util.Scanner;

public class InputValidator {
    
    // Function to get valid integer within range
    public static int getIntegerInRange(Scanner scanner, String prompt, int min, int max) {
        int value;
        do {
            System.out.print(prompt + " (" + min + "-" + max + "): ");
            while (!scanner.hasNextInt()) {
                System.out.println("Please enter a valid number.");
                System.out.print(prompt + " (" + min + "-" + max + "): ");
                scanner.next(); // consume invalid input
            }
            value = scanner.nextInt();
            
            if (value < min || value > max) {
                System.out.println("Number must be between " + min + " and " + max);
            }
        } while (value < min || value > max);
        
        return value;
    }
    
    // Function to validate email format (basic)
    public static boolean isValidEmail(String email) {
        if (email == null || email.trim().isEmpty()) {
            return false;
        }
        
        // Basic email validation
        return email.contains("@") && 
               email.indexOf("@") > 0 && 
               email.indexOf("@") < email.length() - 1 &&
               email.contains(".") &&
               email.lastIndexOf(".") > email.indexOf("@");
    }
    
    // Function to get valid email from user
    public static String getValidEmail(Scanner scanner) {
        String email;
        do {
            System.out.print("Enter email address: ");
            email = scanner.nextLine().trim();
            
            if (!isValidEmail(email)) {
                System.out.println("Invalid email format. Please try again.");
            }
        } while (!isValidEmail(email));
        
        return email;
    }
    
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        int age = getIntegerInRange(scanner, "Enter your age", 1, 120);
        String email = getValidEmail(scanner);
        
        System.out.println("Age: " + age);
        System.out.println("Email: " + email);
        
        scanner.close();
    }
}
```

## 6. Function Design Principles

### Single Responsibility Principle

Each function should have one clear, well-defined purpose:

```java
// Good - Single responsibility
public static double calculateTax(double income, double rate) {
    return income * rate;
}

public static void printTaxReport(String name, double income, double tax) {
    System.out.println("Tax Report for " + name);
    System.out.println("Income: $" + income);
    System.out.println("Tax: $" + tax);
}

// Poor - Multiple responsibilities
public static void calculateAndPrintTax(String name, double income, double rate) {
    double tax = income * rate;  // Calculation responsibility
    System.out.println("Tax Report for " + name);  // Printing responsibility
    System.out.println("Income: $" + income);
    System.out.println("Tax: $" + tax);
}
```

### Function Length and Complexity

Keep functions short and focused:

```java
// Good - Short and focused
public static boolean isLeapYear(int year) {
    return (year % 4 == 0 && year % 100 != 0) || (year % 400 == 0);
}

// Good - Broken into smaller functions
public static String formatPhoneNumber(String digits) {
    if (!isValidPhoneDigits(digits)) {
        return "Invalid phone number";
    }
    return formatAsPhoneNumber(digits);
}

private static boolean isValidPhoneDigits(String digits) {
    return digits != null && digits.length() == 10 && digits.matches("\\d+");
}

private static String formatAsPhoneNumber(String digits) {
    return "(" + digits.substring(0, 3) + ") " + 
           digits.substring(3, 6) + "-" + 
           digits.substring(6);
}
```

### Error Handling in Functions

```java
public static double divide(double a, double b) {
    if (b == 0) {
        throw new IllegalArgumentException("Division by zero is not allowed");
    }
    return a / b;
}

public static String getFileExtension(String filename) {
    if (filename == null || filename.trim().isEmpty()) {
        return "";
    }
    
    int lastDotIndex = filename.lastIndexOf('.');
    if (lastDotIndex == -1 || lastDotIndex == filename.length() - 1) {
        return "";
    }
    
    return filename.substring(lastDotIndex + 1);
}
```

---

## 📋 Summary & Practical Exercise

### Comprehensive Summary

Functions are named blocks of reusable code that serve as the primary tool for abstraction and following the DRY (Don't Repeat Yourself) principle. They consist of:

Function Components:
- Function name: Identifier used to call the function
- Parameters: Input slots that receive arguments when the function is called
- Function body: Block of code that executes when the function is called
- Return statement: Sends results back to the calling code

Key Concepts:
- Parameters vs Arguments: Parameters are placeholders in function definition; arguments are actual values passed when calling
- Function signature: The interface (name, parameters, return type) that defines how to use the function
- Scope: Variables defined within functions exist only within that function
- Reusability: Functions can be called multiple times with different arguments

Functions vs Methods:
- Functions: Independent, standalone code blocks (procedural/functional programming)
- Methods: Functions that belong to objects or classes (object-oriented programming)
- Functions are called directly by name; methods are called through objects using dot notation

Benefits:
- Code reusability and reduced duplication
- Improved maintainability and bug fixing
- Better code organization and readability
- Easier testing and debugging
- Modular development and team collaboration

Design Principles:
- Single responsibility: Each function should do one thing well
- Clear naming: Function names should describe what they do
- Appropriate length: Functions should be short and focused
- Proper error handling: Handle edge cases and invalid inputs
- Consistent interfaces: Similar functions should follow similar patterns

### Practical Exercise

You need to write code that checks whether a given number is "even" or not. Design and implement this functionality:

1) Design a function named `isEven` that takes one number as a parameter
2) What logic should be inside the function to check if a number is even? (Hint: use the modulus operator %)
3) What data type should this function return?

#### Step-by-Step Solution:

Step 1: Function Design Analysis

Function Purpose: Determine if a number is even
Input: One integer number
Output: Boolean value (true if even, false if odd)
Logic: A number is even if it's divisible by 2 (remainder is 0)

Step 2: Implementation in Different Languages

Java Implementation:
```java
public static boolean isEven(int number) {
    return number % 2 == 0;
}

// Usage examples
public static void main(String[] args) {
    System.out.println(isEven(4));   // true
    System.out.println(isEven(7));   // false
    System.out.println(isEven(0));   // true
    System.out.println(isEven(-2));  // true
    System.out.println(isEven(-3));  // false
}
```

Python Implementation:
```python
def is_even(number):
    return number % 2 == 0

# Usage examples
print(is_even(4))   # True
print(is_even(7))   # False
print(is_even(0))   # True
print(is_even(-2))  # True
print(is_even(-3))  # False
```

C Implementation:
```c
#include <stdio.h>
#include <stdbool.h>

bool isEven(int number) {
    return number % 2 == 0;
}

int main() {
    printf("%d\n", isEven(4));   // 1 (true)
    printf("%d\n", isEven(7));   // 0 (false)
    return 0;
}
```

Step 3: Analysis Questions and Answers

1) Function Design:
   - Function name: `isEven` (clear, descriptive, follows naming conventions)
   - Parameter: `int number` (takes one integer parameter)
   - Return type: `boolean` (true/false result)

2) Internal Logic:
   - Use modulus operator (%) to find remainder when divided by 2
   - If remainder is 0, the number is even
   - If remainder is 1, the number is odd
   - Expression: `number % 2 == 0`

3) Return Data Type:
   - Should return `boolean` (true/false)
   - This makes the function's purpose clear and enables use in conditional statements

Step 4: Extended Implementation with Input Validation

```java
public static boolean isEven(int number) {
    // Basic implementation
    return number % 2 == 0;
}

// Enhanced version with validation and user interaction
public static void checkEvenNumbers() {
    Scanner scanner = new Scanner(System.in);
    
    System.out.print("Enter a number to check if it's even: ");
    int number = scanner.nextInt();
    
    if (isEven(number)) {
        System.out.println(number + " is an even number.");
    } else {
        System.out.println(number + " is an odd number.");
    }
}

// Function to check multiple numbers
public static void analyzeNumbers(int[] numbers) {
    int evenCount = 0;
    int oddCount = 0;
    
    System.out.println("Number Analysis:");
    for (int number : numbers) {
        if (isEven(number)) {
            System.out.println(number + " is even");
            evenCount++;
        } else {
            System.out.println(number + " is odd");
            oddCount++;
        }
    }
    
    System.out.println("Summary: " + evenCount + " even, " + oddCount + " odd");
}
```

Step 5: Testing the Function

```java
public static void testIsEvenFunction() {
    // Test cases
    int[] testNumbers = {0, 1, 2, -1, -2, 100, 101};
    
    System.out.println("Testing isEven function:");
    for (int number : testNumbers) {
        boolean result = isEven(number);
        System.out.println("isEven(" + number + ") = " + result);
    }
}

// Expected output:
// isEven(0) = true
// isEven(1) = false
// isEven(2) = true
// isEven(-1) = false
// isEven(-2) = true
// isEven(100) = true
// isEven(101) = false
```

This exercise demonstrates the complete process of function design, implementation, and testing, while reinforcing the concepts of parameters, return values, and logical operations within functions.

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
