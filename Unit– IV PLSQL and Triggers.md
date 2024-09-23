
### **Unit IV: PL/SQL and Triggers - Detailed Notes**

---

### **4.1 Basics of PL/SQL**

PL/SQL (Procedural Language/Structured Query Language) is a block-structured language that enhances SQL by adding procedural features. It allows embedding SQL statements in programming constructs like loops, conditions, exceptions, etc. PL/SQL is tightly integrated with SQL and provides powerful capabilities to interact with Oracle databases.

#### **PL/SQL Block Structure**
A PL/SQL program is organized into blocks, each having three parts:
1. **Declaration Section**: Where variables, cursors, constants, and exceptions are defined.
2. **Execution Section**: The core logic, containing SQL and PL/SQL statements.
3. **Exception Handling Section**: Handles runtime errors.

Example:
```sql
DECLARE
  emp_name employees.emp_name%TYPE;
BEGIN
  SELECT emp_name INTO emp_name FROM employees WHERE emp_id = 1;
  DBMS_OUTPUT.PUT_LINE('Employee Name: ' || emp_name);
EXCEPTION
  WHEN NO_DATA_FOUND THEN
    DBMS_OUTPUT.PUT_LINE('No employee found.');
END;
```

---

### **4.1.1 Data Types:**

PL/SQL supports a wide range of data types for handling different kinds of data. These data types can be grouped into several categories.
#### **1. Scalar Data Types**

Scalar data types store a single value and do not contain internal components. These include:

#### **a. Numeric Data Types**
Used for storing numeric values.
- **NUMBER**: Stores fixed and floating-point numbers.
#### **b. Character Data Types**
Used for storing text strings.
- **CHAR**: Fixed-length character data.
- **VARCHAR2**: Variable-length character data.

#### **c. Date and Time Data Types**
Used for storing date and time information.
- **DATE**: Stores date and time down to seconds.
- **TIMESTAMP**: Stores date and time with fractional seconds.
#### **d. Anchored Data Types** 
use the `%TYPE` and `%ROWTYPE` attributes to define variables that inherit the data type of a column or row, ensuring compatibility with database schema changes.
  - **`%TYPE`**: Anchors the variable to the data type of a specific column.
  - **`%ROWTYPE`**: Anchors a variable to the row type of a table or cursor.

Example:
```sql
DECLARE
  emp_name employees.emp_name%TYPE;  -- Anchors to the emp_name column in employees table
  emp_rec employees%ROWTYPE;          -- Anchors to the structure of the entire row
BEGIN
  SELECT * INTO emp_rec FROM employees WHERE emp_id = 101;
  DBMS_OUTPUT.PUT_LINE(emp_rec.emp_name);
END;
```

---

### **4.2 Advantages of PL/SQL over SQL**

1. **Procedural Logic**: PL/SQL allows the use of control structures (loops, conditionals), making it more powerful than SQL for complex operations.
2. **Better Performance**: Reduces network traffic by bundling multiple SQL statements into a single block that can be executed at once.
3. **Modularity**: Supports procedures, functions, and packages, enabling code reuse and better organization.
4. **Error Handling**: Provides robust exception handling mechanisms that help deal with runtime errors and manage database transactions safely.
5. **Portability**: PL/SQL code can run on any Oracle database, making it portable.

---

### **4.3 Control Structures**

PL/SQL offers three types of control structures for decision-making and looping:

#### **1. Conditional Control**
- **IF-THEN-ELSE**: Executes code based on a condition.
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
- **LOOP**: A basic loop that runs until an `EXIT` condition is met.
  ```sql
  DECLARE
    counter NUMBER := 1;
  BEGIN
    LOOP
      DBMS_OUTPUT.PUT_LINE('Iteration: ' || counter);
      counter := counter + 1;
      EXIT WHEN counter > 5;
    END LOOP;
  END;
  ```

- **FOR Loop**: Iterates a specific number of times.
  ```sql
  BEGIN
    FOR i IN 1..5 LOOP
      DBMS_OUTPUT.PUT_LINE('Value: ' || i);
    END LOOP;
  END;
  ```

#### **3. Sequential Control**
The **`GOTO` statement** in PL/SQL allows unconditional branching to a specific label within a block of code. It is rarely used because it can make the code harder to read and maintain, but it provides a way to jump directly to a labeled part of the program.

#### **Syntax**
```sql
<<label_name>>
BEGIN
  -- Some code
  GOTO label_name;  -- Jumps to the specified label
  -- Code that will be skipped
  <<label_name>>
  -- Code that is executed after the jump
END;
```

#### **Key Points:**
1. The **`GOTO` statement** transfers control to a labeled section of code.
2. The target label must be within the same block, and the label should be enclosed in double angle brackets `<< >>`.
3. Avoid overusing `GOTO`, as it can make the program flow difficult to follow.

#### **Example**
```sql
DECLARE
  counter NUMBER := 1;
BEGIN
  <<start_loop>>
  IF counter <= 5 THEN
    DBMS_OUTPUT.PUT_LINE('Counter: ' || counter);
    counter := counter + 1;
    GOTO start_loop;  -- Jumps back to the labeled part
  END IF;
END;
```

### **4.4 Exceptions**

Exceptions in PL/SQL handle runtime errors, preventing the program from crashing and allowing it to handle errors gracefully.

#### **1. Predefined Exceptions**
- **NO_DATA_FOUND**: Triggered when a SELECT INTO query returns no rows.
- **ZERO_DIVIDE**: Raised when a division by zero occurs.

Example:
```sql
BEGIN
  SELECT emp_name INTO emp_name FROM employees WHERE emp_id = 1000;
EXCEPTION
  WHEN NO_DATA_FOUND THEN
    DBMS_OUTPUT.PUT_LINE('No employee found.');
END;
```

#### **2. User-Defined Exceptions**
Programmers can define custom exceptions for specific conditions.

Example:
```sql
DECLARE
  low_salary EXCEPTION;
  salary NUMBER := 500;
BEGIN
  IF salary < 1000 THEN
    RAISE low_salary;
  END IF;
EXCEPTION
  WHEN low_salary THEN
    DBMS_OUTPUT.PUT_LINE('Salary is too low.');
END;
```

---

### **4.5 Cursors**

Cursors are used to process query result sets one row at a time.

#### **1. Implicit Cursors**
Automatically created by Oracle for single-row queries.

Example:
```sql
BEGIN
  SELECT emp_name INTO name FROM employees WHERE emp_id = 1;
END;
```

#### **2. Explicit Cursors**
Defined explicitly for handling queries returning multiple rows.

Example:
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
Allow the cursor to be dynamically opened with a SQL string.

Example:
```sql
DECLARE
  TYPE ref_cursor IS REF CURSOR;
  my_cursor ref_cursor;
  emp_name employees.emp_name%TYPE;
BEGIN
  OPEN my_cursor FOR 'SELECT emp_name FROM employees';
  FETCH my_cursor INTO emp_name;
  CLOSE my_cursor;
END;
```

---

### **4.6 Procedures & Functions**

- **Procedure**: A subprogram that performs an action but does not return a value.
  ```sql
  CREATE OR REPLACE PROCEDURE update_salary (emp_id IN NUMBER, new_salary IN NUMBER) IS
  BEGIN
    UPDATE employees SET salary = new_salary WHERE employee_id = emp_id;
  END;
  ```

- **Function**: A subprogram that returns a value.
  ```sql
  CREATE OR REPLACE FUNCTION get_salary (emp_id IN NUMBER) RETURN NUMBER IS
    salary employees.salary%TYPE;
  BEGIN
    SELECT salary INTO salary FROM employees WHERE employee_id = emp_id;
    RETURN salary;
  END;
  ```

---

### **4.7 Fundamentals of Database Triggers**

A trigger is a stored PL/SQL block that automatically executes in response to a specific event (e.g., `INSERT`, `UPDATE`, `DELETE`) on a table or view.

Triggers can be used to:
1. Enforce complex business rules.
2. Automatically log changes to the database.
3. Perform actions based on database events.

---

### **4.8 Creating Triggers**

Basic syntax to create a trigger:
```sql
CREATE OR REPLACE TRIGGER trigger_name
BEFORE INSERT OR UPDATE ON employees
FOR EACH ROW
BEGIN
  -- Trigger body here
END;
```

Example:
```sql
CREATE OR REPLACE TRIGGER emp_salary_trigger
BEFORE UPDATE OF salary ON employees
FOR EACH ROW
BEGIN
  IF :NEW.salary < :OLD.salary THEN
    RAISE_APPLICATION_ERROR(-20001, 'Salary cannot be decreased.');
  END IF;
END;
```

---

### **4.9 Types of Triggers**

#### **1. BEFORE Trigger**
Executes before the DML operation.

Example:
```sql
CREATE OR REPLACE TRIGGER before_insert_trigger
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
  :NEW.salary := :NEW.salary + 1000;  -- Adjusts salary before insert
END;
```

#### **2. AFTER Trigger**
Executes after the DML operation.

Example:
```sql
CREATE OR REPLACE TRIGGER after_update_trigger
AFTER UPDATE ON employees
FOR EACH ROW
BEGIN
  DBMS_OUTPUT.PUT_LINE('Employee salary updated.');
END;
```

#### **3. FOR EACH ROW**
Executes once for each row affected by the DML statement.

Example:
```sql
CREATE OR REPLACE TRIGGER row_trigger
BEFORE UPDATE ON employees
FOR EACH ROW
BEGIN
  DBMS_OUTPUT.PUT_LINE('Updated Employee: ' || :NEW.emp_name);
END;
```

#### **4. FOR EACH STATEMENT**
Executes once per DML statement, regardless of how many rows are affected.

Example:
```sql
CREATE OR REPLACE TRIGGER stmt_trigger
AFTER DELETE ON employees
BEGIN
  DBMS_OUTPUT.PUT_LINE('Employee data deleted.');
END;
```
