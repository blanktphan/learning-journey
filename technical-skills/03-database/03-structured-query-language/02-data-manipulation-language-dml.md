# 📖 Data Manipulation Language (DML): INSERT, UPDATE, DELETE

## 🎯 Learning Objectives

Upon completion of this topic, you will be able to:

- Define and explain the role of DML in modifying and changing data within databases
- Write and understand the syntax of INSERT statements to add new data rows
- Write and understand the syntax of UPDATE statements to modify existing data, recognizing the importance of WHERE clauses
- Write and understand the syntax of DELETE statements to remove data, recognizing the importance of WHERE clauses

---

## 1. Introduction to DML

In the previous lesson, we learned about DQL (SELECT), which performs "read-only" operations to retrieve and view data. In this lesson, we will explore DML (Data Manipulation Language), which consists of commands used to "modify" data directly within tables.

DML is the heart of creating truly interactive applications because data in most systems is not static but constantly changing. Examples include new user registrations, posting messages, or updating product statuses. DML commands consist of three main statements: INSERT, UPDATE, and DELETE.

### Why DML is Essential:
- Enables dynamic data management in real-world applications
- Supports interactive user experiences
- Allows real-time data updates and modifications
- Forms the foundation of modern database-driven applications
- Essential for maintaining current and accurate information

### DML in Context:
```
Database Operations Hierarchy:
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

---

## 2. Adding Data: The INSERT Statement

The INSERT statement is used to add one or more new rows (tuples) into a table.

### Basic Syntax:
```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);
```

### Key Principles:
- **INSERT INTO table_name**: Specifies which table to add data to
- **(column1, column2, ...)**: Lists the column names where data will be inserted (best practice)
- **VALUES (value1, value2, ...)**: Specifies the actual data values, in the same order as the column list

### Example: Adding a New Student
Add a new student to the STUDENTS table:

```sql
INSERT INTO STUDENTS (StudentID, FullName, Major)
VALUES (2025001, 'Somkiat Kayan-rian', 'Computer Engineering');
```

### Sample STUDENTS Table Structure:
```
STUDENTS Table (Before INSERT):
┌──────────┬─────────────────────┬─────────────────┬─────┬─────────────────┐
│ StudentID│      FullName       │      Major      │ GPA │      Email      │
├──────────┼─────────────────────┼─────────────────┼─────┼─────────────────┤
│   001    │ John Smith          │ Computer Sci    │ 3.75│ john@email.com  │
│   002    │ Sarah Johnson       │ Mathematics     │ 3.90│ sarah@email.com │
│   003    │ Mike Brown          │ Physics         │ 3.25│ mike@email.com  │
└──────────┴─────────────────────┴─────────────────┴─────┴─────────────────┘
```

After INSERT operation:
```
STUDENTS Table (After INSERT):
┌──────────┬─────────────────────┬─────────────────┬─────┬─────────────────┐
│ StudentID│      FullName       │      Major      │ GPA │      Email      │
├──────────┼─────────────────────┼─────────────────┼─────┼─────────────────┤
│   001    │ John Smith          │ Computer Sci    │ 3.75│ john@email.com  │
│   002    │ Sarah Johnson       │ Mathematics     │ 3.90│ sarah@email.com │
│   003    │ Mike Brown          │ Physics         │ 3.25│ mike@email.com  │
│ 2025001  │ Somkiat Kayan-rian  │ Computer Eng    │ NULL│ NULL            │
└──────────┴─────────────────────┴─────────────────┴─────┴─────────────────┘
```

### INSERT Variations:

#### Insert with all columns specified:
```sql
INSERT INTO STUDENTS (StudentID, FullName, Major, GPA, Email)
VALUES (2025002, 'Anna Wilson', 'Data Science', 3.85, 'anna@university.edu');
```

#### Insert multiple rows at once:
```sql
INSERT INTO STUDENTS (StudentID, FullName, Major, GPA)
VALUES 
    (2025003, 'Peter Parker', 'Physics', 3.70),
    (2025004, 'Mary Jane', 'Chemistry', 3.65),
    (2025005, 'Tony Stark', 'Engineering', 3.95);
```

---

## 3. Modifying Data: The UPDATE Statement

The UPDATE statement is used to modify values in columns of existing rows in a table.

### Basic Syntax:
```sql
UPDATE table_name
SET column1 = new_value1, column2 = new_value2
WHERE condition;
```

### Critical Role of WHERE Clause:
- WHERE specifies which rows to update based on conditions
- **CRITICAL WARNING**: If you omit the WHERE clause, UPDATE will modify ALL rows in the table, which can cause severe data damage

### Example: Changing a Student's Major
Change the major of student with ID 2025001 to Data Science:

```sql
UPDATE STUDENTS
SET Major = 'Data Science'
WHERE StudentID = 2025001;
```

### Before UPDATE:
```
┌──────────┬─────────────────────┬─────────────────┐
│ StudentID│      FullName       │      Major      │
├──────────┼─────────────────────┼─────────────────┤
│ 2025001  │ Somkiat Kayan-rian  │ Computer Eng    │
└──────────┴─────────────────────┴─────────────────┘
```

### After UPDATE:
```
┌──────────┬─────────────────────┬─────────────────┐
│ StudentID│      FullName       │      Major      │
├──────────┼─────────────────────┼─────────────────┤
│ 2025001  │ Somkiat Kayan-rian  │ Data Science    │
└──────────┴─────────────────────┴─────────────────┘
```

### Additional UPDATE Examples:

#### Update multiple columns:
```sql
UPDATE STUDENTS
SET Major = 'Computer Science', GPA = 3.90
WHERE StudentID = 2025001;
```

#### Update with calculations:
```sql
-- Increase GPA by 0.1 for all Computer Science students
UPDATE STUDENTS
SET GPA = GPA + 0.1
WHERE Major = 'Computer Science';
```

### Dangerous UPDATE Example (What NOT to do):
```sql
-- DANGEROUS: Updates ALL students!
UPDATE STUDENTS
SET Major = 'Undeclared';
-- Without WHERE, every student's major becomes 'Undeclared'
```

---

## 4. Removing Data: The DELETE Statement

The DELETE statement is used to remove entire rows from a table.

### Basic Syntax:
```sql
DELETE FROM table_name
WHERE condition;
```

### Critical Role of WHERE Clause:
- Similar to UPDATE, WHERE specifies which rows to delete
- **CRITICAL WARNING**: If you omit the WHERE clause, DELETE will remove ALL rows from the table, which is typically irreversible

### Example: Removing a Student Record
Delete the student with ID 2025001:

```sql
DELETE FROM STUDENTS
WHERE StudentID = 2025001;
```

### Before DELETE:
```
STUDENTS Table (Before DELETE):
┌──────────┬─────────────────────┬─────────────────┬─────┐
│ StudentID│      FullName       │      Major      │ GPA │
├──────────┼─────────────────────┼─────────────────┼─────┤
│   001    │ John Smith          │ Computer Sci    │ 3.75│
│   002    │ Sarah Johnson       │ Mathematics     │ 3.90│
│ 2025001  │ Somkiat Kayan-rian  │ Data Science    │ 3.85│
└──────────┴─────────────────────┴─────────────────┴─────┘
```

### After DELETE:
```
STUDENTS Table (After DELETE):
┌──────────┬─────────────────────┬─────────────────┬─────┐
│ StudentID│      FullName       │      Major      │ GPA │
├──────────┼─────────────────────┼─────────────────┼─────┤
│   001    │ John Smith          │ Computer Sci    │ 3.75│
│   002    │ Sarah Johnson       │ Mathematics     │ 3.90│
└──────────┴─────────────────────┴─────────────────┴─────┘
```

### Dangerous DELETE Example (What NOT to do):
```sql
-- EXTREMELY DANGEROUS: Deletes ALL students!
DELETE FROM STUDENTS;
-- Without WHERE, every student record is deleted
```

---

## 5. Safety Best Practices for DML Operations

### Always Test with SELECT First:
```sql
-- Before UPDATE or DELETE, test the condition with SELECT
SELECT * FROM STUDENTS WHERE StudentID = 2025001;
-- If the result looks correct, then proceed with UPDATE/DELETE
UPDATE STUDENTS SET Major = 'Data Science' WHERE StudentID = 2025001;
```

### Use Transactions for Safety:
```sql
-- Start a transaction
BEGIN TRANSACTION;

-- Perform the operation
UPDATE STUDENTS SET GPA = 4.0 WHERE StudentID = 2025001;

-- Check the result
SELECT * FROM STUDENTS WHERE StudentID = 2025001;

-- If correct: COMMIT; If wrong: ROLLBACK
COMMIT;  -- or ROLLBACK;
```

### Create Backups Before Major Operations:
```sql
-- Create a backup table before major changes
CREATE TABLE STUDENTS_BACKUP AS SELECT * FROM STUDENTS;
```

---

## 📋 Summary & Practical Exercise

### Comprehensive Summary

DML is a group of SQL commands used to modify data, consisting of INSERT (add), UPDATE (modify), and DELETE (remove). The most crucial aspect is always using WHERE clauses with UPDATE and DELETE statements to ensure you operate on the correct data as intended.

#### Key Concepts Covered:
- **INSERT Statement**: Adds new records to tables with proper syntax and data type considerations
- **UPDATE Statement**: Modifies existing data with critical emphasis on WHERE clause usage
- **DELETE Statement**: Removes records with safety considerations and irreversible nature warnings
- **WHERE Clause Importance**: Essential for targeting specific rows in UPDATE and DELETE operations
- **Safety Practices**: Transaction management, backup strategies, and testing procedures
- **Common Pitfalls**: Data type mismatches, constraint violations, and missing WHERE clauses

#### DML Command Summary:
```
DML Operations Overview:
┌─────────────┬─────────────────────┬─────────────────────┐
│  Command    │      Purpose        │   Critical Notes    │
├─────────────┼─────────────────────┼─────────────────────┤
│   INSERT    │  Add new records    │  Check constraints  │
│   UPDATE    │  Modify existing    │  Always use WHERE   │
│   DELETE    │  Remove records     │  Always use WHERE   │
└─────────────┴─────────────────────┴─────────────────────┘
```

### Practical Exercise

Based on the BOOKS table structure: BOOKS(BookID, Title, Author, PublicationYear, Genre)

Consider this sample BOOKS table:
```
BOOKS Table:
┌────────┬─────────────────────┬─────────────────┬──────────────┬─────────────────┐
│ BookID │       Title         │     Author      │ Publication  │     Genre       │
│        │                     │                 │     Year     │                 │
├────────┼─────────────────────┼─────────────────┼──────────────┼─────────────────┤
│  001   │ Dune                │ Frank Herbert   │    1965      │ Science Fiction │
│  002   │ 1984                │ George Orwell   │    1949      │ Dystopian       │
│  003   │ Foundation          │ Isaac Asimov    │    1951      │ Science Fiction │
│  123   │ Old Science Book    │ John Doe        │    2020      │ Science         │
│  456   │ Outdated Manual     │ Jane Smith      │    1995      │ Reference       │
└────────┴─────────────────────┴─────────────────┴──────────────┴─────────────────┘
```

#### Exercise Questions:

**Question 1**: Write an INSERT statement to add a new book to the table.
```sql
-- Your solution here:
INSERT INTO BOOKS (BookID, Title, Author, PublicationYear, Genre)
VALUES (789, 'Modern Database Systems', 'Alice Johnson', 2024, 'Technology');
```

**Question 2**: Write an UPDATE statement to change the publication year of the book with BookID 123 to 2025.
```sql
-- Your solution here:
UPDATE BOOKS
SET PublicationYear = 2025
WHERE BookID = 123;
```

**Question 3**: Write a DELETE statement to remove the book with BookID 456.
```sql
-- Your solution here:
DELETE FROM BOOKS
WHERE BookID = 456;
```

#### Expected Results After All Operations:
```
BOOKS Table (Final State):
┌────────┬─────────────────────┬─────────────────┬──────────────┬─────────────────┐
│ BookID │       Title         │     Author      │ Publication  │     Genre       │
│        │                     │                 │     Year     │                 │
├────────┼─────────────────────┼─────────────────┼──────────────┼─────────────────┤
│  001   │ Dune                │ Frank Herbert   │    1965      │ Science Fiction │
│  002   │ 1984                │ George Orwell   │    1949      │ Dystopian       │
│  003   │ Foundation          │ Isaac Asimov    │    1951      │ Science Fiction │
│  123   │ Old Science Book    │ John Doe        │    2025      │ Science         │
│  789   │ Modern Database Sys │ Alice Johnson   │    2024      │ Technology      │
└────────┴─────────────────────┴─────────────────┴──────────────┴─────────────────┘
```

#### Additional Practice Challenges:

**Challenge 1**: Insert three books at once using a single INSERT statement.

**Challenge 2**: Update all books published before 1960 to have genre 'Classic Literature'.

**Challenge 3**: Delete all books with genre 'Reference' that were published before 2000.

**Challenge 4**: Create a safe UPDATE operation using a transaction to change an author's name, including rollback capability.

#### Safety Checklist:
Before executing any DML operation, remember to:
- [ ] Test conditions with SELECT first
- [ ] Always include WHERE clause for UPDATE and DELETE
- [ ] Backup important data before major changes
- [ ] Use transactions for critical operations
- [ ] Verify data types match table schema
- [ ] Check for constraint violations

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.