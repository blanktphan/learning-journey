# 📖 Keys and Constraints: Primary, Foreign, Unique

## 🎯 Learning Objectives

Upon completion of this topic, you will be able to:

- Define and distinguish between Superkey, Candidate Key, Primary Key, and Foreign Key
- Explain the role of keys in guaranteeing data uniqueness and establishing relationships
- Understand the concepts of "Entity Integrity" and "Referential Integrity" as fundamental rules enforced by keys
- Identify and explain other types of constraints used to maintain data correctness

---

## Introduction: The Foundation of Data Integrity

In relational databases, keys are the fundamental mechanisms that ensure data integrity, uniqueness, and proper relationships between tables. They serve as the backbone of database design, preventing data corruption and maintaining logical consistency across the entire system.

### Why Keys Matter

Keys solve critical data management challenges:
- Unique Identification: Guarantee every row can be uniquely identified
- Relationship Establishment: Create logical connections between tables
- Data Integrity: Prevent invalid or inconsistent data entry
- Performance Optimization: Enable efficient indexing and searching

---

## 1. 🔑 Keys: The Identity Tools

In the relational model, we need a 100% guaranteed method to uniquely identify any specific tuple (row) in a table without confusion with other rows. A key is a set of one or more attributes (columns) that serves this purpose.

### 🌟 Superkey

Definition: A superkey is any set of attributes that, when combined, can uniquely identify a tuple in a relation.

Key Characteristics:
- May contain more attributes than necessary
- If K is a superkey, then any superset of K is also a superkey
- Multiple superkeys can exist for a single relation

Example: Consider table STUDENTS(StudentID, CitizenID, FirstName, LastName)

```
STUDENTS Table:
┌─────────────┬─────────────┬─────────────┬─────────────┐
│  StudentID  │  CitizenID  │  FirstName  │  LastName   │
├─────────────┼─────────────┼─────────────┼─────────────┤
│    1001     │ 1234567890  │   Somchai   │   Jaidee    │
│    1002     │ 9876543210  │    Maria    │   Garcia    │
│    1003     │ 5555555555  │   Ahmed     │   Hassan    │
└─────────────┴─────────────┴─────────────┴─────────────┘
```

Superkey Examples:
- `{StudentID}` ✅ (Student ID is unique)
- `{CitizenID}` ✅ (Citizen ID is unique)
- `{StudentID, FirstName}` ✅ (Still unique, even though FirstName alone might not be)
- `{CitizenID, LastName}` ✅ (Still unique, contains the unique CitizenID)
- `{StudentID, CitizenID, FirstName, LastName}` ✅ (All attributes together)

SQL Implementation:
```sql
-- These constraints ensure superkey properties
CREATE TABLE students (
    student_id INTEGER UNIQUE,        -- This alone forms a superkey
    citizen_id VARCHAR(10) UNIQUE,    -- This alone forms a superkey
    first_name VARCHAR(50),
    last_name VARCHAR(50)
);
```

### 🎯 Candidate Key

Definition: A candidate key is a minimal superkey - meaning if you remove any attribute from it, it would no longer be a superkey.

Key Characteristics:
- Smallest possible set of attributes that maintains uniqueness
- No redundant attributes
- Multiple candidate keys can exist in a single relation
- Foundation for choosing the primary key

Example: From the STUDENTS table above:

Candidate Keys:
- `{StudentID}` ✅ (Minimal - cannot remove anything)
- `{CitizenID}` ✅ (Minimal - cannot remove anything)

NOT Candidate Keys:
- `{StudentID, FirstName}` ❌ (Not minimal - can remove FirstName)
- `{CitizenID, LastName}` ❌ (Not minimal - can remove LastName)

Advanced Example with Composite Candidate Key:
```sql
CREATE TABLE course_sections (
    course_code VARCHAR(10),     -- e.g., "CS101"
    semester VARCHAR(10),        -- e.g., "Fall"
    year INTEGER,                -- e.g., 2024
    section_number INTEGER,      -- e.g., 1, 2, 3
    instructor_id INTEGER,
    room VARCHAR(20)
);

-- Composite candidate key: no two sections can have the same course, semester, year, and section number
-- {course_code, semester, year, section_number} is a candidate key
```

### 👑 Primary Key (PK)

Definition: A primary key is the chosen candidate key that serves as the main identifier for tuples in a relation.

Selection Criteria:
1. Stability: Values rarely change over time
2. Simplicity: Shorter and easier to understand
3. Meaningfulness: Clear business significance
4. Performance: Efficient for indexing and joining

Primary Key Rules:
- UNIQUE: No duplicate values allowed
- NOT NULL: No null values permitted
- IMMUTABLE: Values should not change frequently
- SINGLE PER TABLE: Only one primary key per table

Implementation Examples:

Simple Primary Key:
```sql
CREATE TABLE students (
    student_id INTEGER PRIMARY KEY,  -- Single-column primary key
    citizen_id VARCHAR(10) UNIQUE,   -- Candidate key not chosen as primary
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE
);
```

Composite Primary Key:
```sql
CREATE TABLE enrollments (
    student_id INTEGER,
    course_id VARCHAR(10),
    semester VARCHAR(10),
    year INTEGER,
    grade CHAR(2),
    enrollment_date DATE,
    
    -- Composite primary key
    PRIMARY KEY (student_id, course_id, semester, year),
    
    -- Foreign key constraints (explained later)
    FOREIGN KEY (student_id) REFERENCES students(student_id),
    FOREIGN KEY (course_id) REFERENCES courses(course_id)
);
```

Auto-Generated Primary Keys:
```sql
-- Using auto-increment for surrogate keys
CREATE TABLE books (
    book_id INTEGER PRIMARY KEY AUTO_INCREMENT,  -- Surrogate key
    isbn VARCHAR(13) UNIQUE,                     -- Natural candidate key
    title VARCHAR(200) NOT NULL,
    author VARCHAR(100) NOT NULL,
    publication_year INTEGER
);
```

### 🔗 Foreign Key (FK): The Relationship Builder

Definition: A foreign key is a set of attributes in one table (referencing table) whose values must match the values of a candidate key (usually primary key) in another table (referenced table).

Purpose:
- Create and enforce logical relationships between tables
- Maintain referential integrity
- Prevent orphaned records
- Enable complex queries across multiple tables

Visual Representation:
```
STUDENTS Table (Referenced)           ENROLLMENTS Table (Referencing)
┌─────────────┬─────────────┐        ┌─────────────┬─────────────┬─────────────┐
│ StudentID   │    Name     │        │EnrollmentID │ StudentID   │  CourseID   │
│    (PK)     │             │        │    (PK)     │    (FK)     │    (FK)     │
├─────────────┼─────────────┤        ├─────────────┼─────────────┼─────────────┤
│    1001     │  Somchai    │◄───────┤     E001    │    1001     │   CS101     │
│    1002     │   Maria     │◄───────┤     E002    │    1002     │   MATH201   │
│    1003     │   Ahmed     │◄───────┤     E003    │    1001     │   MATH201   │
└─────────────┴─────────────┘        └─────────────┴─────────────┴─────────────┘
                                                           │
                ┌─────────────┬─────────────┐             │
                │  CourseID   │ CourseName  │◄────────────┘
                │    (PK)     │             │
                ├─────────────┼─────────────┤
                │   CS101     │Programming  │
                │  MATH201    │ Calculus    │
                └─────────────┴─────────────┘
                     COURSES Table
```

SQL Implementation:
```sql
-- Parent tables (referenced tables)
CREATE TABLE students (
    student_id INTEGER PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE
);

CREATE TABLE courses (
    course_id VARCHAR(10) PRIMARY KEY,
    course_name VARCHAR(100) NOT NULL,
    credits INTEGER CHECK (credits > 0)
);

-- Child table (referencing table) with foreign keys
CREATE TABLE enrollments (
    enrollment_id INTEGER PRIMARY KEY AUTO_INCREMENT,
    student_id INTEGER,
    course_id VARCHAR(10),
    enrollment_date DATE DEFAULT CURRENT_DATE,
    grade CHAR(2),
    
    -- Foreign key constraints
    FOREIGN KEY (student_id) 
        REFERENCES students(student_id) 
        ON DELETE CASCADE 
        ON UPDATE CASCADE,
        
    FOREIGN KEY (course_id) 
        REFERENCES courses(course_id) 
        ON DELETE RESTRICT 
        ON UPDATE CASCADE
);
```

Foreign Key Actions:

| Action | Description | Example |
|--------|-------------|---------|
| `CASCADE` | Propagate changes to child records | Delete student → Delete their enrollments |
| `RESTRICT` | Prevent parent changes if children exist | Cannot delete course with active enrollments |
| `SET NULL` | Set foreign key to NULL | Delete instructor → Set course instructor to NULL |
| `SET DEFAULT` | Set foreign key to default value | Delete department → Set employee dept to default |

---

## 2. 🛡️ Integrity Rules

Keys enforce two fundamental integrity rules that are essential for database correctness:

### 🎯 Entity Integrity

Rule: The primary key value must never be NULL.

Rationale: 
- Primary key represents the identity of an entity
- If NULL, the entity cannot be uniquely identified
- Prevents "anonymous" records that cannot be referenced

Implementation:
```sql
CREATE TABLE students (
    student_id INTEGER PRIMARY KEY,    -- Automatically NOT NULL
    name VARCHAR(100) NOT NULL
);

-- This insertion will fail
INSERT INTO students (student_id, name) 
VALUES (NULL, 'John Doe');  -- Error: Primary key cannot be NULL
```

Entity Integrity Violations:
```sql
-- ❌ These operations violate entity integrity
INSERT INTO students VALUES (NULL, 'Alice');        -- NULL primary key
UPDATE students SET student_id = NULL WHERE name = 'Bob';  -- Setting PK to NULL
```

### 🔗 Referential Integrity

Rule: A foreign key value must either:
1. Match an existing primary key in the referenced table, OR
2. Be NULL (if the relationship is optional)

Rationale:
- Prevents "orphaned" records that reference non-existent entities
- Maintains logical consistency across related tables
- Ensures all relationships are valid

Valid Foreign Key States:
```sql
-- Valid insertions (referential integrity maintained)
INSERT INTO enrollments (student_id, course_id) 
VALUES (1001, 'CS101');     -- Both 1001 and CS101 exist

INSERT INTO enrollments (student_id, course_id) 
VALUES (1002, NULL);        -- NULL is allowed if relationship is optional
```

Referential Integrity Violations:
```sql
-- ❌ These operations violate referential integrity
INSERT INTO enrollments (student_id, course_id) 
VALUES (9999, 'CS101');     -- Student 9999 doesn't exist

INSERT INTO enrollments (student_id, course_id) 
VALUES (1001, 'XYZ999');    -- Course XYZ999 doesn't exist

DELETE FROM students WHERE student_id = 1001;  -- Fails if enrollments exist
```

Maintaining Referential Integrity:
```sql
-- Safe deletion with cascade
CREATE TABLE enrollments (
    -- ... other columns ...
    FOREIGN KEY (student_id) 
        REFERENCES students(student_id) 
        ON DELETE CASCADE    -- Delete enrollments when student is deleted
);

-- Safe deletion with restriction
CREATE TABLE course_offerings (
    -- ... other columns ...
    FOREIGN KEY (course_id) 
        REFERENCES courses(course_id) 
        ON DELETE RESTRICT   -- Prevent course deletion if offerings exist
);
```

---

## 3. 🔒 Other Database Constraints

Beyond keys, DBMS provide additional constraints to maintain data quality and business rules:

### 📝 NOT NULL Constraint

Purpose: Ensures that a column always contains a value.

Usage: For mandatory fields that are essential for business logic.

```sql
CREATE TABLE employees (
    employee_id INTEGER PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,      -- Mandatory
    last_name VARCHAR(50) NOT NULL,       -- Mandatory
    email VARCHAR(100) NOT NULL UNIQUE,   -- Mandatory and unique
    phone VARCHAR(20),                    -- Optional
    hire_date DATE NOT NULL DEFAULT CURRENT_DATE
);

-- ❌ This insertion will fail
INSERT INTO employees (employee_id, last_name, email) 
VALUES (1, 'Smith', 'john@company.com');  -- Missing required first_name
```

### ✨ UNIQUE Constraint

Purpose: Ensures all values in a column (or combination of columns) are distinct.

Key Differences from Primary Key:
- Allows one NULL value (NULL ≠ NULL in uniqueness comparison)
- Multiple UNIQUE constraints allowed per table
- Can be modified after table creation

```sql
CREATE TABLE users (
    user_id INTEGER PRIMARY KEY,
    username VARCHAR(50) UNIQUE,          -- Unique username
    email VARCHAR(100) UNIQUE,            -- Unique email
    phone VARCHAR(20) UNIQUE,             -- Unique phone
    social_security VARCHAR(11) UNIQUE    -- Unique SSN
);

-- Composite unique constraint
CREATE TABLE course_schedules (
    schedule_id INTEGER PRIMARY KEY,
    course_id VARCHAR(10),
    classroom VARCHAR(20),
    time_slot VARCHAR(20),
    day_of_week VARCHAR(10),
    
    -- No two courses can use the same classroom at the same time
    UNIQUE (classroom, time_slot, day_of_week)
);
```

### ✅ CHECK Constraint

Purpose: Enforces domain constraints and business rules at the database level.

Benefits:
- Automatic validation of data values
- Consistent rule enforcement across all applications
- Performance optimization through early validation

```sql
CREATE TABLE products (
    product_id INTEGER PRIMARY KEY,
    product_name VARCHAR(100) NOT NULL,
    price DECIMAL(10,2) CHECK (price > 0),                    -- Positive prices
    discount_rate DECIMAL(3,2) CHECK (discount_rate BETWEEN 0 AND 1), -- 0-100%
    category VARCHAR(50) CHECK (category IN ('Electronics', 'Books', 'Clothing')),
    stock_quantity INTEGER CHECK (stock_quantity >= 0),       -- Non-negative stock
    
    -- Complex check constraint
    CONSTRAINT check_price_discount 
        CHECK (price * (1 - discount_rate) > 0)               -- Final price > 0
);

-- Academic constraints
CREATE TABLE grades (
    grade_id INTEGER PRIMARY KEY,
    student_id INTEGER,
    course_id VARCHAR(10),
    letter_grade CHAR(2) CHECK (letter_grade IN ('A+', 'A', 'A-', 'B+', 'B', 'B-', 'C+', 'C', 'C-', 'D+', 'D', 'F')),
    numeric_grade DECIMAL(4,2) CHECK (numeric_grade BETWEEN 0.00 AND 4.00),
    credit_hours INTEGER CHECK (credit_hours BETWEEN 1 AND 6),
    
    -- Ensure grade consistency
    CONSTRAINT check_grade_consistency CHECK (
        (letter_grade = 'A+' AND numeric_grade >= 3.85) OR
        (letter_grade = 'A' AND numeric_grade BETWEEN 3.70 AND 3.84) OR
        (letter_grade = 'F' AND numeric_grade < 1.00)
        -- ... more grade mappings
    )
);
```

### 🕒 DEFAULT Constraint

Purpose: Provides automatic values for columns when no value is specified.

```sql
CREATE TABLE orders (
    order_id INTEGER PRIMARY KEY AUTO_INCREMENT,
    customer_id INTEGER NOT NULL,
    order_date DATE DEFAULT CURRENT_DATE,
    status VARCHAR(20) DEFAULT 'PENDING',
    priority VARCHAR(10) DEFAULT 'NORMAL',
    total_amount DECIMAL(10,2) DEFAULT 0.00,
    
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);

-- Using defaults
INSERT INTO orders (customer_id, total_amount) 
VALUES (1001, 299.99);
-- Automatically sets: order_date = today, status = 'PENDING', priority = 'NORMAL'
```

---

## 4. 🏗️ Real-World Application: E-Commerce Database Design

Let's apply these concepts to design a comprehensive e-commerce system:

### 📊 Complete Schema with All Constraint Types

```sql
-- Customers table with various constraints
CREATE TABLE customers (
    customer_id INTEGER PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE,
    phone VARCHAR(20) UNIQUE,
    birth_date DATE CHECK (birth_date < CURRENT_DATE),
    registration_date DATE DEFAULT CURRENT_DATE,
    status ENUM('ACTIVE', 'INACTIVE', 'SUSPENDED') DEFAULT 'ACTIVE',
    credit_limit DECIMAL(10,2) DEFAULT 1000.00 CHECK (credit_limit >= 0)
);

-- Categories with hierarchical structure
CREATE TABLE categories (
    category_id INTEGER PRIMARY KEY AUTO_INCREMENT,
    category_name VARCHAR(100) NOT NULL UNIQUE,
    parent_category_id INTEGER,
    description TEXT,
    
    -- Self-referencing foreign key for hierarchy
    FOREIGN KEY (parent_category_id) 
        REFERENCES categories(category_id) 
        ON DELETE SET NULL
);

-- Products with comprehensive constraints
CREATE TABLE products (
    product_id INTEGER PRIMARY KEY AUTO_INCREMENT,
    sku VARCHAR(50) NOT NULL UNIQUE,                    -- Stock Keeping Unit
    product_name VARCHAR(200) NOT NULL,
    category_id INTEGER,
    price DECIMAL(10,2) NOT NULL CHECK (price > 0),
    cost DECIMAL(10,2) CHECK (cost >= 0),
    stock_quantity INTEGER DEFAULT 0 CHECK (stock_quantity >= 0),
    reorder_level INTEGER DEFAULT 10 CHECK (reorder_level >= 0),
    weight_kg DECIMAL(6,2) CHECK (weight_kg > 0),
    status ENUM('ACTIVE', 'DISCONTINUED', 'OUT_OF_STOCK') DEFAULT 'ACTIVE',
    created_date DATE DEFAULT CURRENT_DATE,
    
    -- Business rule: cost should be less than price
    CONSTRAINT check_profit_margin CHECK (cost < price),
    
    FOREIGN KEY (category_id) 
        REFERENCES categories(category_id) 
        ON DELETE SET NULL
);

-- Orders with comprehensive tracking
CREATE TABLE orders (
    order_id INTEGER PRIMARY KEY AUTO_INCREMENT,
    customer_id INTEGER NOT NULL,
    order_number VARCHAR(20) NOT NULL UNIQUE,
    order_date DATETIME DEFAULT CURRENT_TIMESTAMP,
    status ENUM('PENDING', 'PROCESSING', 'SHIPPED', 'DELIVERED', 'CANCELLED') DEFAULT 'PENDING',
    subtotal DECIMAL(10,2) DEFAULT 0.00 CHECK (subtotal >= 0),
    tax_amount DECIMAL(10,2) DEFAULT 0.00 CHECK (tax_amount >= 0),
    shipping_cost DECIMAL(10,2) DEFAULT 0.00 CHECK (shipping_cost >= 0),
    total_amount DECIMAL(10,2) GENERATED ALWAYS AS (subtotal + tax_amount + shipping_cost),
    
    -- Payment tracking
    payment_method ENUM('CREDIT_CARD', 'DEBIT_CARD', 'PAYPAL', 'BANK_TRANSFER'),
    payment_status ENUM('PENDING', 'COMPLETED', 'FAILED', 'REFUNDED') DEFAULT 'PENDING',
    
    FOREIGN KEY (customer_id) 
        REFERENCES customers(customer_id) 
        ON DELETE RESTRICT  -- Cannot delete customer with orders
);

-- Order items with quantity and pricing constraints
CREATE TABLE order_items (
    order_item_id INTEGER PRIMARY KEY AUTO_INCREMENT,
    order_id INTEGER NOT NULL,
    product_id INTEGER NOT NULL,
    quantity INTEGER NOT NULL CHECK (quantity > 0),
    unit_price DECIMAL(10,2) NOT NULL CHECK (unit_price > 0),
    line_total DECIMAL(10,2) GENERATED ALWAYS AS (quantity * unit_price),
    
    -- Composite unique constraint: one product per order
    UNIQUE (order_id, product_id),
    
    FOREIGN KEY (order_id) 
        REFERENCES orders(order_id) 
        ON DELETE CASCADE,
        
    FOREIGN KEY (product_id) 
        REFERENCES products(product_id) 
        ON DELETE RESTRICT
);

-- Inventory tracking with audit trail
CREATE TABLE inventory_transactions (
    transaction_id INTEGER PRIMARY KEY AUTO_INCREMENT,
    product_id INTEGER NOT NULL,
    transaction_type ENUM('PURCHASE', 'SALE', 'ADJUSTMENT', 'RETURN') NOT NULL,
    quantity_change INTEGER NOT NULL,  -- Can be negative for sales
    transaction_date DATETIME DEFAULT CURRENT_TIMESTAMP,
    reference_order_id INTEGER,        -- Optional reference to order
    notes TEXT,
    
    FOREIGN KEY (product_id) 
        REFERENCES products(product_id) 
        ON DELETE RESTRICT,
        
    FOREIGN KEY (reference_order_id) 
        REFERENCES orders(order_id) 
        ON DELETE SET NULL
);
```

### 🔍 Advanced Constraint Examples

Complex Business Rules with Triggers:
```sql
-- Trigger to automatically update product stock
DELIMITER $$
CREATE TRIGGER update_stock_after_order 
    AFTER INSERT ON order_items
    FOR EACH ROW
BEGIN
    UPDATE products 
    SET stock_quantity = stock_quantity - NEW.quantity
    WHERE product_id = NEW.product_id;
    
    -- Check if reorder needed
    IF (SELECT stock_quantity FROM products WHERE product_id = NEW.product_id) 
       <= (SELECT reorder_level FROM products WHERE product_id = NEW.product_id) THEN
        
        INSERT INTO reorder_alerts (product_id, alert_date, current_stock)
        VALUES (NEW.product_id, NOW(), 
                (SELECT stock_quantity FROM products WHERE product_id = NEW.product_id));
    END IF;
END$$
DELIMITER ;
```

---

## 📋 Summary & Practical Exercise

### Comprehensive Summary

Key Hierarchy:
1. Superkey: Any set of attributes that uniquely identifies tuples
2. Candidate Key: Minimal superkey (cannot remove any attributes)
3. Primary Key: Chosen candidate key for main identification
4. Foreign Key: Links to primary/candidate keys in other tables

Integrity Rules:
- Entity Integrity: Primary keys must never be NULL
- Referential Integrity: Foreign keys must reference existing values or be NULL

Additional Constraints:
- NOT NULL: Mandatory fields
- UNIQUE: Distinct values (allows one NULL)
- CHECK: Domain and business rule validation
- DEFAULT: Automatic value assignment

### 🧠 Practice Exercise: Enhanced Library System

Building on the previous library exercise, design a comprehensive schema with all constraint types:

Exercise Requirements:

1. BOOKS Table Enhancement:
   - Add appropriate primary key choice
   - Include foreign key to PUBLISHERS table
   - Add check constraints for business rules

2. Additional Tables:
   - PUBLISHERS(PublisherID, PublisherName, Address, Phone)
   - MEMBERS(MemberID, Name, Email, Phone, MembershipDate)
   - CHECKOUTS(CheckoutID, BookID, MemberID, CheckoutDate, DueDate, ReturnDate)

Your Task:
```sql
-- Complete this enhanced schema
CREATE TABLE publishers (
    -- Add appropriate attributes and constraints
);

CREATE TABLE books (
    book_id INTEGER PRIMARY KEY AUTO_INCREMENT,
    isbn VARCHAR(13) UNIQUE NOT NULL,
    title VARCHAR(200) NOT NULL,
    author VARCHAR(100) NOT NULL,
    publisher_id INTEGER,  -- Foreign key
    publication_year INTEGER,
    pages INTEGER,
    price DECIMAL(8,2),
    status ENUM('available', 'checked_out', 'reserved', 'damaged') DEFAULT 'available',
    
    -- Add appropriate constraints
    -- 1. Check constraint for publication year
    -- 2. Check constraint for pages
    -- 3. Check constraint for price
    -- 4. Foreign key constraint to publishers
);

CREATE TABLE members (
    -- Design member table with constraints
);

CREATE TABLE checkouts (
    -- Design checkout table with:
    -- 1. Composite or surrogate primary key
    -- 2. Foreign keys to books and members
    -- 3. Check constraints for dates
    -- 4. Business rule: due_date > checkout_date
);
```

Guided Questions:
1. Why choose `book_id` as primary key instead of `isbn`?
2. What foreign key actions should be used for the book-publisher relationship?
3. How would you prevent a book from being checked out if it's already checked out?
4. What constraints ensure realistic date relationships in checkouts?

Advanced Challenge:
Design constraints to handle:
- Maximum checkout period (e.g., 14 days)
- Member borrowing limits (e.g., maximum 5 books)
- Fine calculation for overdue books
- Reservation system for popular books

This exercise reinforces the practical application of all key and constraint concepts in a real-world scenario.

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.