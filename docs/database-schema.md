# Database Schema Notes

This project is designed around a relational database-backed CRUD workflow.

## Core idea

A CRUD application usually needs at least one table that represents the records being created, viewed, updated, and deleted.

Example employee-style table:

```sql
CREATE TABLE employees (
    id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    email VARCHAR(255) NOT NULL,
    department VARCHAR(100),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## Common queries

Create record:

```sql
INSERT INTO employees (first_name, last_name, email, department)
VALUES (?, ?, ?, ?);
```

Read records:

```sql
SELECT id, first_name, last_name, email, department
FROM employees
ORDER BY last_name, first_name;
```

Update record:

```sql
UPDATE employees
SET first_name = ?, last_name = ?, email = ?, department = ?
WHERE id = ?;
```

Delete record:

```sql
DELETE FROM employees
WHERE id = ?;
```

## Security notes

- Do not commit real database credentials.
- Use prepared statements for user-provided input.
- Validate form input before writing to the database.
- Avoid displaying raw database errors to users in production.
