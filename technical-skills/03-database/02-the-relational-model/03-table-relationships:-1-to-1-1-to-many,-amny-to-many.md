# 📖 Table Relationships: 1-to-1, 1-to-Many, Many-to-Many

## 🎯 Learning Objectives

Upon completion of this topic, you will be able to:

- Define "table relationships" in the context of relational databases
- Identify, explain, and model the three fundamental relationship types (One-to-One, One-to-Many, Many-to-Many)
- Understand how to implement each relationship type using Primary Keys and Foreign Keys
- Recognize and understand the purpose of "Junction Tables" for Many-to-Many relationships

---

## 1. Introduction: The Power of Connections

The true power of relational databases doesn't come from individual tables working in isolation, but from creating meaningful relationships between those tables. These relationships, enforced through Foreign Keys, enable us to model complex real-world scenarios, reduce data redundancy, and maintain data integrity across the entire system.

We define relationship types using Cardinality, which describes how many rows in one table can be related to how many rows in another table.

### Why Relationships Matter

Relationships solve fundamental data management challenges:
- Real-World Modeling: Accurately represent complex business scenarios
- Data Normalization: Eliminate redundant information storage
- Integrity Enforcement: Maintain consistency across related data
- Query Power: Enable sophisticated cross-table analysis

---

## 2. The Three Fundamental Relationship Types

### A. 🔗 One-to-One Relationship (1:1)

Definition: One row in Table A can relate to at most one row in Table B, and vice versa.

Characteristics:
- Least common relationship type in practice
- Often used for data separation rather than true business relationships
- Requires UNIQUE constraint on Foreign Key

#### 💡 Common Use Cases

1. Security Separation: Separate sensitive data from main table
```sql
-- Example: Separate employee salary information
EMPLOYEES(EmployeeID (PK), Name, Department, HireDate)
EMPLOYEE_SALARIES(SalaryID (PK), EmployeeID (FK, UNIQUE), BaseSalary, Bonus)
```

2. Performance Optimization: Separate large, infrequently accessed data
```sql
-- Example: Separate detailed profile information
USERS(UserID (PK), Username, Email, Status)
USER_PROFILES(ProfileID (PK), UserID (FK, UNIQUE), Bio, ProfilePicture, DetailedInfo)
```

#### 🌍 Real-World Example
Each country has exactly one capital city, and each capital city belongs to exactly one country.

#### 📊 Visual Representation
```
COUNTRIES                    CAPITALS
┌─────────────┬─────────────┐ ┌─────────────┬─────────────┬─────────────┐
│ CountryID   │CountryName  │ │ CapitalID   │ CapitalName │ CountryID   │
│    (PK)     │             │ │    (PK)     │             │(FK, UNIQUE) │
├─────────────┼─────────────┤ ├─────────────┼─────────────┼─────────────┤
│     1       │   Thailand  │◄┤     101     │   Bangkok   │      1      │
│     2       │    Japan    │◄┤     102     │    Tokyo    │      2      │
│     3       │   Germany   │◄┤     103     │   Berlin    │      3      │
└─────────────┴─────────────┘ └─────────────┴─────────────┴─────────────┘
```

#### 🛠️ SQL Implementation
```sql
-- Parent table
CREATE TABLE countries (
    country_id INTEGER PRIMARY KEY AUTO_INCREMENT,
    country_name VARCHAR(100) NOT NULL UNIQUE,
    continent VARCHAR(50),
    population BIGINT
);

-- Child table with 1:1 relationship
CREATE TABLE capitals (
    capital_id INTEGER PRIMARY KEY AUTO_INCREMENT,
    capital_name VARCHAR(100) NOT NULL,
    population INTEGER,
    country_id INTEGER UNIQUE,  -- UNIQUE enforces 1:1 relationship
    
    FOREIGN KEY (country_id) 
        REFERENCES countries(country_id) 
        ON DELETE CASCADE 
        ON UPDATE CASCADE
);
```

### B. 📈 One-to-Many Relationship (1:N)

Definition: One row in Table A ("one side") can relate to multiple rows in Table B ("many side"), but each row in Table B relates to exactly one row in Table A.

Characteristics:
- Most common relationship type in databases
- Foreign Key placed in the "many" side table
- No UNIQUE constraint on Foreign Key (allows duplicates)

#### 🌍 Real-World Example
One teacher can teach multiple courses, but each course has exactly one primary instructor.

#### 📊 Visual Representation
```
TEACHERS (One Side)              COURSES (Many Side)
┌─────────────┬─────────────┐    ┌─────────────┬─────────────┬─────────────┐
│ TeacherID   │ TeacherName │    │  CourseID   │ CourseName  │ TeacherID   │
│    (PK)     │             │    │    (PK)     │             │    (FK)     │
├─────────────┼─────────────┤    ├─────────────┼─────────────┼─────────────┤
│     T001    │ Dr. Smith   │◄───┤   CS101     │Programming  │    T001     │
│     T002    │ Dr. Johnson │◄┐  ├─────────────┼─────────────┼─────────────┤
│     T003    │ Dr. Brown   │ │  │   CS102     │Data Struct  │    T001     │
└─────────────┴─────────────┘ │  ├─────────────┼─────────────┼─────────────┤
                               └─┤  MATH201    │  Calculus   │    T002     │
                                  ├─────────────┼─────────────┼─────────────┤
                                  │  MATH301    │  Statistics │    T002     │
                                  └─────────────┴─────────────┴─────────────┘
```

#### 🛠️ SQL Implementation
```sql
-- Parent table (one side)
CREATE TABLE teachers (
    teacher_id VARCHAR(10) PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE,
    department VARCHAR(50),
    hire_date DATE
);

-- Child table (many side)
CREATE TABLE courses (
    course_id VARCHAR(10) PRIMARY KEY,
    course_name VARCHAR(100) NOT NULL,
    credits INTEGER CHECK (credits BETWEEN 1 AND 6),
    teacher_id VARCHAR(10),  -- Foreign Key (no UNIQUE constraint)
    
    FOREIGN KEY (teacher_id) 
        REFERENCES teachers(teacher_id) 
        ON DELETE SET NULL  -- Course remains if teacher leaves
        ON UPDATE CASCADE,
        
    INDEX idx_teacher (teacher_id)  -- Performance optimization
);
```

#### 🔄 Self-Referencing Example (Organizational Hierarchy)
```sql
-- Employees can have managers (who are also employees)
CREATE TABLE employees (
    employee_id INTEGER PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    position VARCHAR(100),
    manager_id INTEGER,  -- Self-referencing foreign key
    
    FOREIGN KEY (manager_id) 
        REFERENCES employees(employee_id) 
        ON DELETE SET NULL
);

-- Sample hierarchical data
INSERT INTO employees VALUES 
(1, 'John', 'CEO', 'Chief Executive', NULL),      -- Top level
(2, 'Alice', 'Smith', 'VP Engineering', 1),      -- Reports to CEO
(3, 'Bob', 'Johnson', 'Senior Developer', 2),    -- Reports to VP
(4, 'Carol', 'Brown', 'Junior Developer', 2);    -- Reports to VP
```

### C. 🔄 Many-to-Many Relationship (M:N)

Definition: Multiple rows in Table A can relate to multiple rows in Table B, and vice versa.

Characteristics:
- Cannot be implemented directly between two tables
- Requires a Junction Table (also called Linking Table or Bridge Table)
- Junction table contains Foreign Keys from both related tables
- Primary Key is usually a composite key

#### 🌍 Real-World Example
Students can enroll in multiple courses, and each course can have multiple students enrolled.

#### 📊 Visual Representation
```
STUDENTS                     ENROLLMENTS (Junction)               COURSES
┌─────────────┬─────────────┐ ┌─────────────┬─────────────┐ ┌─────────────┬─────────────┐
│ StudentID   │ StudentName │ │ StudentID   │  CourseID   │ │  CourseID   │ CourseName  │
│    (PK)     │             │ │   (FK,PK)   │   (FK,PK)   │ │    (PK)     │             │
├─────────────┼─────────────┤ ├─────────────┼─────────────┤ ├─────────────┼─────────────┤
│    S001     │   Alice     │◄┤    S001     │   CS101     │►│   CS101     │Programming  │
│    S002     │    Bob      │◄┤    S001     │   MATH201   │►│   CS102     │Data Struct  │
│    S003     │   Carol     │◄┤    S002     │   CS101     │►│   MATH201   │  Calculus   │
└─────────────┴─────────────┘ │    S002     │   CS102     │►│   MATH301   │ Statistics  │
                               │    S003     │   MATH201   │►└─────────────┴─────────────┘
                               │    S003     │   MATH301   │
                               └─────────────┴─────────────┘
```

#### 🛠️ SQL Implementation
```sql
-- First entity
CREATE TABLE students (
    student_id VARCHAR(10) PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE,
    major VARCHAR(50),
    enrollment_date DATE DEFAULT CURRENT_DATE
);

-- Second entity
CREATE TABLE courses (
    course_id VARCHAR(10) PRIMARY KEY,
    course_name VARCHAR(100) NOT NULL,
    credits INTEGER CHECK (credits BETWEEN 1 AND 6),
    department VARCHAR(50),
    description TEXT
);

-- Junction table for M:N relationship
CREATE TABLE enrollments (
    student_id VARCHAR(10),
    course_id VARCHAR(10),
    enrollment_date DATE DEFAULT CURRENT_DATE,
    grade CHAR(2),
    semester VARCHAR(20),
    year INTEGER,
    
    -- Composite primary key
    PRIMARY KEY (student_id, course_id, semester, year),
    
    -- Foreign key constraints
    FOREIGN KEY (student_id) 
        REFERENCES students(student_id) 
        ON DELETE CASCADE,
        
    FOREIGN KEY (course_id) 
        REFERENCES courses(course_id) 
        ON DELETE CASCADE,
        
    -- Additional constraints
    CHECK (grade IN ('A+', 'A', 'A-', 'B+', 'B', 'B-', 'C+', 'C', 'C-', 'D+', 'D', 'F'))
);
```

#### 💰 Rich Junction Table Example (Product-Supplier with Pricing)
```sql
-- Products can have multiple suppliers with different prices
CREATE TABLE products (
    product_id INTEGER PRIMARY KEY AUTO_INCREMENT,
    product_name VARCHAR(200) NOT NULL,
    description TEXT
);

CREATE TABLE suppliers (
    supplier_id INTEGER PRIMARY KEY AUTO_INCREMENT,
    supplier_name VARCHAR(100) NOT NULL,
    contact_email VARCHAR(100),
    phone VARCHAR(20)
);

-- Junction table with additional business data
CREATE TABLE product_suppliers (
    product_id INTEGER,
    supplier_id INTEGER,
    unit_price DECIMAL(10,2) NOT NULL,      -- Supplier-specific pricing
    minimum_order_quantity INTEGER,
    lead_time_days INTEGER,
    last_updated DATE DEFAULT CURRENT_DATE,
    
    PRIMARY KEY (product_id, supplier_id),
    
    FOREIGN KEY (product_id) 
        REFERENCES products(product_id) 
        ON DELETE CASCADE,
        
    FOREIGN KEY (supplier_id) 
        REFERENCES suppliers(supplier_id) 
        ON DELETE CASCADE,
        
    CHECK (unit_price > 0),
    CHECK (minimum_order_quantity > 0)
);
```

---

## 3. 🏗️ Real-World Application: E-Commerce System

Let's apply all three relationship types in a comprehensive e-commerce example:

```sql
-- Users table
CREATE TABLE users (
    user_id INTEGER PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    registration_date DATETIME DEFAULT CURRENT_TIMESTAMP
);

-- User profiles (1:1 relationship)
CREATE TABLE user_profiles (
    profile_id INTEGER PRIMARY KEY AUTO_INCREMENT,
    user_id INTEGER UNIQUE NOT NULL,  -- 1:1 relationship
    bio TEXT,
    profile_picture_url VARCHAR(500),
    phone VARCHAR(20),
    address TEXT,
    
    FOREIGN KEY (user_id) 
        REFERENCES users(user_id) 
        ON DELETE CASCADE
);

-- Categories table
CREATE TABLE categories (
    category_id INTEGER PRIMARY KEY AUTO_INCREMENT,
    category_name VARCHAR(100) UNIQUE NOT NULL,
    description TEXT,
    parent_category_id INTEGER,  -- Self-referencing for hierarchy
    
    FOREIGN KEY (parent_category_id) 
        REFERENCES categories(category_id)
);

-- Products table
CREATE TABLE products (
    product_id INTEGER PRIMARY KEY AUTO_INCREMENT,
    product_name VARCHAR(200) NOT NULL,
    description TEXT,
    price DECIMAL(10,2) CHECK (price > 0),
    stock_quantity INTEGER DEFAULT 0,
    category_id INTEGER,  -- 1:N relationship with categories
    
    FOREIGN KEY (category_id) 
        REFERENCES categories(category_id) 
        ON DELETE SET NULL
);

-- Orders (1:N relationship with users)
CREATE TABLE orders (
    order_id INTEGER PRIMARY KEY AUTO_INCREMENT,
    user_id INTEGER NOT NULL,  -- 1:N: One user, many orders
    order_date DATETIME DEFAULT CURRENT_TIMESTAMP,
    status ENUM('PENDING', 'PROCESSING', 'SHIPPED', 'DELIVERED') DEFAULT 'PENDING',
    total_amount DECIMAL(10,2),
    
    FOREIGN KEY (user_id) 
        REFERENCES users(user_id) 
        ON DELETE RESTRICT  -- Cannot delete user with orders
);

-- Order items (M:N between orders and products)
CREATE TABLE order_items (
    order_id INTEGER,
    product_id INTEGER,
    quantity INTEGER NOT NULL CHECK (quantity > 0),
    unit_price DECIMAL(10,2) NOT NULL,
    line_total DECIMAL(10,2) GENERATED ALWAYS AS (quantity * unit_price),
    
    PRIMARY KEY (order_id, product_id),
    
    FOREIGN KEY (order_id) 
        REFERENCES orders(order_id) 
        ON DELETE CASCADE,
        
    FOREIGN KEY (product_id) 
        REFERENCES products(product_id) 
        ON DELETE RESTRICT
);

-- Product reviews (M:N between users and products)
CREATE TABLE product_reviews (
    user_id INTEGER,
    product_id INTEGER,
    rating INTEGER CHECK (rating BETWEEN 1 AND 5),
    review_text TEXT,
    review_date DATETIME DEFAULT CURRENT_TIMESTAMP,
    
    PRIMARY KEY (user_id, product_id),
    
    FOREIGN KEY (user_id) 
        REFERENCES users(user_id) 
        ON DELETE CASCADE,
        
    FOREIGN KEY (product_id) 
        REFERENCES products(product_id) 
        ON DELETE CASCADE
);
```

### 📊 Query Examples for Different Relationships

1:1 Queries (User Profiles):
```sql
-- Get user with profile information
SELECT u.username, u.email, p.bio, p.phone
FROM users u
LEFT JOIN user_profiles p ON u.user_id = p.user_id
WHERE u.user_id = 123;
```

1:N Queries (User Orders):
```sql
-- Get all orders for a specific user
SELECT o.order_id, o.order_date, o.status, o.total_amount
FROM orders o
WHERE o.user_id = 123
ORDER BY o.order_date DESC;

-- Count orders per user
SELECT u.username, COUNT(o.order_id) as order_count
FROM users u
LEFT JOIN orders o ON u.user_id = o.user_id
GROUP BY u.user_id, u.username
ORDER BY order_count DESC;
```

M:N Queries (Product Reviews):
```sql
-- Get all reviews for a specific product
SELECT u.username, r.rating, r.review_text, r.review_date
FROM product_reviews r
JOIN users u ON r.user_id = u.user_id
WHERE r.product_id = 456
ORDER BY r.review_date DESC;

-- Get average rating per product
SELECT p.product_name, 
       AVG(r.rating) as avg_rating,
       COUNT(r.rating) as review_count
FROM products p
LEFT JOIN product_reviews r ON p.product_id = r.product_id
GROUP BY p.product_id, p.product_name
ORDER BY avg_rating DESC;
```

---

## Summary & Practical Exercise

### 📋 Summary

Relationship Types:
1. One-to-One (1:1): Use UNIQUE Foreign Key - for data separation
2. One-to-Many (1:N): Foreign Key in "many" side - most common type
3. Many-to-Many (M:N): Junction Table with composite keys - for complex relationships

Implementation Rules:
- 1:1: `FK + UNIQUE` constraint
- 1:N: `FK` in child table (many side)
- M:N: Junction table with `FK` from both entities

### 🧠 Practice Exercise: E-Commerce Product-Supplier Analysis

Question: Consider the relationship between Products and Suppliers in an e-commerce system:

1. What type of relationship should exist between Products and Suppliers (1:1, 1:N, or M:N)? Why?

Analysis:
- One product can be supplied by multiple suppliers (for better pricing/availability)
- One supplier can supply multiple products (typical business model)
- Answer: Many-to-Many (M:N) relationship

2. How would you design the schema to support this relationship?

Your Task: Complete this schema design:
```sql
CREATE TABLE products (
    product_id INTEGER PRIMARY KEY AUTO_INCREMENT,
    product_name VARCHAR(200) NOT NULL,
    description TEXT,
    category VARCHAR(100)
);

CREATE TABLE suppliers (
    supplier_id INTEGER PRIMARY KEY AUTO_INCREMENT,
    supplier_name VARCHAR(100) NOT NULL,
    contact_email VARCHAR(100),
    phone VARCHAR(20),
    address TEXT
);

-- Design the junction table
CREATE TABLE product_suppliers (
    -- Add appropriate columns and constraints
    -- Consider: pricing, minimum order quantity, lead time
);
```

Advanced Challenge: 
- How would you find the cheapest supplier for each product?
- How would you handle supplier discontinuing a product?
- What additional attributes might be useful in the junction table?

Solution Framework:
```sql
-- Junction table with business data
CREATE TABLE product_suppliers (
    product_id INTEGER,
    supplier_id INTEGER,
    unit_price DECIMAL(10,2) NOT NULL,
    minimum_order_quantity INTEGER DEFAULT 1,
    lead_time_days INTEGER,
    is_preferred_supplier BOOLEAN DEFAULT FALSE,
    last_updated DATE DEFAULT CURRENT_DATE,
    
    PRIMARY KEY (product_id, supplier_id),
    
    FOREIGN KEY (product_id) 
        REFERENCES products(product_id) 
        ON DELETE CASCADE,
        
    FOREIGN KEY (supplier_id) 
        REFERENCES suppliers(supplier_id) 
        ON DELETE CASCADE,
        
    CHECK (unit_price > 0),
    CHECK (minimum_order_quantity > 0)
);

-- Query: Find cheapest supplier per product
SELECT p.product_name, s.supplier_name, ps.unit_price
FROM products p
JOIN product_suppliers ps ON p.product_id = ps.product_id
JOIN suppliers s ON ps.supplier_id = s.supplier_id
WHERE ps.unit_price = (
    SELECT MIN(ps2.unit_price)
    FROM product_suppliers ps2
    WHERE ps2.product_id = p.product_id
)
ORDER BY p.product_name;
```

This exercise demonstrates how relationship analysis leads to proper database design decisions and supports complex business requirements.

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.