# 📖 Data Query Language (DQL): SELECT Statement

## 🎯 Learning Objectives

Upon completion of this topic, you will be able to:

- Define SQL and explain its role as the standard query language for RDBMS
- Identify and explain the important sub-languages of SQL (DQL, DML, DDL, DCL)
- Understand the basic structure and syntax of the SELECT statement
- Write queries to retrieve data from a single table using SELECT, FROM, and WHERE clauses

---

## 1. Introduction to SQL

SQL (Structured Query Language), pronounced as "SEE-quel" or "S-Q-L", is a structured query language that serves as the ANSI/ISO standard language specifically designed for managing and querying data in Relational Database Management Systems (RDBMS).

A distinctive characteristic of SQL is that it is a declarative language. This means users "declare" what results they want (What) without needing to specify how the computer should retrieve the data (How). The responsibility of finding the most efficient method falls to the Query Optimizer within the DBMS.

### Key Features of SQL:
- Standardized across different database systems
- Declarative nature - focus on what, not how
- Powerful data manipulation capabilities
- Supports complex queries and operations
- Case-insensitive keywords (though data may be case-sensitive)

---

## 2. Sub-languages of SQL

SQL can be divided into four main categories of commands:

### DQL (Data Query Language)
- Purpose: Query and retrieve data
- Primary command: SELECT
- Most frequently used category in daily operations

### DML (Data Manipulation Language)
- Purpose: Manipulate data within tables
- Commands: INSERT, UPDATE, DELETE
- Used for adding, modifying, and removing records

### DDL (Data Definition Language)
- Purpose: Define and manage database structure
- Commands: CREATE, ALTER, DROP
- Used for creating and modifying database objects like tables, indexes

### DCL (Data Control Language)
- Purpose: Control data access and permissions
- Commands: GRANT, REVOKE
- Used for managing user privileges and security

```
SQL Command Categories:
┌─────────────────────────────────────────────┐
│                    SQL                      │
├─────────┬─────────┬─────────┬─────────────┤
│   DQL   │   DML   │   DDL   │     DCL     │
│ SELECT  │ INSERT  │ CREATE  │   GRANT     │
│         │ UPDATE  │ ALTER   │   REVOKE    │
│         │ DELETE  │ DROP    │             │
└─────────┴─────────┴─────────┴─────────────┘
```

In this lesson, we will focus on DQL, which is the most commonly used category.

---

## 3. SELECT Statement: The Heart of Data Querying

The SELECT statement is used to retrieve data from a database. The most basic structure consists of two essential parts:

```sql
SELECT column1, column2, ...
FROM table_name;
```

### Components Breakdown:
- SELECT: Specifies which columns you want to display
- FROM: Specifies which table to retrieve data from

### Selecting All Columns
To retrieve all columns from a table, use the wildcard symbol (*):

```sql
SELECT * FROM STUDENTS;
```

### Example with Sample Data
Consider a STUDENTS table:

```
STUDENTS Table:
┌──────────┬─────────────────┬─────────────┬─────┬─────────────────┐
│ StudentID│    FullName     │    Major    │ GPA │   Email         │
├──────────┼─────────────────┼─────────────┼─────┼─────────────────┤
│   001    │ John Smith      │ Computer Sci│ 3.75│ john@email.com  │
│   002    │ Sarah Johnson   │ Mathematics │ 3.90│ sarah@email.com │
│   003    │ Mike Brown      │ Physics     │ 3.25│ mike@email.com  │
│   004    │ Lisa Wilson     │ Computer Sci│ 3.60│ lisa@email.com  │
└──────────┴─────────────────┴─────────────┴─────┴─────────────────┘
```

Basic SELECT examples:

```sql
-- Select specific columns
SELECT FullName, Major FROM STUDENTS;

-- Select all columns
SELECT * FROM STUDENTS;

-- Select single column
SELECT FullName FROM STUDENTS;
```

---

## 4. Filtering Data with WHERE Clause

The WHERE clause is used to filter rows based on specified conditions. It selects only the rows that meet the given criteria.

### Basic Syntax:
```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

The condition is a logical expression that evaluates to either TRUE or FALSE for each row.

### Example: High-Performing Students
Find the names and majors of students with GPA greater than 3.50:

```sql
SELECT FullName, Major
FROM STUDENTS
WHERE GPA > 3.50;
```

Result:
```
┌─────────────────┬─────────────┐
│    FullName     │    Major    │
├─────────────────┼─────────────┤
│ John Smith      │ Computer Sci│
│ Sarah Johnson   │ Mathematics │
│ Lisa Wilson     │ Computer Sci│
└─────────────────┴─────────────┘
```

### Common WHERE Operators:

```sql
-- Comparison operators
WHERE GPA > 3.5          -- Greater than
WHERE GPA >= 3.5         -- Greater than or equal
WHERE GPA < 3.0          -- Less than
WHERE GPA <= 3.0         -- Less than or equal
WHERE GPA = 3.75         -- Equal to
WHERE GPA != 3.0         -- Not equal to (or <> )

-- Text comparison
WHERE Major = 'Computer Science'
WHERE FullName LIKE 'John%'      -- Starts with 'John'
WHERE Email LIKE '%@gmail.com'   -- Ends with '@gmail.com'

-- Multiple conditions
WHERE GPA > 3.0 AND Major = 'Computer Science'
WHERE GPA > 3.8 OR Major = 'Mathematics'
WHERE GPA BETWEEN 3.0 AND 3.8
WHERE Major IN ('Computer Science', 'Mathematics', 'Physics')
```

### Processing Flow
When executing a SELECT statement with WHERE:

1. DBMS goes to the specified table (FROM clause)
2. Applies the filter condition to all rows (WHERE clause)
3. Selects only rows that satisfy the condition
4. Returns the specified columns (SELECT clause) from filtered rows

```
Query Processing Flow:
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   FROM      │───▶│   WHERE     │───▶│   SELECT    │
│ (Get Table) │    │ (Filter)    │    │ (Project)   │
└─────────────┘    └─────────────┘    └─────────────┘
```

---

## 5. Practical Examples

### Library Database Example
Consider a BOOKS table:

```
BOOKS Table:
┌────────┬─────────────────────┬─────────────────┬──────────────┬─────────────────┐
│ BookID │       Title         │     Author      │ Publication  │     Genre       │
│        │                     │                 │     Year     │                 │
├────────┼─────────────────────┼─────────────────┼──────────────┼─────────────────┤
│  001   │ Dune                │ Frank Herbert   │    1965      │ Science Fiction │
│  002   │ 1984                │ George Orwell   │    1949      │ Dystopian       │
│  003   │ Foundation          │ Isaac Asimov    │    1951      │ Science Fiction │
│  004   │ Neuromancer         │ William Gibson  │    1984      │ Science Fiction │
│  005   │ The Martian         │ Andy Weir       │    2011      │ Science Fiction │
└────────┴─────────────────────┴─────────────────┴──────────────┴─────────────────┘
```

Query examples:

```sql
-- All science fiction books
SELECT Title, Author
FROM BOOKS
WHERE Genre = 'Science Fiction';

-- Books published after 2000
SELECT Title, PublicationYear
FROM BOOKS
WHERE PublicationYear > 2000;

-- Science fiction books published after 1980
SELECT Title, Author, PublicationYear
FROM BOOKS
WHERE Genre = 'Science Fiction' AND PublicationYear > 1980;
```

---

## Practice Exercises

### Exercise 1: Basic SELECT
Given the STUDENTS table shown earlier, write queries to:

1. Display all student information
2. Show only student names and emails
3. List all unique majors

### Exercise 2: WHERE Conditions
Write queries to find:

1. Students with GPA exactly 3.75
2. Students whose major is not 'Physics'
3. Students with GPA between 3.5 and 3.8 (inclusive)

### Exercise 3: Library Challenge
From the BOOKS table, write a SQL command to find the title and publication year of all books in the 'Science Fiction' genre that were published after the year 2000.

Expected query structure:
```sql
SELECT Title, PublicationYear
FROM BOOKS
WHERE Genre = 'Science Fiction' AND PublicationYear > 2000;
```

### Exercise 4: Complex Conditions
Write queries using the STUDENTS table to:

1. Find Computer Science students with GPA above 3.6
2. Find students whose names start with 'S' or have GPA above 3.8
3. List students whose email contains 'gmail'

---

## Summary

SQL is the standard language for working with relational databases, consisting of various sub-languages. The SELECT statement is the primary command in the DQL group used for querying data. The FROM clause specifies the table source, and the WHERE clause filters rows based on specified conditions.

Key concepts covered:
- SQL as a declarative language
- Four main SQL sub-languages (DQL, DML, DDL, DCL)
- Basic SELECT syntax with FROM and WHERE
- Logical conditions and comparison operators
- Query processing flow and filtering mechanisms

Understanding these fundamentals provides the foundation for more advanced SQL operations and complex data retrieval scenarios.

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.