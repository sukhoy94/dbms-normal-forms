# DBMS normal forms

Normalization is a process in database design that organizes columns (attributes) and tables (relations) to minimize data redundancy. It involves dividing large tables into smaller, more manageable pieces without losing information.

## 1. First Normal Form (1NF)

Definition: A table is in 1NF if:

```
All columns contain only atomic (indivisible) values.
Each column contains values of a single type.
Each column contains only one value per row.
Each row is unique.
```

Example

```
| StudentID | Name       | Courses        |
|-----------|------------|----------------|
| 1         | Alice      | Math, English  |
| 2         | Bob        | Math, Science  |

| StudentID | Name       | Courses        |
|-----------|------------|----------------|
| 1         | Alice      | Math, English  |
| 2         | Bob        | Math, Science  |
```

To Convert to 1NF:

```
| StudentID | Name  | Course   |
|-----------|-------|----------|
| 1         | Alice | Math     |
| 1         | Alice | English  |
| 2         | Bob   | Math     |
| 2         | Bob   | Science  |
```

## 2. Second Normal Form (2NF)

Definition: A table is in 2NF if:
- It is in 1NF.
- All non-key attributes are fully functional dependent on the primary key.

To understand 2NF, we need to understand functional dependencies, particularly partial dependencies.

### Functional Dependency
A functional dependency occurs when one attribute uniquely determines another attribute. For example, if we know a student's ID, we can determine their name.

### Partial Dependency
A partial dependency occurs when a non-key attribute is functionally dependent on part of a composite key (but not the whole key). This situation arises only when the primary key is composite (consisting of two or more columns).

Example:

If the primary key is a composite key, each non-key attribute must depend on the whole key, not just part of it.

```
| StudentID | CourseID | Instructor | CourseName |
|-----------|----------|------------|------------|
| 1         | 101      | Prof. A    | Math       |
| 1         | 102      | Prof. B    | English    |
| 2         | 101      | Prof. A    | Math       |
| 2         | 103      | Prof. C    | Science    |

```


### Analysis for 2NF

Instructor depends on CourseID, not on the whole composite key (StudentID, CourseID).
CourseName depends on CourseID, not on the whole composite key (StudentID, CourseID).
These partial dependencies violate the 2NF rule. To convert this table into 2NF, we need to eliminate these partial dependencies.

```
Student Course Table:
| StudentID | CourseID |
|-----------|----------|
| 1         | 101      |
| 1         | 102      |
| 2         | 101      |
| 2         | 103      |


Course Table:
| CourseID | Instructor | CourseName |
|----------|------------|------------|
| 101      | Prof. A    | Math       |
| 102      | Prof. B    | English    |
| 103      | Prof. C    | Science    |

```

### Explanation
Student-Course Table: The StudentID and CourseID together form the composite primary key, and there are no partial dependencies because this table only contains these key attributes.

Course Table: The CourseID is now the primary key, and Instructor and CourseName are fully functionally dependent on CourseID, eliminating partial dependencies.

By decomposing the original table into these two tables, we ensure that every non-key attribute is fully functionally dependent on the entire primary key in each table. This decomposition achieves Second Normal Form (2NF), reducing redundancy and ensuring data integrity.


## 3. Third normal form

The Third Normal Form (3NF) is a database normalization level used to reduce data redundancy and ensure data integrity. A table is in 3NF if:

- It is in Second Normal Form (2NF).
- All the attributes are functionally dependent only on the primary key and nothing else (i.e., there are no transitive dependencies).

Example:


Consider a table storing information about employees, departments, and the location of the departments:
```
| EmployeeID | EmployeeName | DepartmentID | DepartmentName | DepartmentLocation |
|------------|--------------|--------------|----------------|--------------------|
| 1          | John         | D01          | HR             | New York           |
| 2          | Jane         | D02          | IT             | San Francisco      |
| 3          | Bob          | D01          | HR             | New York           |
| 4          | Alice        | D03          | Finance        | Chicago            |
```

In this table:

- The primary key is EmployeeID.
- DepartmentName and DepartmentLocation are non-key attributes.

Dependencies:

- EmployeeName depends on EmployeeID.
- DepartmentName depends on DepartmentID.
- DepartmentLocation depends on DepartmentID.
- DepartmentID determines DepartmentName and DepartmentLocation, so there is a transitive dependency: EmployeeID -> DepartmentID -> DepartmentName and DepartmentLocation.
- This table is in 2NF but not in 3NF because of the transitive dependencies.

To achieve 3NF, we need to eliminate the transitive dependencies by creating separate tables for employees and departments.

```
employee table

| EmployeeID | EmployeeName | DepartmentID |
|------------|--------------|--------------|
| 1          | John         | D01          |
| 2          | Jane         | D02          |
| 3          | Bob          | D01          |
| 4          | Alice        | D03          |

department table

| DepartmentID | DepartmentName | DepartmentLocation |
|--------------|----------------|--------------------|
| D01          | HR             | New York           |
| D02          | IT             | San Francisco      |
| D03          | Finance        | Chicago            |

```
