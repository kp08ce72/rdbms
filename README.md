### **Unit I: Introduction to Database System and SQL Commands (Oracle Syntax)**

---

#### **1.1 Concepts and Definitions**
- **Database**: An organized collection of structured data, typically stored electronically.
- **Database Systems**: Software systems designed to manage databases, e.g., Oracle Database, MySQL.
- **Database Environment**: The hardware, software, data, procedures, and people involved in managing and using a database.

#### **1.2 Data Terminology**
- **Data**: Raw facts that require processing to be meaningful.
- **Information**: Processed data that is meaningful and useful.
- **Data Item or Fields**: A single piece of data, e.g., a name or ID.
- **Records**: A collection of related fields, e.g., a row in a table.
- **Files**: A collection of related records.
- **Metadata**: Data about data; provides information about other data (e.g., file size, author).
- **Data Dictionary**: A centralized repository of metadata.  
   - Components: Tables, Columns, Data types, Constraints, etc.

#### **1.3 Schemas, Sub-schemas, and Instances**
- **Schema**: The structure of a database, defining tables, fields, and relationships.
- **Sub-schema**: A subset of the schema tailored for specific users.
- **Instance**: The actual content of the database at a given point in time.

#### **1.4 Data Types**
Common Oracle data types include:
- **NUMBER**: Numeric values.
- **VARCHAR2**: Variable-length character strings.
- **DATE**: Stores dates and times.
- **CHAR**: Fixed-length character strings.
- **FLOAT**: Floating-point numbers.

---

### **1.5 Database Language Commands (Oracle DDL)**

#### **DDL (Data Definition Language)**
Used to define and modify database structures.
- **CREATE**: Creates new tables, databases, indexes, or views.
   ```sql
   CREATE TABLE students (id NUMBER, name VARCHAR2(50), age NUMBER);
   ```
- **ALTER**: Modifies an existing database object like a table.
   ```sql
   ALTER TABLE students ADD address VARCHAR2(100);
   ```
- **TRUNCATE**: Removes all rows from a table but retains the structure.
   ```sql
   TRUNCATE TABLE students;
   ```
- **DROP**: Deletes a table or database.
   ```sql
   DROP TABLE students;
   ```

---

### **1.6 DML (Data Manipulation Language - Oracle)**

Used to manipulate data in the database.
- **INSERT**: Adds new records to a table.
   ```sql
   INSERT INTO students (id, name, age) VALUES (1, 'Rahul', 22);
   ```
- **SELECT**: Retrieves data from the database.
   ```sql
   SELECT * FROM students;
   ```
- **UPDATE**: Modifies existing records in a table.
   ```sql
   UPDATE students SET age = 23 WHERE id = 1;
   ```
- **DELETE**: Removes records from a table.
   ```sql
   DELETE FROM students WHERE id = 1;
   ```

---

### **1.7 Transactional Control Commands (Oracle)**

Oracle supports transactional control for managing transactions within the database.
- **COMMIT**: Saves all changes made during the transaction.
   ```sql
   COMMIT;
   ```
- **SAVEPOINT**: Sets a point in a transaction to which one can rollback.
   ```sql
   SAVEPOINT sp1;
   ```
- **ROLLBACK**: Undoes changes to the last commit or to a specific savepoint.
   ```sql
   ROLLBACK TO sp1;
   ```

---

### **1.8 DCL (Data Control Language - Oracle)**

Used to control access to data within the database.
- **GRANT**: Provides specific users access privileges.
   ```sql
   GRANT SELECT, INSERT ON students TO user1;
   ```
- **REVOKE**: Removes access privileges from users.
   ```sql
   REVOKE SELECT, INSERT ON students FROM user1;
   ```

   ### **Unit II: SQL Cheat Sheet – In-Built Functions and Joins**

---

### **2.1.1 Operators**

#### **1. Arithmetic Operators**: Perform mathematical operations.
- `+`, `-`, `*`, `/`

#### **2. Comparison Operators**: Compare two values.
- `=`, `!=`, `>`, `<`, `>=`, `<=`

#### **3. Logical Operators**: Combine multiple conditions.
- **AND**: All conditions must be true.
- **OR**: At least one condition must be true.
- **NOT**: Reverses the result of a condition.

---

### **2.1.2 SQL Functions**

#### **a> Single Row Functions (Scalar Functions)**: Operate on individual rows and return a single result for each row.

##### **i. Date Functions**
- **ADD_MONTHS**: Adds a specified number of months to a date.
   ```sql
   SELECT ADD_MONTHS(SYSDATE, 6) FROM dual;
   ```
- **MONTHS_BETWEEN**: Returns the number of months between two dates.
   ```sql
   SELECT MONTHS_BETWEEN('01-JAN-2023', '01-MAY-2023') FROM dual;
   ```
- **ROUND**: Rounds a date to the nearest day, month, or year.
   ```sql
   SELECT ROUND(SYSDATE, 'MONTH') FROM dual;
   ```
- **TRUNC**: Truncates a date to a specified format (day, month, year).
   ```sql
   SELECT TRUNC(SYSDATE, 'YEAR') FROM dual;
   ```

##### **ii. Numeric Functions**
- **ABS**: Returns the absolute value of a number.
   ```sql
   SELECT ABS(-10) FROM dual;
   ```
- **POWER**: Raises a number to a specified power.
   ```sql
   SELECT POWER(2, 3) FROM dual;
   ```
- **MOD**: Returns the remainder of a division.
   ```sql
   SELECT MOD(10, 3) FROM dual;
   ```
- **ROUND**: Rounds a number to a specified decimal point.
   ```sql
   SELECT ROUND(123.456, 2) FROM dual;
   ```
- **TRUNC**: Truncates a number to a specified number of decimal places.
   ```sql
   SELECT TRUNC(123.456, 2) FROM dual;
   ```
- **SQRT**: Returns the square root of a number.
   ```sql
   SELECT SQRT(16) FROM dual;
   ```

##### **iii. Character Functions**
- **INITCAP**: Capitalizes the first letter of each word.
   ```sql
   SELECT INITCAP('sql tutorial') FROM dual;
   ```
- **LOWER**: Converts a string to lowercase.
   ```sql
   SELECT LOWER('HELLO') FROM dual;
   ```
- **UPPER**: Converts a string to uppercase.
   ```sql
   SELECT UPPER('hello') FROM dual;
   ```
- **LTRIM**: Removes leading characters from a string.
   ```sql
   SELECT LTRIM('000123', '0') FROM dual;
   ```
- **RTRIM**: Removes trailing characters from a string.
   ```sql
   SELECT RTRIM('123000', '0') FROM dual;
   ```
- **REPLACE**: Replaces all occurrences of a substring within a string.
   ```sql
   SELECT REPLACE('hello world', 'world', 'SQL') FROM dual;
   ```
- **SUBSTR**: Extracts a substring from a string.
   ```sql
   SELECT SUBSTR('SQL Tutorial', 1, 3) FROM dual;
   ```
- **INSTR**: Returns the position of a substring within a string.
   ```sql
   SELECT INSTR('SQL Tutorial', 'T') FROM dual;
   ```

##### **iv. Conversion Functions**
- **TO_CHAR**: Converts a date or number to a string.
   ```sql
   SELECT TO_CHAR(SYSDATE, 'DD-MM-YYYY') FROM dual;
   ```
- **TO_DATE**: Converts a string to a date.
   ```sql
   SELECT TO_DATE('2023-08-10', 'YYYY-MM-DD') FROM dual;
   ```
- **TO_NUMBER**: Converts a string to a number.
   ```sql
   SELECT TO_NUMBER('12345') FROM dual;
   ```

---

### **Aggregate Functions (Group Functions)**
- **COUNT**: Counts rows in a result set.
   ```sql
   SELECT COUNT(*) FROM students;
   ```
- **SUM**: Returns the sum of numeric values.
   ```sql
   SELECT SUM(salary) FROM employees;
   ```
- **AVG**: Returns the average of numeric values.
   ```sql
   SELECT AVG(salary) FROM employees;
   ```
- **MAX**: Returns the maximum value.
   ```sql
   SELECT MAX(salary) FROM employees;
   ```
- **MIN**: Returns the minimum value.
   ```sql
   SELECT MIN(salary) FROM employees;
   ```

---

### **2.2 Group By, Having, and Order By Clauses**

- **GROUP BY**: Groups rows that have the same values in specified columns.
   ```sql
   SELECT department, COUNT(*) FROM employees GROUP BY department;
   ```

- **HAVING**: Filters rows after grouping (works like WHERE but for aggregated data).
   ```sql
   SELECT department, COUNT(*) FROM employees GROUP BY department HAVING COUNT(*) > 5;
   ```

- **ORDER BY**: Sorts the result set by one or more columns.
   ```sql
   SELECT * FROM employees ORDER BY salary DESC;
   ```

---

### **2.3 Joins**

#### **a> Inner or Simple Joins**
- **Equi-Join**: Uses equality (`=`) to join related columns from two tables.
   ```sql
   SELECT e.name, d.department_name 
   FROM employees e JOIN departments d 
   ON e.department_id = d.department_id;
   ```

- **Non-Equi Join**: Uses other operators (`<`, `>`, etc.) to join tables.
   ```sql
   SELECT e.name, s.grade 
   FROM employees e JOIN salary_grades s 
   ON e.salary BETWEEN s.low AND s.high;
   ```

- **Self-Join**: Joins a table to itself.
   ```sql
   SELECT e1.name, e2.name 
   FROM employees e1 JOIN employees e2 
   ON e1.manager_id = e2.employee_id;
   ```

#### **b> Outer Joins**
- **Left Outer Join**: Returns all rows from the left table and matching rows from the right.
   ```sql
   SELECT e.name, d.department_name 
   FROM employees e LEFT JOIN departments d 
   ON e.department_id = d.department_id;
   ```

- **Right Outer Join**: Returns all rows from the right table and matching rows from the left.
   ```sql
   SELECT e.name, d.department_name 
   FROM employees e RIGHT JOIN departments d 
   ON e.department_id = d.department_id;
   ```

- **Full Outer Join**: Returns rows when there is a match in either table.
   ```sql
   SELECT e.name, d.department_name 
   FROM employees e FULL JOIN departments d 
   ON e.department_id = d.department_id;
   ```

#### **c> Cross Join**
- **Cross Join**: Returns the Cartesian product of two tables.
   ```sql
   SELECT e.name, d.department_name 
   FROM employees e CROSS JOIN departments d;
   ```

---

### **2.4 Subqueries**

- **Multiple-Row Subquery**: Returns multiple rows.
   ```sql
   SELECT name FROM employees 
   WHERE department_id IN (SELECT department_id FROM departments WHERE location_id = 1700);
   ```

- **Correlated Subquery**: The subquery depends on values from the outer query.
   ```sql
   SELECT e.name 
   FROM employees e 
   WHERE salary > (SELECT AVG(salary) FROM employees WHERE department_id = e.department_id);
   ```

---

### **2.5 SQL Set Operators**

- **UNION**: Combines results from two queries and removes duplicates.
   ```sql
   SELECT name FROM employees 
   UNION 
   SELECT name FROM contractors;
   ```

- **UNION ALL**: Combines results and includes duplicates.
   ```sql
   SELECT name FROM employees 
   UNION ALL 
   SELECT name FROM contractors;
   ```

- **INTERSECT**: Returns only rows present in both queries.
   ```sql
   SELECT name FROM employees 
   INTERSECT 
   SELECT name FROM contractors;
   ```

- **MINUS**: Returns rows from the first query that are not in the second.
   ```sql
   SELECT name FROM employees 
   MINUS 
   SELECT name FROM contractors;
   ```

   ### **Unit III: Database Integrity Constraints & Objects Cheat Sheet (Oracle Syntax)**

---

### **3.1 Domain Integrity Constraints**
Ensure data entered in a column adheres to specific rules.

- **NOT NULL**: Ensures that a column cannot have `NULL` values.
  ```sql
  CREATE TABLE employees (
      emp_id NUMBER NOT NULL,
      emp_name VARCHAR2(50) NOT NULL
  );
  ```

- **CHECK**: Ensures that the data in a column meets a specified condition.
  ```sql
  CREATE TABLE employees (
      emp_id NUMBER,
      emp_age NUMBER CHECK (emp_age >= 18)
  );
  ```

---

### **3.2 Entity Integrity Constraints**
Ensure that each row in the table is unique and identifiable.

- **UNIQUE**: Ensures that all values in a column are unique.
  ```sql
  CREATE TABLE employees (
      emp_email VARCHAR2(100) UNIQUE
  );
  ```

- **PRIMARY KEY**: A combination of `NOT NULL` and `UNIQUE`. It ensures each row has a unique identifier.
  ```sql
  CREATE TABLE employees (
      emp_id NUMBER PRIMARY KEY
  );
  ```

---

### **3.3 Referential Integrity Constraints**
Ensure relationships between tables are maintained.

- **FOREIGN KEY**: Links a column in one table to the primary key in another.
  ```sql
  CREATE TABLE departments (
      dept_id NUMBER PRIMARY KEY
  );

  CREATE TABLE employees (
      emp_id NUMBER PRIMARY KEY,
      dept_id NUMBER,
      FOREIGN KEY (dept_id) REFERENCES departments(dept_id)
  );
  ```

- **ON DELETE CASCADE**: Automatically deletes rows in the child table when the corresponding row in the parent table is deleted.
  ```sql
  CREATE TABLE employees (
      emp_id NUMBER PRIMARY KEY,
      dept_id NUMBER,
      FOREIGN KEY (dept_id) REFERENCES departments(dept_id) ON DELETE CASCADE
  );
  ```

- **ON DELETE SET NULL**: Sets the foreign key column to `NULL` when the corresponding parent row is deleted.
  ```sql
  CREATE TABLE employees (
      emp_id NUMBER PRIMARY KEY,
      dept_id NUMBER,
      FOREIGN KEY (dept_id) REFERENCES departments(dept_id) ON DELETE SET NULL
  );
  ```

---

### **3.4 Views**
A virtual table based on a SELECT query.

- **CREATE VIEW**: Creates a new view.
  ```sql
  CREATE VIEW emp_view AS 
  SELECT emp_id, emp_name FROM employees;
  ```

- **ALTER VIEW**: Modifies an existing view.
  ```sql
  CREATE OR REPLACE VIEW emp_view AS 
  SELECT emp_id, emp_name, emp_salary FROM employees;
  ```

- **DROP VIEW**: Deletes an existing view.
  ```sql
  DROP VIEW emp_view;
  ```

---

### **3.5 Synonym**
An alias for a database object.

- **CREATE SYNONYM**: Creates a synonym for a table, view, or other database object.
  ```sql
  CREATE SYNONYM emp_syn FOR employees;
  ```

- **DROP SYNONYM**: Deletes an existing synonym.
  ```sql
  DROP SYNONYM emp_syn;
  ```

---

### **3.6 Sequences**
Generate unique numbers, often used for primary key values.

- **CREATE SEQUENCE**: Creates a new sequence.
  ```sql
  CREATE SEQUENCE emp_seq
  START WITH 1
  INCREMENT BY 1
  NOCACHE;
  ```

- **ALTER SEQUENCE**: Modifies an existing sequence.
  ```sql
  ALTER SEQUENCE emp_seq
  INCREMENT BY 10;
  ```

- **DROP SEQUENCE**: Deletes a sequence.
  ```sql
  DROP SEQUENCE emp_seq;
  ```

---

### **3.7 Index**
Improve the speed of data retrieval.

- **Unique Index**: Ensures that the indexed column contains unique values.
  ```sql
  CREATE UNIQUE INDEX emp_email_idx ON employees(emp_email);
  ```

- **Composite Index**: Creates an index on multiple columns.
  ```sql
  CREATE INDEX emp_comp_idx ON employees(emp_name, emp_age);
  ```

- **DROP Index**: Deletes an index.
  ```sql
  DROP INDEX emp_email_idx;
  ```

  ### **Unit IV: PL/SQL and Triggers Cheat Sheet (Oracle Syntax)**

---

### **4.1 Basics of PL/SQL**
PL/SQL (Procedural Language/Structured Query Language) is Oracle's procedural extension to SQL.

#### **4.1.1 Data Types**
- **Anchored Data Type (`%TYPE` and `%ROWTYPE`)**: Automatically defines a variable's data type based on the type of another variable or table column.
  - `%TYPE`: Anchors the variable to the data type of a column.
    ```sql
    DECLARE
      emp_name employees.emp_name%TYPE;
    BEGIN
      SELECT emp_name INTO emp_name FROM employees WHERE emp_id = 1;
    END;
    ```
  - `%ROWTYPE`: Anchors a variable to an entire row of a table or cursor.
    ```sql
    DECLARE
      emp_rec employees%ROWTYPE;
    BEGIN
      SELECT * INTO emp_rec FROM employees WHERE emp_id = 1;
    END;
    ```

---

### **4.2 Advantages of PL/SQL over SQL**
- **Procedural Language**: Combines procedural programming with SQL to handle complex business logic.
- **Modularity**: PL/SQL allows code to be organized into procedures, functions, packages, and triggers.
- **Error Handling**: Provides robust error handling through exception mechanisms.
- **Performance**: Reduces network traffic by bundling multiple SQL statements into a block of code.

---

### **4.3 Control Structures**

#### **1. Conditional Control**
- **IF-THEN-ELSE**: Executes a set of statements based on a condition.
  ```sql
  DECLARE
    salary NUMBER := 5000;
  BEGIN
    IF salary > 10000 THEN
      DBMS_OUTPUT.PUT_LINE('High Salary');
    ELSE
      DBMS_OUTPUT.PUT_LINE('Normal Salary');
    END IF;
  END;
  ```

#### **2. Iterative Control**
- **LOOP**: Repeats a block of statements until a condition is met.
  ```sql
  DECLARE
    i NUMBER := 1;
  BEGIN
    LOOP
      DBMS_OUTPUT.PUT_LINE('Count: ' || i);
      i := i + 1;
      EXIT WHEN i > 5;
    END LOOP;
  END;
  ```

- **FOR Loop**: Executes a loop a specified number of times.
  ```sql
  DECLARE
    i NUMBER;
  BEGIN
    FOR i IN 1..5 LOOP
      DBMS_OUTPUT.PUT_LINE('Count: ' || i);
    END LOOP;
  END;
  ```

#### **3. Sequential Control**
- PL/SQL executes statements sequentially by default, without any explicit control.

---

### **4.4 Exceptions**
Handle errors that occur during execution.

#### **1. Predefined Exceptions**
- **NO_DATA_FOUND**: Raised when a SELECT INTO statement returns no rows.
  ```sql
  BEGIN
    SELECT emp_name INTO name FROM employees WHERE emp_id = 1000;
  EXCEPTION
    WHEN NO_DATA_FOUND THEN
      DBMS_OUTPUT.PUT_LINE('No employee found.');
  END;
  ```

- **ZERO_DIVIDE**: Raised when there is a division by zero.
  ```sql
  BEGIN
    DECLARE
      x NUMBER := 10;
      y NUMBER := 0;
      result NUMBER;
    BEGIN
      result := x / y;
    EXCEPTION
      WHEN ZERO_DIVIDE THEN
        DBMS_OUTPUT.PUT_LINE('Division by zero is not allowed.');
    END;
  END;
  ```

#### **2. User-Defined Exceptions**
- Define and raise custom exceptions.
  ```sql
  DECLARE
    invalid_salary EXCEPTION;
    salary NUMBER := 500;
  BEGIN
    IF salary < 1000 THEN
      RAISE invalid_salary;
    END IF;
  EXCEPTION
    WHEN invalid_salary THEN
      DBMS_OUTPUT.PUT_LINE('Salary is too low.');
  END;
  ```

---

### **4.5 Cursors**
A cursor is a pointer to the result set of a query.

#### **1. Implicit Cursors**
- Automatically created for `SELECT INTO`, `INSERT`, `UPDATE`, or `DELETE` statements.
  ```sql
  BEGIN
    SELECT emp_name INTO name FROM employees WHERE emp_id = 1;
  END;
  ```

#### **2. Explicit Cursors**
- Defined and controlled by the programmer.
  ```sql
  DECLARE
    CURSOR emp_cursor IS SELECT emp_name FROM employees;
    emp_name employees.emp_name%TYPE;
  BEGIN
    OPEN emp_cursor;
    LOOP
      FETCH emp_cursor INTO emp_name;
      EXIT WHEN emp_cursor%NOTFOUND;
      DBMS_OUTPUT.PUT_LINE(emp_name);
    END LOOP;
    CLOSE emp_cursor;
  END;
  ```

#### **3. Dynamic Cursors**
- Cursors created dynamically using `OPEN FOR`.
  ```sql
  DECLARE
    TYPE ref_cursor IS REF CURSOR;
    my_cursor ref_cursor;
    emp_name employees.emp_name%TYPE;
  BEGIN
    OPEN my_cursor FOR 'SELECT emp_name FROM employees';
    LOOP
      FETCH my_cursor INTO emp_name;
      EXIT WHEN my_cursor%NOTFOUND;
      DBMS_OUTPUT.PUT_LINE(emp_name);
    END LOOP;
    CLOSE my_cursor;
  END;
  ```

---

### **4.6 Procedures & Functions**

#### **Procedure**: A subprogram that performs an action but does not return a value.
  ```sql
  CREATE OR REPLACE PROCEDURE update_salary (emp_id IN NUMBER, new_salary IN NUMBER) IS
  BEGIN
    UPDATE employees SET salary = new_salary WHERE employee_id = emp_id;
  END update_salary;
  ```

#### **Function**: A subprogram that returns a value.
  ```sql
  CREATE OR REPLACE FUNCTION get_salary (emp_id IN NUMBER) RETURN NUMBER IS
    salary employees.salary%TYPE;
  BEGIN
    SELECT salary INTO salary FROM employees WHERE employee_id = emp_id;
    RETURN salary;
  END get_salary;
  ```

---

### **4.7 Fundamentals of Database Triggers**
Triggers are stored PL/SQL blocks that automatically execute when a specified DML event occurs (like `INSERT`, `UPDATE`, `DELETE`).

---

### **4.8 Creating Triggers**

- **Basic Syntax** for creating a trigger:
  ```sql
  CREATE OR REPLACE TRIGGER emp_trigger
  BEFORE INSERT ON employees
  FOR EACH ROW
  BEGIN
    DBMS_OUTPUT.PUT_LINE('New employee added: ' || :NEW.emp_name);
  END;
  ```

---

### **4.9 Types of Triggers**

#### **1. BEFORE Trigger**
- Executes before a DML operation.
  ```sql
  CREATE OR REPLACE TRIGGER before_insert_trigger
  BEFORE INSERT ON employees
  FOR EACH ROW
  BEGIN
    :NEW.emp_name := UPPER(:NEW.emp_name);
  END;
  ```

#### **2. AFTER Trigger**
- Executes after a DML operation.
  ```sql
  CREATE OR REPLACE TRIGGER after_insert_trigger
  AFTER INSERT ON employees
  FOR EACH ROW
  BEGIN
    DBMS_OUTPUT.PUT_LINE('Employee ' || :NEW.emp_name || ' was added.');
  END;
  ```

#### **3. FOR EACH ROW**
- Trigger executes once for each row affected by the DML operation.
  ```sql
  CREATE OR REPLACE TRIGGER emp_row_trigger
  BEFORE UPDATE ON employees
  FOR EACH ROW
  BEGIN
    DBMS_OUTPUT.PUT_LINE('Old salary: ' || :OLD.salary || ', New salary: ' || :NEW.salary);
  END;
  ```

#### **4. FOR EACH STATEMENT**
- Trigger executes once per DML statement.
  ```sql
  CREATE OR REPLACE TRIGGER emp_stmt_trigger
  AFTER DELETE ON employees
  BEGIN
    DBMS_OUTPUT.PUT_LINE('Employee data deleted.');
  END;
  ```

  ### **Unit V: Normalization Cheat Sheet**

---

### **5.1 Basics of Normalization**
Normalization is the process of organizing data in a database to minimize redundancy and ensure data integrity. It involves dividing a database into tables and defining relationships between the tables.

- **Goal**: Reduce data redundancy, eliminate anomalies (insertion, update, and deletion), and ensure data consistency.
  
---

### **5.2 Normal Forms**
There are several stages of normalization, each with stricter rules. Common normal forms include 1NF, 2NF, and 3NF.

#### **5.2.1 First Normal Form (1NF)**
A table is in **1NF** if:
- All columns contain **atomic** values (no multi-valued or composite attributes).
- Each entry in a column contains only one value, and there are no repeating groups.

**Example (Non-1NF Table)**:
| Student_ID | Student_Name | Subjects        |
|------------|--------------|-----------------|
| 1          | Ramesh       | Math, Physics   |
| 2          | Sita         | Math, Chemistry |

**1NF Table** (each subject is split into a new row):
| Student_ID | Student_Name | Subject   |
|------------|--------------|-----------|
| 1          | Ramesh       | Math      |
| 1          | Ramesh       | Physics   |
| 2          | Sita         | Math      |
| 2          | Sita         | Chemistry |

---

#### **5.2.2 Second Normal Form (2NF)**
A table is in **2NF** if:
- It is in **1NF**, and
- **All non-key attributes are fully functionally dependent** on the entire primary key (no partial dependency).

**Example (Non-2NF Table)**:
| Student_ID | Subject  | Teacher   |
|------------|----------|-----------|
| 1          | Math     | Mr. A     |
| 1          | Physics  | Mr. B     |
| 2          | Math     | Mr. A     |

In the table above, "Teacher" depends only on "Subject" and not on the full primary key (Student_ID, Subject).

**2NF Table** (separated into two tables):
1. **Students**:
   | Student_ID | Subject   |
   |------------|-----------|
   | 1          | Math      |
   | 1          | Physics   |
   | 2          | Math      |

2. **Subjects**:
   | Subject   | Teacher   |
   |-----------|-----------|
   | Math      | Mr. A     |
   | Physics   | Mr. B     |

---

#### **5.2.3 Third Normal Form (3NF)**
A table is in **3NF** if:
- It is in **2NF**, and
- There is **no transitive dependency** (non-key columns do not depend on other non-key columns).

**Example (Non-3NF Table)**:
| Student_ID | Subject  | Teacher   | Department   |
|------------|----------|-----------|--------------|
| 1          | Math     | Mr. A     | Science      |
| 2          | Physics  | Mr. B     | Science      |

Here, "Department" depends on "Teacher" (which is not a key), so this is not in 3NF.

**3NF Table** (separated into two tables):
1. **Students**:
   | Student_ID | Subject   |
   |------------|-----------|
   | 1          | Math      |
   | 2          | Physics   |

2. **Teachers**:
   | Teacher   | Department  |
   |-----------|-------------|
   | Mr. A     | Science     |
   | Mr. B     | Science     |

---

### **5.3 Advantages and Disadvantages of Normalization**

#### **Advantages:**
1. **Data Integrity**: Ensures consistency and reduces data redundancy.
2. **Eliminates Anomalies**: Helps avoid insertion, update, and deletion anomalies.
3. **Better Organization**: Data is structured logically, making it easier to maintain.
4. **Efficient Use of Storage**: Reduces the amount of duplicated data, saving space.

#### **Disadvantages:**
1. **Complex Queries**: Highly normalized data often requires complex JOIN queries, which may reduce performance.
2. **More Tables**: Data is split into multiple tables, which can increase complexity in database management.
3. **Slower Operations**: Retrieval operations may become slower due to the need to join many tables.
