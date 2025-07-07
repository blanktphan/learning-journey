# 📖 Normalization: 1NF, 2NF, 3NF

## 🎯 Learning Objectives

Upon completion of this topic, you will be able to:

- Define and explain the goals of normalization (reduce redundancy, eliminate data anomalies)
- Identify and explain the three types of data anomalies
- Understand and apply the rules of the first three Normal Forms (1NF, 2NF, 3NF)
- Understand the concept of Functional Dependency as the foundation of normalization

---

## Introduction: The Problems of Poor Table Design

Database normalization is a systematic approach to organizing data to minimize redundancy and prevent data anomalies. Understanding why normalization matters requires seeing what happens when tables are poorly designed.

### Why Normalization Matters

Consider this common scenario in many organizations:
- Data Redundancy: Same information stored multiple times
- Storage Waste: Unnecessary disk space consumption
- Maintenance Nightmares: Updates required in multiple places
- Data Inconsistencies: Different versions of the "same" data

---

## 1. The Problems of Poorly Designed Tables

Let's examine a student course registration table that stores everything in one place:

```
REGISTRATIONS Table (Poorly Designed)
┌───────────┬─────────────┬──────────┬─────────────────┬───────┐
│ StudentID │ StudentName │ CourseID │   CourseName    │ Grade │
├───────────┼─────────────┼──────────┼─────────────────┼───────┤
│   S001    │   Alice     │  CS101   │  Programming    │   A   │
│   S001    │   Alice     │  MATH201 │   Calculus      │   B   │
│   S002    │    Bob      │  CS101   │  Programming    │   B   │
│   S002    │    Bob      │  PHYS301 │   Physics       │   A   │
│   S003    │   Carol     │  MATH201 │   Calculus      │   A   │
└───────────┴─────────────┴──────────┴─────────────────┴───────┘
```

Problems with this design:
- StudentName repeated for every course registration
- CourseName repeated for every student enrollment
- Massive data redundancy leading to serious anomalies

### 🚨 The Three Types of Data Anomalies

#### 1. Insertion Anomaly
Problem: Cannot add a new student to the system unless they register for at least one course.

Example: 
```sql
-- This fails because CourseID (part of primary key) would be NULL
INSERT INTO registrations (StudentID, StudentName, CourseID, CourseName, Grade)
VALUES ('S004', 'David', NULL, NULL, NULL);
```

Real-World Impact: New students must immediately register for courses, even if they're just exploring options.

#### 2. Deletion Anomaly
Problem: Deleting a student's last course registration removes all student information from the database.

Example:
```sql
-- If Bob only has one course and we delete it:
DELETE FROM registrations 
WHERE StudentID = 'S002' AND CourseID = 'CS101';
-- Bob's entire record disappears from the system!
```

Real-World Impact: Lose historical data about students who temporarily drop all courses.

#### 3. Update Anomaly
Problem: Changing course information requires updating multiple rows, risking inconsistency.

Example:
```sql
-- Course name change requires multiple updates
UPDATE registrations 
SET CourseName = 'Advanced Programming'
WHERE CourseID = 'CS101';
-- If we miss any rows, we get inconsistent data!
```

Real-World Impact: Database becomes unreliable with conflicting information.

Normalization is the systematic process of decomposing poorly designed tables into smaller, related tables to eliminate these problems.

---

## 2. Functional Dependency: The Theoretical Foundation

The heart of normalization lies in understanding Functional Dependency, represented as `X → Y`, meaning "the value of X uniquely determines the value of Y" or "Y depends on X."

### 🔍 Understanding Functional Dependencies

Definition: In a relation R, attribute Y is functionally dependent on attribute X if each value of X is associated with exactly one value of Y.

Examples from our REGISTRATIONS table:
```
StudentID → StudentName    (Student ID determines student name)
CourseID → CourseName      (Course ID determines course name)
{StudentID, CourseID} → Grade  (Both student and course determine the grade)
```

### 📊 Visual Representation of Dependencies
```
REGISTRATIONS Dependencies:
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│  StudentID  │───►│ StudentName │    │  CourseID   │───►│ CourseName  │
└─────────────┘    └─────────────┘    └─────────────┘    └─────────────┘
        │                                      │
        └──────────────┐      ┌────────────────┘
                       ▼      ▼
                   ┌─────────────┐
                   │    Grade    │
                   └─────────────┘
```

### 🎯 Types of Functional Dependencies

#### Full Functional Dependency
An attribute depends on the entire primary key, not just part of it.
```
{StudentID, CourseID} → Grade  ✅ (Full dependency)
```

#### Partial Functional Dependency
An attribute depends on only part of a composite primary key.
```
StudentID → StudentName  ❌ (Partial dependency - violates 2NF)
CourseID → CourseName    ❌ (Partial dependency - violates 2NF)
```

#### Transitive Functional Dependency
A non-key attribute depends on another non-key attribute.
```
EmployeeID → DepartmentID → DepartmentName  ❌ (Transitive - violates 3NF)
```

---

## 3. The Normal Forms

Normal Forms are a series of rules that measure the "quality" of table design. The first three forms are most important for practical database design.

### 🥇 First Normal Form (1NF)

Rule: Every column must contain atomic (indivisible) values, and each row must be unique.

Requirements:
1. Single values only - no lists, arrays, or multiple values in one cell
2. Unique rows - no duplicate records
3. Consistent data types - each column contains the same type of data

#### ❌ Violations of 1NF

Example 1: Multiple Values in Single Cell
```
STUDENTS (Violates 1NF)
┌───────────┬─────────────┬─────────────────────┐
│ StudentID │ StudentName │      Courses        │
├───────────┼─────────────┼─────────────────────┤
│   S001    │   Alice     │ CS101, MATH201      │  ❌ Multiple values
│   S002    │    Bob      │ CS101, PHYS301      │  ❌ Multiple values
└───────────┴─────────────┴─────────────────────┘
```

Example 2: Repeating Groups
```
ORDERS (Violates 1NF)
┌─────────┬─────────────┬──────────┬──────────┬──────────┐
│ OrderID │ CustomerName│ Product1 │ Product2 │ Product3 │
├─────────┼─────────────┼──────────┼──────────┼──────────┤
│  O001   │   John      │  Laptop  │  Mouse   │    -     │  ❌ Repeating columns
│  O002   │   Mary      │  Phone   │    -     │    -     │  ❌ Repeating columns
└─────────┴─────────────┴──────────┴──────────┴──────────┘
```

#### ✅ Converting to 1NF

Solution 1: Separate Rows
```
STUDENT_COURSES (1NF Compliant)
┌───────────┬─────────────┬──────────┐
│ StudentID │ StudentName │ CourseID │
├───────────┼─────────────┼──────────┤
│   S001    │   Alice     │  CS101   │  ✅ Atomic values
│   S001    │   Alice     │ MATH201  │  ✅ Atomic values
│   S002    │    Bob      │  CS101   │  ✅ Atomic values
│   S002    │    Bob      │ PHYS301  │  ✅ Atomic values
└───────────┴─────────────┴──────────┘
```

Solution 2: Separate Tables
```
ORDERS (1NF Compliant)
┌─────────┬─────────────┐     ORDER_ITEMS (1NF Compliant)
│ OrderID │ CustomerName│     ┌─────────┬─────────────┐
├─────────┼─────────────┤     │ OrderID │ ProductName │
│  O001   │   John      │     ├─────────┼─────────────┤
│  O002   │   Mary      │     │  O001   │   Laptop    │
└─────────┴─────────────┘     │  O001   │   Mouse     │
                               │  O002   │   Phone     │
                               └─────────┴─────────────┘
```

#### 🛠️ SQL Implementation for 1NF
```sql
-- Correct 1NF implementation
CREATE TABLE student_courses (
    student_id VARCHAR(10),
    student_name VARCHAR(100),
    course_id VARCHAR(10),
    
    PRIMARY KEY (student_id, course_id),  -- Composite key ensures uniqueness
    
    -- Each column contains atomic values only
    CHECK (student_id IS NOT NULL),
    CHECK (course_id IS NOT NULL)
);
```

### 🥈 Second Normal Form (2NF)

Prerequisites: Table must be in 1NF first.

Rule: Every non-key attribute must be fully functionally dependent on the entire primary key (no partial dependencies).

Note: This rule only applies to tables with composite primary keys.

#### 🔍 Identifying 2NF Violations

From our 1NF example:
```
STUDENT_COURSES (Violates 2NF)
Primary Key: {StudentID, CourseID}

Dependencies:
StudentID → StudentName        ❌ Partial dependency (violates 2NF)
CourseID → CourseName         ❌ Partial dependency (violates 2NF)  
{StudentID, CourseID} → Grade ✅ Full dependency (acceptable)
```

Problems with Partial Dependencies:
- Redundancy: StudentName repeated for every course
- Update Anomalies: Changing a student's name requires multiple updates
- Insertion Anomalies: Cannot add student without course enrollment

#### ✅ Converting to 2NF

Solution: Create separate tables for each entity:

```sql
-- Decompose into 2NF
CREATE TABLE students (
    student_id VARCHAR(10) PRIMARY KEY,
    student_name VARCHAR(100) NOT NULL
);

CREATE TABLE courses (
    course_id VARCHAR(10) PRIMARY KEY,
    course_name VARCHAR(100) NOT NULL,
    credits INTEGER,
    department VARCHAR(50)
);

CREATE TABLE enrollments (
    student_id VARCHAR(10),
    course_id VARCHAR(10),
    grade CHAR(2),
    enrollment_date DATE,
    
    PRIMARY KEY (student_id, course_id),
    
    FOREIGN KEY (student_id) REFERENCES students(student_id),
    FOREIGN KEY (course_id) REFERENCES courses(course_id)
);
```

#### 📊 Visual Representation of 2NF Decomposition
```
Before 2NF (Problems):
┌─────────────────────────────────────────────────────┐
│        STUDENT_COURSES (Violates 2NF)              │
│ StudentID | StudentName | CourseID | CourseName    │
│   (PK)    |   (Partial) |   (PK)   |   (Partial)   │
└─────────────────────────────────────────────────────┘

After 2NF (Solutions):
┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
│    STUDENTS     │  │     COURSES     │  │   ENROLLMENTS   │
│ StudentID (PK)  │  │ CourseID (PK)   │  │ StudentID (FK)  │
│ StudentName     │  │ CourseName      │  │ CourseID (FK)   │
└─────────────────┘  └─────────────────┘  │ Grade           │
                                          └─────────────────┘
```

### 🥉 Third Normal Form (3NF)

Prerequisites: Table must be in 2NF first.

Rule: There must be no transitive dependencies - non-key attributes cannot depend on other non-key attributes.

#### 🔍 Identifying 3NF Violations

Example: Employee table with department information
```
EMPLOYEES (Violates 3NF)
┌────────────┬──────────────┬──────────────┬─────────────────┐
│ EmployeeID │ EmployeeName │ DepartmentID │ DepartmentName  │
│    (PK)    │              │              │                 │
├────────────┼──────────────┼──────────────┼─────────────────┤
│    E001    │    Alice     │     D01      │   Engineering   │
│    E002    │     Bob      │     D01      │   Engineering   │
│    E003    │    Carol     │     D02      │      Sales      │
│    E004    │    David     │     D02      │      Sales      │
└────────────┴──────────────┴──────────────┴─────────────────┘

Dependencies:
EmployeeID → DepartmentID      ✅ Direct dependency
DepartmentID → DepartmentName  ❌ Transitive dependency
Therefore: EmployeeID → DepartmentID → DepartmentName ❌ Violates 3NF
```

Problems with Transitive Dependencies:
- Redundancy: Department names repeated for each employee
- Update Anomalies: Changing department name requires multiple updates
- Inconsistency: Risk of different department names for same ID

#### ✅ Converting to 3NF

Solution: Separate entities into their own tables:

```sql
-- 3NF Implementation
CREATE TABLE departments (
    department_id VARCHAR(10) PRIMARY KEY,
    department_name VARCHAR(100) NOT NULL UNIQUE,
    location VARCHAR(100),
    manager_id VARCHAR(10)
);

CREATE TABLE employees (
    employee_id VARCHAR(10) PRIMARY KEY,
    employee_name VARCHAR(100) NOT NULL,
    department_id VARCHAR(10),
    hire_date DATE,
    salary DECIMAL(10,2),
    
    FOREIGN KEY (department_id) 
        REFERENCES departments(department_id)
        ON UPDATE CASCADE
        ON DELETE SET NULL
);
```

#### 📊 Complete 3NF Example

Student Information System in 3NF:
```sql
-- Students table (entity: student)
CREATE TABLE students (
    student_id VARCHAR(10) PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE,
    phone VARCHAR(20),
    enrollment_date DATE DEFAULT CURRENT_DATE
);

-- Departments table (entity: department)  
CREATE TABLE departments (
    department_id VARCHAR(10) PRIMARY KEY,
    department_name VARCHAR(100) NOT NULL UNIQUE,
    building VARCHAR(50),
    phone VARCHAR(20)
);

-- Courses table (entity: course)
CREATE TABLE courses (
    course_id VARCHAR(10) PRIMARY KEY,
    course_name VARCHAR(100) NOT NULL,
    credits INTEGER CHECK (credits BETWEEN 1 AND 6),
    department_id VARCHAR(10),
    description TEXT,
    
    FOREIGN KEY (department_id) 
        REFERENCES departments(department_id)
);

-- Instructors table (entity: instructor)
CREATE TABLE instructors (
    instructor_id VARCHAR(10) PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    department_id VARCHAR(10),
    email VARCHAR(100) UNIQUE,
    
    FOREIGN KEY (department_id) 
        REFERENCES departments(department_id)
);

-- Course sections table (entity: course offering)
CREATE TABLE course_sections (
    section_id INTEGER PRIMARY KEY AUTO_INCREMENT,
    course_id VARCHAR(10),
    instructor_id VARCHAR(10),
    semester VARCHAR(20),
    year INTEGER,
    classroom VARCHAR(20),
    max_enrollment INTEGER,
    
    FOREIGN KEY (course_id) 
        REFERENCES courses(course_id),
    FOREIGN KEY (instructor_id) 
        REFERENCES instructors(instructor_id),
        
    UNIQUE (course_id, semester, year, classroom)
);

-- Enrollments table (relationship: student enrolls in section)
CREATE TABLE enrollments (
    enrollment_id INTEGER PRIMARY KEY AUTO_INCREMENT,
    student_id VARCHAR(10),
    section_id INTEGER,
    enrollment_date DATE DEFAULT CURRENT_DATE,
    grade CHAR(2),
    status ENUM('ENROLLED', 'COMPLETED', 'WITHDRAWN') DEFAULT 'ENROLLED',
    
    FOREIGN KEY (student_id) 
        REFERENCES students(student_id),
    FOREIGN KEY (section_id) 
        REFERENCES course_sections(section_id),
        
    UNIQUE (student_id, section_id)  -- Student can't enroll twice in same section
);
```

---

## 4. 🏗️ Real-World Normalization Example

Let's work through a complete normalization process using an e-commerce order system.

### 📋 Original Unnormalized Table

```
ORDERS (Unnormalized - 0NF)
┌─────────┬────────────┬────────────┬─────────────────┬─────────────────┬───────────┬─────────────┬──────────┬───────┐
│ OrderID │ OrderDate  │ CustomerID │  CustomerName   │ CustomerAddress │ ProductID │ ProductName │ Quantity │ Price │
├─────────┼────────────┼────────────┼─────────────────┼─────────────────┼───────────┼─────────────┼──────────┼───────┤
│  O001   │ 2024-01-15 │    C001    │     John Doe    │ 123 Main St     │   P001    │   Laptop    │    1     │  999  │
│  O001   │ 2024-01-15 │    C001    │     John Doe    │ 123 Main St     │   P002    │    Mouse    │    2     │   25  │
│  O002   │ 2024-01-16 │    C002    │    Jane Smith   │ 456 Oak Ave     │   P001    │   Laptop    │    1     │  999  │
│  O003   │ 2024-01-17 │    C001    │     John Doe    │ 123 Main St     │   P003    │  Keyboard   │    1     │   75  │
└─────────┴────────────┴────────────┴─────────────────┴─────────────────┴───────────┴─────────────┴──────────┴───────┘
```

### 🔄 Step-by-Step Normalization

#### Step 1: Convert to 1NF
Analysis: The table already has atomic values and unique rows.
Result: Already in 1NF.

#### Step 2: Convert to 2NF
Analysis: 
- Primary Key: `{OrderID, ProductID}`
- Dependencies:
  - `OrderID → {OrderDate, CustomerID, CustomerName, CustomerAddress}` ❌ Partial
  - `ProductID → {ProductName, Price}` ❌ Partial
  - `{OrderID, ProductID} → Quantity` ✅ Full

Solution:
```sql
-- Orders table (order information)
CREATE TABLE orders (
    order_id VARCHAR(10) PRIMARY KEY,
    order_date DATE NOT NULL,
    customer_id VARCHAR(10) NOT NULL,
    customer_name VARCHAR(100) NOT NULL,
    customer_address TEXT
);

-- Products table (product information)
CREATE TABLE products (
    product_id VARCHAR(10) PRIMARY KEY,
    product_name VARCHAR(100) NOT NULL,
    price DECIMAL(10,2) NOT NULL CHECK (price > 0),
    category VARCHAR(50),
    description TEXT
);

-- Order items table (relationship)
CREATE TABLE order_items (
    order_id VARCHAR(10),
    product_id VARCHAR(10),
    quantity INTEGER NOT NULL CHECK (quantity > 0),
    
    PRIMARY KEY (order_id, product_id),
    
    FOREIGN KEY (order_id) REFERENCES orders(order_id),
    FOREIGN KEY (product_id) REFERENCES products(product_id)
);
```

#### Step 3: Convert to 3NF
Analysis: 
- In `orders` table: `CustomerID → {CustomerName, CustomerAddress}` ❌ Transitive

Solution:
```sql
-- Customers table (separate customer entity)
CREATE TABLE customers (
    customer_id VARCHAR(10) PRIMARY KEY,
    customer_name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    phone VARCHAR(20),
    address TEXT,
    registration_date DATE DEFAULT CURRENT_DATE
);

-- Orders table (clean - only order-specific data)
CREATE TABLE orders (
    order_id VARCHAR(10) PRIMARY KEY,
    customer_id VARCHAR(10) NOT NULL,
    order_date DATE NOT NULL,
    status ENUM('PENDING', 'PROCESSING', 'SHIPPED', 'DELIVERED') DEFAULT 'PENDING',
    total_amount DECIMAL(10,2),
    
    FOREIGN KEY (customer_id) 
        REFERENCES customers(customer_id)
        ON UPDATE CASCADE
        ON DELETE RESTRICT  -- Can't delete customer with orders
);

-- Products table (unchanged - already normalized)
CREATE TABLE products (
    product_id VARCHAR(10) PRIMARY KEY,
    product_name VARCHAR(100) NOT NULL,
    price DECIMAL(10,2) NOT NULL CHECK (price > 0),
    category VARCHAR(50),
    stock_quantity INTEGER DEFAULT 0,
    description TEXT
);

-- Order items table (relationship with additional data)
CREATE TABLE order_items (
    order_item_id INTEGER PRIMARY KEY AUTO_INCREMENT,
    order_id VARCHAR(10),
    product_id VARCHAR(10),
    quantity INTEGER NOT NULL CHECK (quantity > 0),
    unit_price DECIMAL(10,2) NOT NULL,  -- Price at time of order
    line_total DECIMAL(10,2) GENERATED ALWAYS AS (quantity * unit_price),
    
    FOREIGN KEY (order_id) 
        REFERENCES orders(order_id) 
        ON DELETE CASCADE,
        
    FOREIGN KEY (product_id) 
        REFERENCES products(product_id) 
        ON DELETE RESTRICT,
        
    UNIQUE (order_id, product_id)  -- One product per order (or use surrogate key)
);
```

### 📊 Benefits of 3NF Design

Query Examples:
```sql
-- Get customer order history
SELECT c.customer_name, o.order_date, o.total_amount
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
WHERE c.customer_id = 'C001'
ORDER BY o.order_date DESC;

-- Get order details with products
SELECT o.order_id, c.customer_name, p.product_name, 
       oi.quantity, oi.unit_price, oi.line_total
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id
JOIN order_items oi ON o.order_id = oi.order_id
JOIN products p ON oi.product_id = p.product_id
WHERE o.order_id = 'O001';

-- Update product price (affects future orders only)
UPDATE products 
SET price = 1099.00 
WHERE product_id = 'P001';
-- Historical orders maintain original prices via unit_price
```

---

## Summary & Practical Exercise

### 📋 Summary

Normalization Goals:
1. Eliminate Redundancy: Store each fact only once
2. Prevent Anomalies: Avoid insertion, deletion, and update problems
3. Improve Integrity: Maintain consistent, accurate data
4. Optimize Storage: Reduce unnecessary data duplication

Normal Form Rules:
- 1NF: Atomic values, unique rows
- 2NF: No partial dependencies (eliminate redundancy from composite keys)
- 3NF: No transitive dependencies (separate entities completely)

Key Principle: Each table should describe exactly one entity and contain only attributes that directly describe that entity.

### 🧠 Practice Exercise: Order Management System

Scenario: You receive an Excel file with order data containing these columns:
`OrderID, OrderDate, CustomerID, CustomerName, CustomerAddress, ProductID, ProductName, Quantity, Price`

Questions:
1. What normal form is this data currently in?
2. What anomalies might occur with this design?
3. How would you decompose this table to achieve 3NF?

Your Task: Design a normalized database schema:

```sql
-- Complete this normalization exercise
CREATE TABLE customers (
    -- Design customer table
);

CREATE TABLE products (
    -- Design product table  
);

CREATE TABLE orders (
    -- Design order table
);

CREATE TABLE order_items (
    -- Design order items table
);
```

Guided Analysis:

Step 1: Identify Current Form
- Contains atomic values ✅ (1NF)
- Has composite dependencies ❌ (violates 2NF)
- Has transitive dependencies ❌ (violates 3NF)
- Current State: 1NF only

Step 2: Identify Dependencies
```
OrderID → {OrderDate, CustomerID}
CustomerID → {CustomerName, CustomerAddress}  
ProductID → {ProductName, Price}
{OrderID, ProductID} → Quantity
```

Step 3: Identify Anomalies
- Insertion: Can't add customer without order
- Deletion: Deleting last order loses customer data
- Update: Changing customer info requires multiple updates

Step 4: Solution Framework
```sql
-- 3NF Solution
CREATE TABLE customers (
    customer_id VARCHAR(10) PRIMARY KEY,
    customer_name VARCHAR(100) NOT NULL,
    customer_address TEXT,
    email VARCHAR(100) UNIQUE,
    phone VARCHAR(20)
);

CREATE TABLE products (
    product_id VARCHAR(10) PRIMARY KEY,
    product_name VARCHAR(100) NOT NULL,
    current_price DECIMAL(10,2) CHECK (current_price > 0),
    category VARCHAR(50),
    description TEXT
);

CREATE TABLE orders (
    order_id VARCHAR(10) PRIMARY KEY,
    customer_id VARCHAR(10) NOT NULL,
    order_date DATE NOT NULL,
    status VARCHAR(20) DEFAULT 'PENDING',
    
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);

CREATE TABLE order_items (
    order_id VARCHAR(10),
    product_id VARCHAR(10),
    quantity INTEGER CHECK (quantity > 0),
    unit_price DECIMAL(10,2),  -- Price at time of order
    
    PRIMARY KEY (order_id, product_id),
    
    FOREIGN KEY (order_id) REFERENCES orders(order_id) ON DELETE CASCADE,
    FOREIGN KEY (product_id) REFERENCES products(product_id)
);
```

Advanced Challenge: How would you handle:
- Products with time-varying prices?
- Orders with discounts or taxes?
- Customers with multiple addresses?
- Product variants (size, color)?

This exercise demonstrates how proper normalization creates flexible, maintainable database designs that grow with business requirements.

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.