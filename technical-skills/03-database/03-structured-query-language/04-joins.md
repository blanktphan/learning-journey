# 📖 SQL JOINs: Combining Data from Multiple Tables

## 🎯 Learning Objectives

Upon completion of this topic, you will be able to:

- Explain the purpose of using JOINs to combine data from different tables
- Understand and write INNER JOIN statements, which are the most commonly used joins
- Distinguish the differences between INNER JOIN and OUTER JOINs (LEFT, RIGHT)
- Write LEFT JOIN statements to retrieve all data from one table even when there is no related data in another table

---

## 1. Introduction: The Power of Relational Data

From our lesson on Normalization, we learned that good database design involves breaking data into multiple tables to reduce redundancy. The important question is: How do we bring the separated data back together to display complete results? For example, how can we display "student names" alongside "course names" they are enrolled in, when this data exists in separate tables?

The answer is using JOINs, which are SQL commands used to "combine rows from two or more tables based on related columns between them." This is the mechanism that makes the "Relational" in RDBMS work in practice.

### Why JOINs are Essential:
- Enable data retrieval across normalized table structures
- Maintain data integrity while providing comprehensive views
- Support complex queries that span multiple entities
- Form the foundation of relational database querying
- Allow flexible data presentation without data duplication

### JOIN Concepts Overview:
```
Table Relationship Example:
┌─────────────────┐         ┌─────────────────┐
│    STUDENTS     │         │   ENROLLMENTS   │
├─────────────────┤         ├─────────────────┤
│ StudentID (PK)  │◄────────┤ StudentID (FK)  │
│ StudentName     │         │ CourseID        │
│ Major           │         │ Grade           │
└─────────────────┘         └─────────────────┘
```

---

## 2. Inner Join: Combining Tables with Matching Data

INNER JOIN is the most frequently used type of join. It returns only rows that have "matching values in the join condition from both tables."

### Analogy:
If visualized as a Venn diagram, INNER JOIN returns results only from the overlapping area where both circles intersect.

### Basic Syntax:
```sql
SELECT table1.column_name, table2.column_name
FROM table1
INNER JOIN table2 ON table1.related_column = table2.related_column;
```

### Key Components:
- **ON Clause**: Specifies the join condition, typically matching Primary Key from one table with Foreign Key from another table
- **Table Aliases**: Optional shorthand names for tables (AS keyword)
- **Column Selection**: Choose specific columns from either or both tables

### Example: Student Enrollments
Find "student names" and "course IDs" for each enrollment.

**Tables involved**: 
- STUDENTS(StudentID, StudentName, Major)
- ENROLLMENTS(StudentID, CourseID, Grade)

```sql
SELECT S.StudentName, E.CourseID
FROM STUDENTS AS S
INNER JOIN ENROLLMENTS AS E ON S.StudentID = E.StudentID;
```

### Sample Data and Results:

**STUDENTS Table:**
```
┌───────────┬─────────────────┬─────────────────┐
│ StudentID │   StudentName   │      Major      │
├───────────┼─────────────────┼─────────────────┤
│    001    │ John Smith      │ Computer Science│
│    002    │ Sarah Johnson   │ Mathematics     │
│    003    │ Mike Brown      │ Physics         │
│    004    │ Lisa Wilson     │ Computer Science│
└───────────┴─────────────────┴─────────────────┘
```

**ENROLLMENTS Table:**
```
┌───────────┬──────────┬───────┐
│ StudentID │ CourseID │ Grade │
├───────────┼──────────┼───────┤
│    001    │  CS101   │   A   │
│    001    │  MATH201 │   B   │
│    002    │  MATH201 │   A   │
│    002    │  STAT301 │   B+  │
│    004    │  CS101   │   A-  │
└───────────┴──────────┴───────┘
```

**INNER JOIN Result:**
```
┌─────────────────┬──────────┐
│   StudentName   │ CourseID │
├─────────────────┼──────────┤
│ John Smith      │  CS101   │
│ John Smith      │  MATH201 │
│ Sarah Johnson   │  MATH201 │
│ Sarah Johnson   │  STAT301 │
│ Lisa Wilson     │  CS101   │
└─────────────────┴──────────┘
```

**Note**: Mike Brown (StudentID 003) doesn't appear in results because he has no enrollments.

### More Complex INNER JOIN Examples:

#### Multiple Table Join:
```sql
SELECT S.StudentName, C.CourseName, E.Grade
FROM STUDENTS S
INNER JOIN ENROLLMENTS E ON S.StudentID = E.StudentID
INNER JOIN COURSES C ON E.CourseID = C.CourseID;
```

#### INNER JOIN with WHERE Conditions:
```sql
SELECT S.StudentName, E.CourseID, E.Grade
FROM STUDENTS S
INNER JOIN ENROLLMENTS E ON S.StudentID = E.StudentID
WHERE S.Major = 'Computer Science' AND E.Grade IN ('A', 'A+');
```

---

## 3. Outer Joins: Including Unmatched Data

Sometimes we need all data from one table, even when there are no matching records in another table. In these cases, we use OUTER JOINs.

### LEFT JOIN (or LEFT OUTER JOIN)

**Definition**: Returns ALL rows from the left table (first table after FROM) and matching rows from the right table. If no match exists in the right table, the right table columns will display as NULL.

### Example: All Students with Their Enrollments
Display all student names along with their enrolled courses (students who haven't enrolled should still appear in the list).

```sql
SELECT S.StudentName, E.CourseID
FROM STUDENTS AS S
LEFT JOIN ENROLLMENTS AS E ON S.StudentID = E.StudentID;
```

**LEFT JOIN Result:**
```
┌─────────────────┬──────────┐
│   StudentName   │ CourseID │
├─────────────────┼──────────┤
│ John Smith      │  CS101   │
│ John Smith      │  MATH201 │
│ Sarah Johnson   │  MATH201 │
│ Sarah Johnson   │  STAT301 │
│ Mike Brown      │   NULL   │  ← Appears with NULL CourseID
│ Lisa Wilson     │  CS101   │
└─────────────────┴──────────┘
```

**Key Difference**: Mike Brown now appears in the results with NULL CourseID because LEFT JOIN includes all students regardless of enrollment status.

### Visual Comparison: INNER vs LEFT JOIN

```
INNER JOIN (Intersection Only):
┌─────────────┐     ┌─────────────┐
│  STUDENTS   │     │ ENROLLMENTS │
│      ┌──────┼─────┼──────┐      │
│      │ ████ │     │ ████ │      │  ← Only overlapping data
│      └──────┼─────┼──────┘      │
│             │     │             │
└─────────────┘     └─────────────┘

LEFT JOIN (All from Left + Matches):
┌─────────────┐     ┌─────────────┐
│ ███████████ │     │ ENROLLMENTS │
│ ███████████ │     │      ████   │  ← All STUDENTS + matching ENROLLMENTS
│ ███████████ │     │             │
│             │     │             │
└─────────────┘     └─────────────┘
```

### RIGHT JOIN (or RIGHT OUTER JOIN)

**Definition**: Works opposite to LEFT JOIN - returns ALL rows from the right table (table after JOIN keyword). In practice, this is rarely used because it can always be rewritten as a LEFT JOIN by switching table order.

### Example: All Enrollments with Student Information
```sql
SELECT S.StudentName, E.CourseID
FROM STUDENTS AS S
RIGHT JOIN ENROLLMENTS AS E ON S.StudentID = E.StudentID;
```

### FULL OUTER JOIN

**Definition**: Returns all rows from both tables. If a row has no match in the other table, the columns from that table will show as NULL. It's like combining LEFT and RIGHT JOINs.

### Example: Complete Student and Enrollment Picture
```sql
SELECT S.StudentName, E.CourseID
FROM STUDENTS AS S
FULL OUTER JOIN ENROLLMENTS AS E ON S.StudentID = E.StudentID;
```

---

## 4. Practical Examples with Library Database

Let's work through examples using BOOKS and AUTHORS tables as mentioned in the Thai text.

### Database Schema:
```
AUTHORS Table:
┌──────────┬─────────────────┐
│ AuthorID │   AuthorName    │
├──────────┼─────────────────┤
│    101   │ Frank Herbert   │
│    102   │ Isaac Asimov    │
│    103   │ George Orwell   │
│    104   │ Jane Austen     │
└──────────┴─────────────────┘

BOOKS Table:
┌────────┬─────────────────────┬──────────┐
│ BookID │       Title         │ AuthorID │
├────────┼─────────────────────┼──────────┤
│   001  │ Dune                │   101    │
│   002  │ Foundation          │   102    │
│   003  │ 1984                │   103    │
│   004  │ I, Robot            │   102    │
└────────┴─────────────────────┴──────────┘
```

### Challenge 1: INNER JOIN for Book Titles and Author Names
Write an INNER JOIN to display book titles alongside their author names:

```sql
SELECT B.Title, A.AuthorName
FROM BOOKS AS B
INNER JOIN AUTHORS AS A ON B.AuthorID = A.AuthorID;
```

**Result:**
```
┌─────────────────────┬─────────────────┐
│       Title         │   AuthorName    │
├─────────────────────┼─────────────────┤
│ Dune                │ Frank Herbert   │
│ Foundation          │ Isaac Asimov    │
│ 1984                │ George Orwell   │
│ I, Robot            │ Isaac Asimov    │
└─────────────────────┴─────────────────┘
```

### Challenge 2: LEFT JOIN for All Authors with Their Books
Write a LEFT JOIN to display all author names with their book titles (authors without books should show NULL for title):

```sql
SELECT A.AuthorName, B.Title
FROM AUTHORS AS A
LEFT JOIN BOOKS AS B ON A.AuthorID = B.AuthorID;
```

**Result:**
```
┌─────────────────┬─────────────────────┐
│   AuthorName    │       Title         │
├─────────────────┼─────────────────────┤
│ Frank Herbert   │ Dune                │
│ Isaac Asimov    │ Foundation          │
│ Isaac Asimov    │ I, Robot            │
│ George Orwell   │ 1984                │
│ Jane Austen     │ NULL                │  ← No books in system
└─────────────────┴─────────────────────┘
```

---

## 5. Advanced JOIN Techniques

### Self-Join
Joining a table with itself to find relationships within the same table:

```sql
-- Find employees and their managers
SELECT E1.EmployeeName, E2.EmployeeName AS ManagerName
FROM EMPLOYEES E1
LEFT JOIN EMPLOYEES E2 ON E1.ManagerID = E2.EmployeeID;
```

### Multiple JOINs
Combining data from three or more tables:

```sql
SELECT S.StudentName, C.CourseName, P.ProfessorName
FROM STUDENTS S
INNER JOIN ENROLLMENTS E ON S.StudentID = E.StudentID
INNER JOIN COURSES C ON E.CourseID = C.CourseID
INNER JOIN PROFESSORS P ON C.ProfessorID = P.ProfessorID;
```

### JOINs with Aggregation
Combining joins with aggregate functions:

```sql
-- Count books per author
SELECT A.AuthorName, COUNT(B.BookID) AS BookCount
FROM AUTHORS A
LEFT JOIN BOOKS B ON A.AuthorID = B.AuthorID
GROUP BY A.AuthorID, A.AuthorName;
```

---

## 6. Performance Considerations

### Indexing for JOINs:
- Ensure join columns are indexed
- Primary keys are automatically indexed
- Foreign keys should be indexed for better performance

### JOIN Order:
- Start with the most selective table (smallest result set)
- Use WHERE conditions early to reduce data volume
- Consider query execution plans

### Best Practices:
```sql
-- Good: Use explicit JOIN syntax
SELECT S.StudentName, E.CourseID
FROM STUDENTS S
INNER JOIN ENROLLMENTS E ON S.StudentID = E.StudentID;

-- Avoid: Implicit joins (comma syntax)
SELECT S.StudentName, E.CourseID
FROM STUDENTS S, ENROLLMENTS E
WHERE S.StudentID = E.StudentID;
```

---

## 📋 Summary & Practical Exercise

### Comprehensive Summary

JOINs are commands for combining data from multiple tables using conditions specified in the ON clause. INNER JOIN returns results only for rows found in both tables, while LEFT JOIN returns all rows from the left table regardless of matches in the right table.

#### Key Concepts Covered:
- **INNER JOIN**: Returns only matching records from both tables
- **LEFT JOIN**: Returns all records from left table, matching records from right table
- **RIGHT JOIN**: Returns all records from right table, matching records from left table
- **FULL OUTER JOIN**: Returns all records from both tables
- **Join Conditions**: Using ON clause to specify relationship criteria
- **Table Aliases**: Shorthand notation for cleaner, more readable queries

#### JOIN Types Summary:
```
JOIN Types Overview:
┌─────────────────┬─────────────────────┬─────────────────────┐
│   JOIN Type     │      Result         │    Use Case         │
├─────────────────┼─────────────────────┼─────────────────────┤
│  INNER JOIN     │  Matching rows only │  Standard queries   │
│  LEFT JOIN      │  All from left +    │  Include all from   │
│                 │  matching from right│  primary table      │
│  RIGHT JOIN     │  All from right +   │  Rarely used        │
│                 │  matching from left │                     │
│  FULL OUTER     │  All from both      │  Complete picture   │
└─────────────────┴─────────────────────┴─────────────────────┘
```

### Practical Exercise

**Congratulations!** This concludes the final lesson of **Section 3: SQL Language**. You have now learned all the essential commands including querying (DQL), manipulation (DML), definition (DDL), and combining data from multiple tables (JOINs), which are extremely important skills.

In the current database world, there isn't only the relational model. In the next section, we will explore another family of databases that is gaining high popularity, designed for flexibility and handling large-scale data.

#### Challenge Problems Review:
From the schema with BOOKS(BookID, Title, AuthorID) and AUTHORS(AuthorID, AuthorName):

**Question 1**: Write an INNER JOIN to display book titles alongside author names.
```sql
SELECT B.Title, A.AuthorName
FROM BOOKS AS B
INNER JOIN AUTHORS AS A ON B.AuthorID = A.AuthorID;
```

**Question 2**: Write a LEFT JOIN to display all author names with their book titles (authors without books should show NULL for title).
```sql
SELECT A.AuthorName, B.Title
FROM AUTHORS AS A
LEFT JOIN BOOKS AS B ON A.AuthorID = B.AuthorID;
```

#### Additional Practice Challenges:

**Challenge 1**: Create a query showing students who haven't enrolled in any courses.
```sql
SELECT S.StudentName
FROM STUDENTS S
LEFT JOIN ENROLLMENTS E ON S.StudentID = E.StudentID
WHERE E.StudentID IS NULL;
```

**Challenge 2**: Find courses that have no enrolled students.
```sql
SELECT C.CourseName
FROM COURSES C
LEFT JOIN ENROLLMENTS E ON C.CourseID = E.CourseID
WHERE E.CourseID IS NULL;
```

**Challenge 3**: Create a comprehensive report showing all students, their majors, enrolled courses, and grades.
```sql
SELECT S.StudentName, S.Major, C.CourseName, E.Grade
FROM STUDENTS S
LEFT JOIN ENROLLMENTS E ON S.StudentID = E.StudentID
LEFT JOIN COURSES C ON E.CourseID = C.CourseID
ORDER BY S.StudentName, C.CourseName;
```

#### JOIN Best Practices Checklist:
- [ ] Use explicit JOIN syntax instead of comma-separated tables
- [ ] Always specify join conditions in ON clause
- [ ] Use table aliases for better readability
- [ ] Index join columns for better performance
- [ ] Choose appropriate JOIN type based on data requirements
- [ ] Test with sample data to verify results
- [ ] Consider NULL handling in LEFT/RIGHT JOINs
- [ ] Use meaningful column names in SELECT clause

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
