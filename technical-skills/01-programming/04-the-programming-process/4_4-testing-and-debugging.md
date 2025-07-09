# 📖 Testing and Debugging

## 💡 Basic knowledge required:

Having working code or code components that have been implemented (from lesson 4.3)
Understanding of program logic and potential errors that may occur

## 🎯 Learning Objectives

Upon completion of this topic, you will be able to:

- Define "software testing" and explain its purpose in verifying and validating correctness
- Distinguish between important testing levels: Unit Testing, Integration Testing, and System Testing
- Define "debugging" as the process of finding and fixing defects
- Identify common debugging techniques such as print statements and interactive debuggers

---

## 1. Introduction: The Pursuit of Correctness

Getting code to run is only half the work. Just because a program runs without crashing doesn't mean it produces correct results in all situations. Testing and Debugging are two different but closely related activities used to ensure software quality.

**Testing**: The process of "finding" whether bugs exist and where they are located. The goal of testing is to try to break the program or make it behave incorrectly.

**Debugging**: The process of "finding the cause and fixing" the errors that testing has discovered.

### Testing vs Debugging Relationship

```
Software Quality Assurance Process
==================================

Implementation → Testing → Bug Found? → Debugging → Fix Applied
     ↑                        │                         │
     │                        ▼                         │
     │                   No Bugs Found                  │
     │                        │                         │
     │                        ▼                         │
     └────────────── Quality Software ←─────────────────┘

Key Differences:
┌─────────────────────────────────────────┐
│ Testing (Bug Detection):                │
│ • Systematic verification process       │
│ • Attempts to find problems             │
│ • Demonstrates presence of bugs         │
│ • Can prove incorrectness               │
│                                         │
│ Debugging (Bug Resolution):             │
│ • Investigation and repair process      │
│ • Locates root causes                   │
│ • Fixes identified problems             │
│ • Restores correct behavior             │
└─────────────────────────────────────────┘

Working Together:
Testing finds the symptoms → Debugging finds the disease → Fix cures the problem
```

### The Reality of Software Defects

```
Why Testing and Debugging are Essential
=======================================

Perfect Code Myth vs Reality:
┌─────────────────────────────────────────┐
│ Programmer Expectation:                 │
│ "My code works because it compiles      │
│  and runs without errors"               │
│                                         │
│ Reality Check:                          │
│ • Code may work for happy path only     │
│ • Edge cases often reveal bugs          │
│ • Integration issues appear later       │
│ • Real user data exposes problems       │
│                                         │
│ Industry Statistics:                    │
│ • Average: 15-50 defects per 1000 lines │
│ • Even experienced developers introduce │
│   bugs regularly                        │
│ • 80% of defects found in 20% of code   │
└─────────────────────────────────────────┘

Cost of Defects by Discovery Phase:
┌─────────────────────────────────────────┐
│ Development Phase:    $1 to fix         │
│ Testing Phase:        $10 to fix        │
│ Production Phase:     $100 to fix       │
│ Customer Impact:      $1000+ to fix     │
│                                         │
│ Lesson: Find bugs early through         │
│ systematic testing and debugging        │
└─────────────────────────────────────────┘
```

## 2. Software Testing: A Systematic Approach

Software Testing is a systematic process for evaluating software quality to provide information to stakeholders. Testing is typically divided into different levels based on scope, often presented as a "Testing Pyramid."

### The Testing Pyramid

```
Testing Pyramid Structure
=========================

                    /\
                   /  \
                  /    \
                 /System\      ← Few tests, high scope
                /Testing \      • End-to-end workflows
               /──────────\     • User interface testing
              /Integration \    ← Medium tests, medium scope  
             / Testing      \   • Component interactions
            /________________\  • API testing
           /   Unit Testing   \  ← Many tests, low scope
          /____________________\  • Function-level testing
                                  • Fast execution

Foundation Principle: Many fast, focused tests
Peak Principle: Few comprehensive, slow tests

Benefits of Pyramid Structure:
┌─────────────────────────────────────────┐
│ • Fast feedback from unit tests         │
│ • Comprehensive coverage at all levels  │
│ • Cost-effective bug detection          │
│ • Maintainable test suite               │
│ • Clear testing responsibilities        │
└─────────────────────────────────────────┘
```

### A. Unit Testing

**Scope**: Testing the "smallest testable unit" of software, typically individual functions or methods in isolation.

**Goal**: To verify that each code unit works correctly as designed.

**Characteristics**: Fast execution, isolated environment, focused validation.

```
Unit Test Example Structure
===========================

Test Function: isEven()
├── Test Case 1: isEven(4) → Expected: true
├── Test Case 2: isEven(5) → Expected: false  
├── Test Case 3: isEven(0) → Expected: true (edge case)
├── Test Case 4: isEven(-2) → Expected: true (negative even)
└── Test Case 5: isEven(-3) → Expected: false (negative odd)

Unit Test Categories:
┌─────────────────────────────────────────┐
│ Normal Cases (Happy Path):              │
│ • Typical input values                  │
│ • Expected usage scenarios              │
│ • Common data ranges                    │
│                                         │
│ Edge Cases (Boundary Conditions):       │
│ • Minimum/maximum values                │
│ • Empty inputs, null values             │
│ • Zero, negative numbers                │
│                                         │
│ Error Cases (Exception Handling):       │
│ • Invalid input types                   │
│ • Out-of-range values                   │
│ • Resource unavailability               │
└─────────────────────────────────────────┘

Sample Unit Test Implementation:
┌─────────────────────────────────────────┐
│ // Java example using JUnit             │
│ @Test                                   │
│ public void testIsEvenWithPositiveNumbers() {
│     assertTrue(isEven(4));              │
│     assertFalse(isEven(5));             │
│     assertTrue(isEven(2));              │
│ }                                       │
│                                         │
│ @Test                                   │
│ public void testIsEvenWithEdgeCases() { │
│     assertTrue(isEven(0));  // Zero     │
│     assertTrue(isEven(-4)); // Negative │
│     assertFalse(isEven(-3));            │
│ }                                       │
│                                         │
│ @Test(expected = IllegalArgumentException.class)
│ public void testIsEvenWithInvalidInput() {
│     isEven(null); // Should throw exception
│ }                                       │
└─────────────────────────────────────────┘
```

### B. Integration Testing

**Scope**: Testing the "collaboration" between multiple units or modules.

**Goal**: To find errors that occur at the "interfaces" or interactions between different components.

**Focus Areas**: Data flow, communication protocols, shared resources.

```
Integration Testing Scenarios
=============================

E-commerce Checkout Example:
┌─────────────────────────────────────────┐
│ checkout() function integration:        │
│                                         │
│ 1. Input Validation Module              │
│    ↓ (user data)                        │
│ 2. Inventory Check Module               │
│    ↓ (availability confirmation)        │
│ 3. Payment Processing Module            │
│    ↓ (payment authorization)            │
│ 4. Order Creation Module                │
│    ↓ (order details)                    │
│ 5. Email Notification Module            │
│                                         │
│ Integration Test Cases:                 │
│ • Does checkout() pass correct data     │
│   to processPayment()?                  │
│ • Does processPayment() return proper   │
│   confirmation to updateInventory()?    │
│ • Are email notifications triggered     │
│   only after successful payment?        │
│ • How does system handle payment        │
│   failures during inventory update?     │
└─────────────────────────────────────────┘

Types of Integration Testing:
┌─────────────────────────────────────────┐
│ Big Bang Integration:                   │
│ • All modules combined simultaneously   │
│ • Fast but hard to isolate problems     │
│                                         │
│ Incremental Integration:                │
│ • Modules added one at a time           │
│ • Top-down or bottom-up approach        │
│ • Easier problem isolation              │
│                                         │
│ API Integration Testing:                │
│ • Focus on service-to-service calls     │
│ • Verify data contracts                 │
│ • Test error handling between services  │
└─────────────────────────────────────────┘
```

### C. System Testing

**Scope**: Testing the complete, fully integrated software system.

**Goal**: To verify that the overall system can perform according to requirements (both functional and non-functional) from an end-user perspective.

**Perspective**: Black-box testing from user's viewpoint.

```
System Testing Workflow Example
===============================

Online Banking System Test:
┌─────────────────────────────────────────┐
│ Complete User Journey:                  │
│                                         │
│ 1. User Login                           │
│    • Authentication validation          │
│    • Security token generation          │
│    • Session management                 │
│                                         │
│ 2. Account Navigation                   │
│    • Account balance display            │
│    • Transaction history loading        │
│    • Multiple account access            │
│                                         │
│ 3. Money Transfer                       │
│    • Recipient validation               │
│    • Transfer amount verification       │
│    • Real-time balance updates          │
│                                         │
│ 4. Transaction Confirmation             │
│    • Email/SMS notifications            │
│    • Receipt generation                 │
│    • Audit trail creation               │
│                                         │
│ 5. Logout Process                       │
│    • Session termination                │
│    • Security cleanup                   │
│    • Activity logging                   │
└─────────────────────────────────────────┘

System Test Categories:
┌─────────────────────────────────────────┐
│ Functional System Tests:                │
│ • Feature completeness                  │
│ • Business rule validation              │
│ • User workflow verification            │
│                                         │
│ Non-Functional System Tests:            │
│ • Performance under load                │
│ • Security vulnerability scanning       │
│ • Usability and accessibility           │
│ • Compatibility across platforms        │
│                                         │
│ Acceptance Testing:                     │
│ • User acceptance criteria              │
│ • Business requirement satisfaction     │
│ • Production readiness assessment       │
└─────────────────────────────────────────┘
```

## 3. Debugging: The Art of Diagnosis

Debugging is an investigative process to identify problem locations, isolate root causes, and fix those errors. It requires systematic thinking, patience, and methodical problem-solving skills.

### Understanding the Debugging Mindset

```
Debugging as Scientific Investigation
====================================

The Debugging Process:
┌─────────────────────────────────────────┐
│ 1. Observe the Problem                  │
│    • What is the expected behavior?     │
│    • What actually happens?             │
│    • Can you reproduce the issue?       │
│                                         │
│ 2. Form Hypotheses                      │
│    • What could cause this behavior?    │
│    • Which components are involved?     │
│    • What are the most likely causes?   │
│                                         │
│ 3. Design Experiments                   │
│    • How can you test each hypothesis?  │
│    • What data do you need to collect?  │
│    • What tools will help investigation?│
│                                         │
│ 4. Collect Evidence                     │
│    • Run targeted tests                 │
│    • Examine variable values            │
│    • Trace execution flow               │
│                                         │
│ 5. Analyze Results                      │
│    • Does evidence support hypothesis?  │
│    • What can you rule out?             │
│    • What new questions arise?          │
│                                         │
│ 6. Implement Fix                        │
│    • Address root cause, not symptoms   │
│    • Verify fix resolves issue          │
│    • Ensure no new problems introduced  │
└─────────────────────────────────────────┘

Common Debugging Mistakes:
┌─────────────────────────────────────────┐
│ • Changing multiple things at once      │
│ • Fixing symptoms instead of causes     │
│ • Not reproducing the problem first     │
│ • Assuming rather than verifying        │
│ • Giving up too quickly                 │
│ • Not documenting the solution          │
└─────────────────────────────────────────┘
```

### A. Print Debugging

The simplest technique: inserting `print()` statements at various points in code to display variable values and track execution flow. This method is quick but can make code messy and requires cleanup afterward.

```
Print Debugging Strategy
========================

Strategic Print Statement Placement:
┌─────────────────────────────────────────┐
│ function calculateAverage(numbers) {    │
│     console.log("Input:", numbers);     │ ← Entry point
│                                         │
│     if (numbers.length === 0) {         │
│         console.log("Empty array detected");
│         return 0;                       │
│     }                                   │
│                                         │
│     let sum = 0;                        │
│     for (let i = 0; i < numbers.length; i++) {
│         sum += numbers[i];              │
│         console.log(`After adding ${numbers[i]}: sum = ${sum}`);
│     }                                   │ ← Loop progress
│                                         │
│     let average = sum / numbers.length; │
│     console.log("Final calculation:",   │
│                 `${sum} / ${numbers.length} = ${average}`);
│     return average;                     │ ← Final result
│ }                                       │
│                                         │
│ Debug Session Output:                   │
│ Input: [10, 20, 30]                     │
│ After adding 10: sum = 10               │
│ After adding 20: sum = 30               │
│ After adding 30: sum = 60               │
│ Final calculation: 60 / 3 = 20          │
│                                         │
│ Problem: If output shows 15 instead     │
│ of 20, check division logic!            │
└─────────────────────────────────────────┘

Print Debugging Best Practices:
┌─────────────────────────────────────────┐
│ Effective Techniques:                   │
│ • Use descriptive prefixes              │
│   print("DEBUG: variable =", value)     │
│ • Include context information           │
│   print(f"Loop iteration {i}: sum = {sum}")
│ • Print before and after critical ops   │
│   print("Before calculation:", values)  │
│   result = calculate(values)            │
│   print("After calculation:", result)   │
│                                         │
│ Clean-up Strategy:                      │
│ • Use consistent debug prefixes         │
│ • Consider conditional debug flags      │
│   if DEBUG: print("Debug info")         │
│ • Remove or comment out when done       │
│                                         │
│ Limitations:                            │
│ • Makes code messy                      │
│ • Time-consuming for complex issues     │
│ • May affect program performance        │
│ • Difficult in multi-threaded code      │
└─────────────────────────────────────────┘
```

### B. Interactive Debugger

A powerful tool available in most IDEs that allows you to control program execution and inspect program state in real-time.

```
Interactive Debugger Features
=============================

Core Debugger Capabilities:
┌─────────────────────────────────────────┐
│ Breakpoint Management:                  │
│ • Pause execution at specific lines     │
│ • Conditional breakpoints               │
│   (break only when condition is true)   │
│ • Temporary breakpoints                 │
│                                         │
│ Execution Control:                      │
│ • Step Over: Execute current line       │
│ • Step Into: Enter function calls       │
│ • Step Out: Exit current function       │
│ • Continue: Run until next breakpoint   │
│                                         │
│ State Inspection:                       │
│ • Variable values and types             │
│ • Object property examination           │
│ • Array/collection contents             │
│ • Memory usage information              │
│                                         │
│ Call Stack Analysis:                    │
│ • Function call hierarchy               │
│ • Parameter values at each level        │
│ • Return path tracing                   │
└─────────────────────────────────────────┘

Debugger Interface Layout:
┌─────────────────────────────────────────┐
│ Code Editor with Breakpoints:           │
│ 1: function calculateAverage(numbers) { │
│ 2: ●   if (numbers.length === 0) {      │ ← Breakpoint
│ 3:         return 0;                    │
│ 4:     }                                │
│ 5: ●   let sum = 0;                     │ ← Breakpoint
│ 6:     for (let i = 0; i < numbers.length; i++) {
│ 7:         sum += numbers[i];           │
│ 8:     }                                │
│ 9: ●   return sum / numbers.length;     │ ← Breakpoint
├─────────────────────────────────────────┤
│ Variable Inspector:                     │
│ numbers = [10, 20, 30]                  │
│ sum = 30                                │
│ i = 1                                   │
│ numbers.length = 3                      │
├─────────────────────────────────────────┤
│ Call Stack:                             │
│ → calculateAverage(numbers)             │
│   main()                                │
│   <global>                              │
├─────────────────────────────────────────┤
│ Console/Watch:                          │
│ sum / numbers.length = ?                │
│ numbers[i] = 20                         │
└─────────────────────────────────────────┘

Advanced Debugging Techniques:
┌─────────────────────────────────────────┐
│ Conditional Breakpoints:                │
│ • Break only when i > 5                 │
│ • Break when variable equals null       │
│ • Break on exception conditions         │
│                                         │
│ Watch Expressions:                      │
│ • Monitor specific variable changes     │
│ • Track complex expression values       │
│ • Set alerts for unexpected values      │
│                                         │
│ Memory and Performance:                 │
│ • Memory usage tracking                 │
│ • Performance profiling                 │
│ • Resource leak detection               │
└─────────────────────────────────────────┘
```

### Debugging Common Problem Types

```
Systematic Problem Solving
==========================

Algorithm Logic Errors:
┌─────────────────────────────────────────┐
│ Problem: Wrong calculation result       │
│                                         │
│ Debug Strategy:                         │
│ 1. Verify input values are correct      │
│ 2. Trace through calculation steps      │
│ 3. Check mathematical operations        │
│ 4. Validate intermediate results        │
│ 5. Confirm output formatting            │
│                                         │
│ Common Causes:                          │
│ • Off-by-one errors in loops            │
│ • Integer division vs float division    │
│ • Operator precedence mistakes          │
│ • Variable reuse/overwriting            │
└─────────────────────────────────────────┘

Loop and Iteration Issues:
┌─────────────────────────────────────────┐
│ Problem: Infinite loops or wrong counts │
│                                         │
│ Debug Strategy:                         │
│ 1. Check loop initialization            │
│ 2. Verify loop condition logic          │
│ 3. Confirm loop variable updates        │
│ 4. Test with boundary values            │
│                                         │
│ Common Causes:                          │
│ • Condition never becomes false         │
│ • Loop variable not properly updated    │
│ • Wrong comparison operators            │
│ • Nested loop variable conflicts        │
└─────────────────────────────────────────┘

Data Structure Problems:
┌─────────────────────────────────────────┐
│ Problem: Incorrect data access/storage  │
│                                         │
│ Debug Strategy:                         │
│ 1. Verify data structure initialization │
│ 2. Check index/key validity             │
│ 3. Confirm data type compatibility      │
│ 4. Validate data modification operations│
│                                         │
│ Common Causes:                          │
│ • Array index out of bounds             │
│ • Null pointer/reference errors         │
│ • Wrong data type assumptions           │
│ • Improper object property access       │
└─────────────────────────────────────────┘
```

---

## 💡 Real-World Applications

### Professional Testing Strategy

```
Enterprise Testing Approach
===========================

Banking System Example:
┌─────────────────────────────────────────┐
│ Unit Tests (Foundation):                │
│ • calculateInterest() function          │
│ • validateAccountNumber() function      │
│ • formatCurrency() utility              │
│ • encryptPassword() security function   │
│                                         │
│ Integration Tests (Interactions):       │
│ • Account service ↔ Transaction service │
│ • Payment processor ↔ Bank API          │
│ • User interface ↔ Business logic       │
│ • Database ↔ Application layer          │
│                                         │
│ System Tests (End-to-End):              │
│ • Complete customer money transfer      │
│ • Account opening workflow              │
│ • Loan application process              │
│ • Mobile app synchronization            │
│                                         │
│ Test Coverage Goals:                    │
│ • Unit tests: 80%+ code coverage        │
│ • Integration: All critical interfaces  │
│ • System: 100% user scenarios           │
└─────────────────────────────────────────┘

Quality Assurance Metrics:
┌─────────────────────────────────────────┐
│ Defect Detection Effectiveness:         │
│ • Bugs found in testing vs production   │
│ • Time to identify and fix issues       │
│ • Customer-reported vs internal bugs    │
│                                         │
│ Test Automation Benefits:               │
│ • Faster feedback cycles                │
│ • Consistent test execution             │
│ • Regression testing efficiency         │
│ • Reduced manual testing costs          │
└─────────────────────────────────────────┘
```

### Debugging in Team Environment

```
Collaborative Debugging Process
===============================

Professional Bug Resolution Workflow:
┌─────────────────────────────────────────┐
│ 1. Bug Report Creation                  │
│    • Clear problem description          │
│    • Steps to reproduce                 │
│    • Expected vs actual behavior        │
│    • Environment information            │
│                                         │
│ 2. Initial Investigation                │
│    • Reproduce the issue locally        │
│    • Identify affected components       │
│    • Assess impact and priority         │
│                                         │
│ 3. Collaborative Analysis               │
│    • Share findings with team           │
│    • Consult domain experts             │
│    • Review related code changes        │
│                                         │
│ 4. Solution Development                 │
│    • Design fix with minimal risk       │
│    • Create focused test cases          │
│    • Implement and validate solution    │
│                                         │
│ 5. Quality Assurance                    │
│    • Peer code review                   │
│    • Comprehensive testing              │
│    • Documentation updates              │
│                                         │
│ 6. Deployment and Monitoring            │
│    • Staged rollout process             │
│    • Monitor for regressions            │
│    • Post-mortem analysis if needed     │
└─────────────────────────────────────────┘

Team Debugging Best Practices:
┌─────────────────────────────────────────┐
│ Knowledge Sharing:                      │
│ • Document debugging process            │
│ • Share effective techniques            │
│ • Maintain troubleshooting guides       │
│                                         │
│ Tool Standardization:                   │
│ • Common debugging environments         │
│ • Shared logging and monitoring         │
│ • Consistent error reporting            │
│                                         │
│ Skill Development:                      │
│ • Pair debugging sessions               │
│ • Code review with focus on testability │
│ • Regular debugging technique workshops │
└─────────────────────────────────────────┘
```

---

## 📋 Summary & Practical Exercise

### Comprehensive Summary

Testing and Debugging are complementary processes that ensure software quality and reliability. Testing systematically verifies that software meets requirements and functions correctly, while debugging investigates and resolves problems discovered during testing or production use.

Key Concepts:

Testing Strategy:
- Unit Testing validates individual components in isolation with fast, focused tests
- Integration Testing verifies component interactions and data flow between modules
- System Testing confirms complete functionality from end-user perspective
- Testing Pyramid emphasizes many unit tests, fewer integration tests, minimal system tests

Debugging Methodology:
- Print Debugging provides quick insight into program state and execution flow
- Interactive Debuggers offer powerful investigation tools with execution control
- Systematic debugging follows scientific method: observe, hypothesize, experiment, analyze
- Root cause analysis prevents symptom-only fixes that mask underlying problems

Professional Practices:
- Early testing reduces defect costs and improves development efficiency
- Automated testing enables consistent quality assurance and faster feedback
- Collaborative debugging leverages team knowledge and diverse perspectives
- Documentation and knowledge sharing prevent repeated debugging efforts

Quality Assurance:
- Comprehensive testing coverage ensures reliability across usage scenarios
- Proactive debugging prevents customer-impacting issues
- Continuous improvement of testing and debugging processes
- Balance between thorough validation and development velocity

Essential Insight: Testing and debugging are investments in software quality that pay dividends through reduced maintenance costs, improved user satisfaction, and team productivity. Mastering these skills transforms developers from code writers to quality engineers who create reliable, maintainable software systems.

### Practical Exercise: Debug the Average Function

Apply testing and debugging techniques to solve the classic average calculation problem mentioned in the lesson.

#### Exercise Steps:

**Scenario**: Your `calculateAverage(numbers)` function is behaving incorrectly. When you input the list `[10, 20, 30]`, it should return `20` but instead returns `15`.

```
Problem Analysis Framework
==========================

Step 1: Problem Definition
┌─────────────────────────────────────────┐
│ Expected Behavior:                      │
│ calculateAverage([10, 20, 30]) → 20     │
│                                         │
│ Actual Behavior:                        │
│ calculateAverage([10, 20, 30]) → 15     │
│                                         │
│ Error Analysis:                         │
│ • Input seems correct                   │
│ • Output is 25% lower than expected     │
│ • Could be: sum error or division error │
│                                         │
│ Initial Hypotheses:                     │
│ 1. Sum calculation is wrong             │
│ 2. Division logic is incorrect          │
│ 3. Array length calculation is wrong    │
│ 4. Type conversion issue                │
└─────────────────────────────────────────┘

Step 2: Print Debugging Strategy
┌─────────────────────────────────────────┐
│ Strategic Print Placement:              │
│                                         │
│ function calculateAverage(numbers) {    │
│     console.log("1. Input:", numbers);  │
│     console.log("2. Array length:", numbers.length);
│                                         │
│     let sum = 0;                        │
│     console.log("3. Initial sum:", sum);│
│                                         │
│     for (let i = 0; i < numbers.length; i++) {
│         console.log(`4a. Adding numbers[${i}] = ${numbers[i]}`);
│         sum += numbers[i];              │
│         console.log(`4b. Sum after adding: ${sum}`);
│     }                                   │
│                                         │
│     console.log("5. Final sum:", sum);  │
│     console.log("6. Division:", `${sum} / ${numbers.length}`);
│     let result = sum / numbers.length;  │
│     console.log("7. Result:", result);  │
│     return result;                      │
│ }                                       │
│                                         │
│ What to look for in output:             │
│ • Are all array elements being added?   │
│ • Is the sum calculation correct?       │
│ • Is the division using right values?   │
│ • Are there any type conversion issues? │
└─────────────────────────────────────────┘

Step 3: Interactive Debugger Approach
┌─────────────────────────────────────────┐
│ Breakpoint Strategy:                    │
│                                         │
│ Breakpoint 1: Function entry            │
│ • Verify input parameter values         │
│ • Check array structure and contents    │
│                                         │
│ Breakpoint 2: Before loop               │
│ • Confirm initial sum value             │
│ • Verify array length                   │
│                                         │
│ Breakpoint 3: Inside loop               │
│ • Watch sum accumulation                │
│ • Check each array element value        │
│ • Monitor loop variable progression     │
│                                         │
│ Breakpoint 4: After loop                │
│ • Verify final sum value                │
│ • Check division calculation            │
│                                         │
│ Watch Expressions to Monitor:           │
│ • sum (throughout execution)            │
│ • numbers[i] (during loop)              │
│ • numbers.length                        │
│ • sum / numbers.length                  │
└─────────────────────────────────────────┘
```

#### Analysis Questions:

1. **Debugging Strategy Planning**:
   - How would you use print debugging to find the source of this problem?
   - What values would you print, and at which points in the function?
   - If using an interactive debugger, where would you set breakpoints to begin investigation?

2. **Root Cause Analysis**:
   - What are three possible causes for this type of error in an average calculation?
   - How would you determine whether the problem is in sum calculation or division?
   - What evidence would confirm each hypothesis?

3. **Systematic Investigation**:
   - How would you test your fix to ensure it works for other input cases?
   - What additional test cases would you create to prevent regression?
   - How would you verify the fix doesn't introduce new problems?

#### Implementation Challenge:

```
Complete Debugging Exercise
===========================

Step 1: Create the Buggy Function
┌─────────────────────────────────────────┐
│ Implement a calculateAverage function   │
│ that produces the wrong result (15      │
│ instead of 20 for [10, 20, 30])         │
│                                         │
│ Possible bugs to introduce:             │
│ • Wrong loop condition                  │
│ • Incorrect array access                │
│ • Division by wrong value               │
│ • Type conversion error                 │
│                                         │
│ Your buggy implementation:              │
│ _____________________________________   │
│ _____________________________________   │
│ _____________________________________   │
│ _____________________________________   │
└─────────────────────────────────────────┘

Step 2: Apply Debugging Techniques
┌─────────────────────────────────────────┐
│ Use both print debugging and (if        │
│ available) interactive debugger to      │
│ find the bug                            │
│                                         │
│ Document your debugging process:        │
│ • What did you observe?                 │
│ • What hypotheses did you form?         │
│ • What evidence supported/refuted them? │
│ • How did you isolate the root cause?   │
│                                         │
│ Debugging log:                          │
│ _____________________________________   │
│ _____________________________________   │
│ _____________________________________   │
│ _____________________________________   │
└─────────────────────────────────────────┘

Step 3: Write Comprehensive Tests
┌─────────────────────────────────────────┐
│ Create unit tests that would catch      │
│ this bug and prevent future regressions │
│                                         │
│ Test cases to include:                  │
│ • Normal cases: [1,2,3], [5,10,15]      │
│ • Edge cases: [0], [], [negative nums]  │
│ • Large datasets: 100+ numbers          │
│ • Boundary values: very large/small     │
│                                         │
│ Your test implementation:               │
│ _____________________________________   │
│ _____________________________________   │
│ _____________________________________   │
│ _____________________________________   │
└─────────────────────────────────────────┘
```

#### Extension Challenge:

**Advanced Testing and Debugging Scenarios**:

1. **Multi-Function Integration Bug**:
   - Create a system where `calculateAverage()` works with `filterValidNumbers()` and `formatResult()`
   - Introduce a subtle integration bug that only appears when functions work together
   - Use integration testing and debugging techniques to find and fix the issue

2. **Performance Debugging**:
   - Implement an average calculation that becomes slow with large datasets
   - Use profiling tools to identify performance bottlenecks
   - Apply optimization while maintaining correctness

3. **Concurrent Processing Bug**:
   - Design a scenario where multiple threads/processes calculate averages simultaneously
   - Introduce race conditions or shared state problems
   - Use advanced debugging techniques to identify and resolve concurrency issues

This exercise demonstrates how systematic testing and debugging transform error-prone code into reliable, well-tested software components that can be trusted in production environments.

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.