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
