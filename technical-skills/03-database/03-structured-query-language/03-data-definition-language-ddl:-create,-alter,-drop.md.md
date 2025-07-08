# 📖 Data Definition Language (DDL): CREATE, ALTER, DROP

## 🎯 Learning Objectives

Upon completion of this topic, you will be able to:

- Define and explain the role of DDL in creating and managing database schemas
- Write and understand the syntax of CREATE TABLE statements including column definitions, data types, and constraints
- Write and understand the syntax of ALTER TABLE statements to modify existing table structures
- Write and understand the syntax of DROP TABLE statements to permanently delete tables

---

## 1. Introduction to DDL

If DQL (SELECT) is for "reading" data and DML (INSERT, UPDATE, DELETE) is for "writing" data, then DDL (Data Definition Language) is for "creating containers" or structures to store that data.

DDL is a group of SQL commands used to create, modify, and delete various objects in a database. The most important object is the table. DDL commands work with the "structure" or "schema" of the database, not with the "data" contained within it.

### DDL vs Other SQL Categories:
```
SQL Command Categories:
┌─────────────────────────────────────────────┐
│                    SQL                      │
├─────────┬─────────┬─────────┬─────────────┤
│   DQL   │   DML   │   DDL   │     DCL     │
│ SELECT  │ INSERT  │ CREATE  │   GRANT     │
│ (Read)  │ UPDATE  │ ALTER   │   REVOKE    │
│         │ DELETE  │ DROP    │             │
│         │(Modify) │(Define) │(Control)    │
└─────────┴─────────┴─────────┴─────────────┘
```

### Key Characteristics of DDL:
- Works with database structure, not data content
- Changes are typically permanent and immediate
- Affects the schema definition of database objects
- Often requires administrative privileges
- Can impact database performance and storage

---

## 2. Creating Tables: The CREATE TABLE Statement

This command transforms the "blueprint" (schema) we designed into an actual table in the database.

### Basic Syntax:
```sql
CREATE TABLE table_name (
    column1_name    data_type   [column_constraint],
    column2_name    data_type   [column_constraint],
    ...
    [table_constraint]
);
```

### Components Breakdown:
- **table_name**: The name of the table to be created
- **column_name**: The name of each column (attribute)
- **data_type**: The data type for each column (e.g., INTEGER, VARCHAR(255), DATE, DECIMAL(10,2))
- **constraint**: Rules or restrictions such as PRIMARY KEY, FOREIGN KEY, NOT NULL, UNIQUE, CHECK

### Example: Creating the STUDENTS Table
Create the STUDENTS table we previously designed:

```sql
CREATE TABLE STUDENTS (
    StudentID   INT PRIMARY KEY,
    FirstName   VARCHAR(50) NOT NULL,
    LastName    VARCHAR(50) NOT NULL,
    Major       VARCHAR(100),
    GPA         DECIMAL(3, 2) CHECK (GPA >= 0.00 AND GPA <= 4.00)
);
```

### Common Data Types:

#### Numeric Types:
- **INT** or **INTEGER**: Whole numbers (-2,147,483,648 to 2,147,483,647)
- **DECIMAL(p,s)**: Fixed-point numbers (p=precision, s=scale)
- **FLOAT**: Floating-point numbers
- **DOUBLE**: Double-precision floating-point numbers

#### String Types:
- **VARCHAR(n)**: Variable-length strings up to n characters
- **CHAR(n)**: Fixed-length strings of exactly n characters
- **TEXT**: Large text fields for lengthy content

#### Date and Time Types:
- **DATE**: Date values (YYYY-MM-DD)
- **TIME**: Time values (HH:MM:SS)
- **DATETIME**: Combined date and time
- **TIMESTAMP**: Date and time with timezone information

### Common Constraints:
```sql
CREATE TABLE EXAMPLE_TABLE (
    ID          INT PRIMARY KEY,           -- Primary key constraint
    Name        VARCHAR(100) NOT NULL,     -- Cannot be null
    Email       VARCHAR(255) UNIQUE,       -- Must be unique
    Age         INT CHECK (Age >= 18),     -- Must satisfy condition
    Status      VARCHAR(20) DEFAULT 'Active' -- Default value
);
```

---

## 3. Modifying Table Structure: The ALTER TABLE Statement

Used to modify the structure of existing tables, such as adding, removing, or modifying columns.

### Common ALTER TABLE Operations:

#### Adding Columns:
```sql
ALTER TABLE table_name 
ADD COLUMN column_name data_type [constraints];
```

#### Dropping Columns:
```sql
ALTER TABLE table_name 
DROP COLUMN column_name;
```

#### Adding Constraints:
```sql
ALTER TABLE table_name 
ADD CONSTRAINT constraint_name constraint_definition;
```

### Example: Adding Email to STUDENTS Table
Add an Email column with unique constraint to the existing STUDENTS table:

```sql
ALTER TABLE STUDENTS
ADD COLUMN Email VARCHAR(100) UNIQUE;
```

### Before ALTER TABLE:
```
STUDENTS Table Structure (Before):
┌───────────┬─────────────┬─────────────────────┐
│  Column   │  Data Type  │    Constraints      │
├───────────┼─────────────┼─────────────────────┤
│ StudentID │     INT     │    PRIMARY KEY      │
│ FirstName │ VARCHAR(50) │     NOT NULL        │
│ LastName  │ VARCHAR(50) │     NOT NULL        │
│ Major     │VARCHAR(100) │        -            │
│ GPA       │DECIMAL(3,2) │ CHECK (0.00-4.00)   │
└───────────┴─────────────┴─────────────────────┘
```

### After ALTER TABLE:
```
STUDENTS Table Structure (After):
┌───────────┬──────────────┬─────────────────────┐
│  Column   │  Data Type   │    Constraints      │
├───────────┼──────────────┼─────────────────────┤
│ StudentID │     INT      │    PRIMARY KEY      │
│ FirstName │ VARCHAR(50)  │     NOT NULL        │
│ LastName  │ VARCHAR(50)  │     NOT NULL        │
│ Major     │ VARCHAR(100) │        -            │
│ GPA       │ DECIMAL(3,2) │ CHECK (0.00-4.00)   │
│ Email     │ VARCHAR(100) │      UNIQUE         │
└───────────┴──────────────┴─────────────────────┘
```

### Important Considerations:
- **Performance Impact**: ALTER TABLE operations on large tables with massive amounts of data can be resource-intensive and time-consuming
- **Data Compatibility**: Ensure existing data is compatible with new constraints
- **Backup First**: Always backup data before major structural changes
- **Downtime**: Large tables may require maintenance windows for ALTER operations

---

## 4. Removing Tables: The DROP TABLE Statement

Used to permanently delete a table from the database, removing the structure, all data, and related objects (such as indexes).

### Basic Syntax:
```sql
DROP TABLE table_name;
```

### Critical Warning:
The DROP TABLE command is **irreversible** and extremely dangerous because it destroys everything related to that table. It must be used with the highest level of caution.

### What DROP TABLE Removes:
- All table data (every row)
- Table structure definition
- All indexes associated with the table
- All constraints defined on the table
- All triggers associated with the table
- All permissions granted on the table

### Example: Removing a Table
```sql
DROP TABLE STUDENTS;
```

### Result of DROP TABLE:
```
Before DROP TABLE:
┌─────────────────────────────────────┐
│         STUDENTS Table              │
├─────────────────────────────────────┤
│ • Table structure exists            │
│ • Contains student data             │
│ • Has indexes and constraints       │
│ • Accessible for queries            │
└─────────────────────────────────────┘

After DROP TABLE:
┌─────────────────────────────────────┐
│            NOTHING                  │
├─────────────────────────────────────┤
│ • Table completely removed          │
│ • All data permanently lost         │
│ • Structure definition gone         │
│ • Cannot be recovered easily        │
└─────────────────────────────────────┘
```

### Safety Measures for DROP TABLE:

#### Create Backup First:
```sql
-- Create backup before dropping
CREATE TABLE STUDENTS_BACKUP AS SELECT * FROM STUDENTS;
-- Now safe to drop original
DROP TABLE STUDENTS;
```

#### Check Dependencies:
```sql
-- Check if other tables reference this table
SELECT * FROM INFORMATION_SCHEMA.KEY_COLUMN_USAGE 
WHERE REFERENCED_TABLE_NAME = 'STUDENTS';
```

#### Use IF EXISTS (where supported):
```sql
DROP TABLE IF EXISTS STUDENTS;
```

---

## 5. Advanced DDL Concepts

### Creating Tables with Foreign Keys:
```sql
CREATE TABLE STUDENTS (
    StudentID   INT PRIMARY KEY,
    FirstName   VARCHAR(50) NOT NULL,
    LastName    VARCHAR(50) NOT NULL,
    Major       VARCHAR(100)
);

CREATE TABLE ENROLLMENTS (
    EnrollmentID    INT PRIMARY KEY,
    StudentID       INT,
    CourseCode      VARCHAR(10),
    Grade           CHAR(2),
    
    FOREIGN KEY (StudentID) REFERENCES STUDENTS(StudentID)
);
```

### Creating Indexes:
```sql
CREATE INDEX idx_student_lastname ON STUDENTS(LastName);
CREATE INDEX idx_student_major ON STUDENTS(Major);
```

### Best Practices for DDL Operations:

#### Planning and Design:
- Design tables thoroughly before creation
- Consider future requirements and scalability
- Plan for data relationships and constraints
- Choose appropriate data types and sizes

#### Safety Measures:
- Always backup before major changes
- Test DDL statements on development systems first
- Use transactions where possible
- Document all structural changes

---

## 📋 Summary & Practical Exercise

### Comprehensive Summary

DDL commands (CREATE, ALTER, DROP) are used to manage the "structure" of databases, not the data itself. CREATE builds new objects, ALTER modifies existing structures, and DROP permanently removes objects. These commands have significant impact and are often irreversible.

#### Key Concepts Covered:
- **CREATE TABLE**: Building database tables with proper data types and constraints
- **ALTER TABLE**: Modifying existing table structures safely and efficiently
- **DROP TABLE**: Permanently removing tables with proper safety considerations
- **Data Types**: Choosing appropriate types for different kinds of data (INT, VARCHAR, DECIMAL, DATE)
- **Constraints**: Implementing business rules and data integrity (PRIMARY KEY, NOT NULL, UNIQUE, CHECK)
- **Safety Practices**: Backup strategies, testing procedures, and impact considerations

#### DDL Command Summary:
```
DDL Operations Overview:
┌─────────────┬─────────────────────┬─────────────────────┐
│  Command    │      Purpose        │   Critical Notes    │
├─────────────┼─────────────────────┼─────────────────────┤
│   CREATE    │  Build new tables   │  Define structure   │
│   ALTER     │  Modify existing    │  Performance impact │
│   DROP      │  Remove permanently │  IRREVERSIBLE!      │
└─────────────┴─────────────────────┴─────────────────────┘
```

### Practical Exercise

Based on the BOOKS table structure: BOOKS(BookID, Title, Author, PublicationYear, Genre)

#### Exercise Questions:

**Question 1**: Write a complete CREATE TABLE statement for this table, with BookID as PRIMARY KEY and Title as NOT NULL.

```sql
-- Your solution here:
CREATE TABLE BOOKS (
    BookID          INT PRIMARY KEY,
    Title           VARCHAR(255) NOT NULL,
    Author          VARCHAR(200),
    PublicationYear INT,
    Genre           VARCHAR(100)
);
```

**Question 2**: Write an ALTER TABLE statement to add a new column named ISBN which is VARCHAR(13) and must be UNIQUE.

```sql
-- Your solution here:
ALTER TABLE BOOKS
ADD COLUMN ISBN VARCHAR(13) UNIQUE;
```

**Question 3**: (Theoretical) What command would completely remove the BOOKS table?

```sql
-- Your solution here:
DROP TABLE BOOKS;
```

#### Expected Results After Operations:

**After CREATE TABLE:**
```
BOOKS Table Structure (Initial):
┌─────────────────┬──────────────┬─────────────────────┐
│     Column      │  Data Type   │    Constraints      │
├─────────────────┼──────────────┼─────────────────────┤
│ BookID          │     INT      │    PRIMARY KEY      │
│ Title           │ VARCHAR(255) │     NOT NULL        │
│ Author          │ VARCHAR(200) │        -            │
│ PublicationYear │     INT      │        -            │
│ Genre           │ VARCHAR(100) │        -            │
└─────────────────┴──────────────┴─────────────────────┘
```

**After ALTER TABLE (adding ISBN):**
```
BOOKS Table Structure (Final):
┌─────────────────┬──────────────┬─────────────────────┐
│     Column      │  Data Type   │    Constraints      │
├─────────────────┼──────────────┼─────────────────────┤
│ BookID          │     INT      │    PRIMARY KEY      │
│ Title           │ VARCHAR(255) │     NOT NULL        │
│ Author          │ VARCHAR(200) │        -            │
│ PublicationYear │     INT      │        -            │
│ Genre           │ VARCHAR(100) │        -            │
│ ISBN            │ VARCHAR(13)  │      UNIQUE         │
└─────────────────┴──────────────┴─────────────────────┘
```

**After DROP TABLE:**
```
Result: Table BOOKS no longer exists
┌─────────────────────────────────────┐
│            NOTHING                  │
├─────────────────────────────────────┤
│ • Table completely removed          │
│ • All data permanently lost         │
│ • Structure definition gone         │
│ • Cannot be recovered without backup│
└─────────────────────────────────────┘
```

#### Additional Practice Challenges:

**Challenge 1**: Create a complete library system with multiple tables including foreign key relationships.

**Challenge 2**: Design a table with various constraint types (CHECK, DEFAULT, NOT NULL) for a student management system.

**Challenge 3**: Practice safe ALTER operations by adding constraints to existing tables with data.

**Challenge 4**: Create a sequence of DDL operations that can be safely rolled back using transactions.

#### Safety Checklist for DDL Operations:
Before executing any DDL operation, remember to:
- [ ] Plan the table structure thoroughly
- [ ] Choose appropriate data types and constraints
- [ ] Create backups before major changes
- [ ] Test on development environment first
- [ ] Consider performance impact on large tables
- [ ] Document all structural changes
- [ ] Verify foreign key dependencies before DROP operations
- [ ] Use descriptive and consistent naming conventions

#### Common DDL Patterns:
```sql
-- Safe table creation with comprehensive constraints
CREATE TABLE EXAMPLE (
    ID          INT PRIMARY KEY,
    Name        VARCHAR(100) NOT NULL,
    Email       VARCHAR(255) UNIQUE,
    Age         INT CHECK (Age >= 0 AND Age <= 150),
    Status      VARCHAR(20) DEFAULT 'Active',
    CreatedDate TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Safe table modification sequence
ALTER TABLE EXAMPLE ADD COLUMN Phone VARCHAR(15);
ALTER TABLE EXAMPLE ADD CONSTRAINT chk_phone CHECK (Phone LIKE '+%');

-- Safe table removal (with backup)
CREATE TABLE EXAMPLE_BACKUP AS SELECT * FROM EXAMPLE;
DROP TABLE EXAMPLE;
```

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.