# 📖 Topic: Debugging

## 💡 Basic knowledge required

- A written piece of code that may contain latent errors.
- Understanding the difference between syntax errors and runtime errors (from Section 3).

## 🎯 Learning Objectives

- Define "Debugging" as the systematic process of identifying, locating, and fixing defects (Bugs).
- Differentiate between Debugging and Testing.
- Describe common debugging techniques, particularly Print Debugging and using an Interactive Debugger.
- Understand the importance of a systematic, hypothesis-driven approach to debugging.

---

### 1. Introduction: The Art of Diagnosis

Debugging is the systematic process of finding and reducing the number of bugs, or defects, in a computer program to make it behave as expected. It is one of the most critical investigative skills a programmer possesses.

#### Testing vs. Debugging

It is crucial to separate these two activities:

-   Testing asks: "Does a bug exist?" Its goal is to find evidence that the program is behaving incorrectly.
-   Debugging asks: "Where is the bug, and why is it happening?" Its goal is to find the root cause of the failure and fix it. Debugging begins after testing has discovered a problem.

### 2. The Debugging Mindset: A Scientific Approach

Effective debugging is not random guesswork but a disciplined process similar to the scientific method:

```
+-----------------+
| Observe &       |
| Reproduce Bug   |
+-----------------+
        |
        v
+-----------------+
| Formulate       |
| Hypothesis      |
+-----------------+
        |
        v
+-----------------+
| Design & Run    |
| Experiment      |
+-----------------+
        |
        v
+-----------------+
| Analyze & Fix   |
+-----------------+
```

1.  Observe & Reproduce: Observe the bug's symptoms and, most importantly, find a reliable way to make it happen again. If you cannot reproduce the bug, you cannot fix it.
2.  Formulate a Hypothesis: Based on the evidence, make a plausible guess about the cause. e.g., "I suspect the `user_id` variable is becoming null in this function."
3.  Design an Experiment: Find a way to test your hypothesis. This could be adding a `print()` statement, using a debugger to inspect a value, or trying a small code change.
4.  Execute & Analyze: Run the experiment and analyze the result. Does it confirm your hypothesis? If yes, proceed to the fix. If no, you have learned new information. Form a new hypothesis and repeat.

### 3. Common Debugging Techniques

#### Print Debugging (or Logging)

-   Description: The simplest and most universal technique. It involves inserting `print()` or `log()` statements at various points in the code to display variable values and trace the program's execution flow.
-   Pros/Cons: It is fast and works in any environment, but it clutters the code, must be removed later, and can be inconvenient for complex problems.

#### Interactive Debugger

-   Description: A powerful, specialized tool often integrated into an IDE (from lesson 6.1). It allows us to "control" the program's execution.

```
+----------------------+
| Interactive Debugger |
|----------------------|
| > Set Breakpoints    |
| > Step through code  |
| > Inspect variables  |
| > Analyze call stack |
+----------------------+
```

-   Key Capabilities:
    -   Breakpoints: Command the program to "pause" at a specific line.
    -   Stepping: Execute the program one line at a time (Step Over, Step Into, Step Out) to observe behavior in detail.
    -   Variable Inspection: View the value of any variable while the program is paused.
    -   Call Stack Analysis: See the sequence of function calls that led to the current point of failure.

Conclusion: Using a debugger is a much more professional and efficient method than print debugging.

---

## 📋 Comprehensive Summary & Practical Exercise

### Comprehensive Summary

Debugging is the systematic process of finding and fixing bugs, which begins after testing finds a problem. Good debugging relies on a scientific approach (observe, hypothesize, experiment). The most powerful tool for this is an Interactive Debugger, which allows for detailed control and inspection of a program's execution.

### Practical Exercise

Assume your function should apply a 10% discount for items priced over 1,000, but you find it's discounting every item. You suspect the condition `if (price > 1000)` is not working as expected.
1.  If using an Interactive Debugger, on which line would you set a breakpoint? What variable's value would you inspect?
2.  How would you prove or disprove your hypothesis?

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
