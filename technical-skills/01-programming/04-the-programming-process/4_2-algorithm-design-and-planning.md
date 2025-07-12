# 📖 Topic: Algorithm Design and Planning

## 💡 Basic knowledge required

- A clear understanding of program requirements (from lesson 4.1).
- Computational thinking skills, especially problem decomposition and abstraction (from section 2).

## 🎯 Learning Objectives

- Define "algorithm design" as the process of creating a plan to solve a computational problem.
- Understand the characteristics of a good algorithm (correct, efficient, readable).
- Identify and describe tools used for planning algorithms, such as Pseudocode and Flowcharts.
- Apply the planning process to create an algorithm from given requirements.

---

### 1. Introduction: From "What" to "How"

In the previous lesson on Requirement Analysis, we established a clear answer to "WHAT" the system must do. In this lesson, we will focus on answering the question, "HOW to do it."

Algorithm Design is the activity of creating a clear, step-by-step, and finite computational process that takes some value as input and produces some value as output. It is the "logical blueprint" for the software we will build and is a crucial step before starting to write code.

### 2. Characteristics of a Good Algorithm

A good algorithm is not just one that "works," but one that exhibits several key properties:

- **Correctness**: This is the most important attribute. The algorithm must produce the correct output for all possible inputs as defined by the requirements.
- **Efficiency**: It should use resources, such as CPU processing time and memory space, as minimally as possible.
- **Readability & Maintainability**: The logic of the algorithm should be clear and easy for humans to understand, allowing for easier modification, debugging, or extension in the future.
- **Finiteness**: The algorithm must terminate after a finite number of steps.
- **Unambiguity**: Each step must be precisely defined and have only one interpretation.

### 3. Tools for Planning and Representing Algorithms

Before writing actual code, programmers often use these tools to draft and refine their ideas:

#### Pseudocode

- **Description**: An explanation of an algorithm's logic using a language that resembles a programming language but is less formal and not tied to the syntax of any specific language.
- **Objective**: To focus solely on the problem-solving logic without worrying about the complex syntax of a programming language.
- **Example (Checking for a prime number)**:
```
FUNCTION is_prime(number n)
  IF n <= 1 THEN 
    RETURN false
  
  FOR i FROM 2 TO square_root(n)
    IF n % i == 0 THEN
      RETURN false
  END FOR
  
  RETURN true
END FUNCTION
```

#### Flowchart

- **Description**: A diagram that uses standard symbols (e.g., rectangles for processes, diamonds for decisions) connected by arrows to show the "flow" of control and logic.
- **Objective**: To provide a visual overview of the logic and decision points, making it suitable for explaining complex algorithms to non-programmers.
- **ASCII Example (Simple Decision Flow)**:
```
      +------------------+
      |      Start       |
      +--------+---------+
               |
               v
+--------------------------------+
| Get number 'n' from user       |
+----------------+---------------+
                 |
                 v
      +------------------+
      |   Is n > 0 ?     |----(No)---->+-------------------+
      +--------+---------+             | Print "Negative"  |
               |                       +-------------------+
             (Yes)                             |
               |                               v
               v                       +------------------+
      +-------------------+            |       End        |
      | Print "Positive"  |            +------------------+
      +-------------------+
               |
               v
      +------------------+
      |       End        |
      +------------------+
```

### 4. The Practical Planning Process

1.  **Understand the Requirements**: Clearly define the problem, identifying the inputs and the expected outputs.
2.  **Decompose the Problem**: Break the large problem down into smaller, more manageable sub-problems.
3.  **Choose Data Structures**: Decide how to store and organize data (e.g., using an Array, List, Dictionary), as this choice directly impacts the algorithm.
4.  **Draft the Algorithm**: Use pseudocode or flowcharts to outline the sequence of logical steps for solving each sub-problem.
5.  **Refine and Analyze**: Review the drafted algorithm. Is it correct? Does it cover all edge cases? Is it reasonably efficient? Can it be simplified?

---

## 📋 Comprehensive Summary & Practical Exercise

### Comprehensive Summary

Algorithm design is the process of creating a logical blueprint before coding. A good algorithm must be correct, efficient, and understandable. Key planning tools include Pseudocode, for outlining logic without strict syntax, and Flowcharts, for visualizing the process flow.

### Practical Exercise

For the problem "find the average of all numbers in a list":
1.  What is your input? What is the expected output?
2.  Try to write "Pseudocode" to describe the steps for calculating this average.

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
