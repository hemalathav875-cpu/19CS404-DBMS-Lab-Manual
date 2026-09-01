# Experiment 10: PL/SQL – Triggers

## AIM
To write and execute PL/SQL trigger programs for automating actions in response to specific table events like INSERT, UPDATE, or DELETE.

---

## THEORY

A **trigger** is a stored PL/SQL block that is automatically executed or fired when a specified event occurs on a table or view. Triggers can be used for enforcing business rules, auditing changes, or automatic updates.

### Types of Triggers:
- **Before Trigger**: Executes before the operation (INSERT, UPDATE, DELETE).
- **After Trigger**: Executes after the operation.
- **Row-level Trigger**: Executes for each affected row.
- **Statement-level Trigger**: Executes once for the triggering statement.

**Basic Syntax:**
```sql
CREATE OR REPLACE TRIGGER trigger_name
BEFORE|AFTER INSERT|UPDATE|DELETE ON table_name
[FOR EACH ROW]
BEGIN
   -- trigger logic
END;
```

## 1. Write a trigger to log every insertion into a table.
**Steps:**
- Create two tables: `employees` (for storing data) and `employee_log` (for logging the inserts).
- Write an **AFTER INSERT** trigger on the `employees` table to log the new data into the `employee_log` table.

**Expected Output:**
- A new entry is added to the `employee_log` table each time a new record is inserted into the `employees` table.

PROGRAM:
```
1. Create employees table
CREATE TABLE employees (
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    salary NUMBER
);
2. Create employee_log table
CREATE TABLE employee_log (
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    salary NUMBER,
    log_date DATE
);
3. Create AFTER INSERT Trigger
CREATE OR REPLACE TRIGGER emp_insert_log
AFTER INSERT ON employees
FOR EACH ROW
BEGIN
    INSERT INTO employee_log
    VALUES (:NEW.emp_id, :NEW.emp_name, :NEW.salary, SYSDATE);
END;
/
4. Insert a record
INSERT INTO employees
VALUES (101, 'Ravi', 25000);

COMMIT;
5. Check the Log
SELECT * FROM employee_log;
```
OUTPUT:
<img width="907" height="142" alt="image" src="https://github.com/user-attachments/assets/8881cda0-dd95-4a9e-8cb7-9a4689dcef11" />

---

## 2. Write a trigger to prevent deletion of records from a sensitive table.
**Steps:**
- Write a **BEFORE DELETE** trigger on the `sensitive_data` table.
- Use `RAISE_APPLICATION_ERROR` to prevent deletion and issue a custom error message.

**Expected Output:**
- If an attempt is made to delete a record from `sensitive_data`, an error message is raised, e.g., `ERROR: Deletion not allowed on this table.`

PROGGRAM:
```
1. Create sensitive_data Table
CREATE TABLE sensitive_data (
    id NUMBER,
    data VARCHAR2(100)
);
2. Insert Sample Data
INSERT INTO sensitive_data
VALUES (1, 'Confidential Information');

COMMIT;
3. Create BEFORE DELETE Trigger
CREATE OR REPLACE TRIGGER prevent_delete
BEFORE DELETE ON sensitive_data
FOR EACH ROW
BEGIN
    RAISE_APPLICATION_ERROR(
        -20001,
        'Deletion not allowed on this table.'
    );
END;
/
4. Try to Delete a Record
DELETE FROM sensitive_data
WHERE id = 1;
```
OUTPUT:
<img width="676" height="238" alt="image" src="https://github.com/user-attachments/assets/96667678-16ee-43eb-9912-90fe10c53249" />


---

## 3. Write a trigger to automatically update a `last_modified` timestamp.
**Steps:**
- Add a `last_modified` column to the `products` table.
- Write a **BEFORE UPDATE** trigger on the `products` table to set the `last_modified` column to the current timestamp whenever an update occurs.

**Expected Output:**
- The `last_modified` column in the `products` table is updated automatically to the current date and time when any record is updated.

  PROGRAM:
```
  Step 1: Create products Table
CREATE TABLE products (
    product_id NUMBER,
    product_name VARCHAR2(50),
    price NUMBER,
    last_modified TIMESTAMP
);
Step 2: Insert Sample Record
INSERT INTO products
VALUES (101, 'Laptop', 50000, SYSTIMESTAMP);

COMMIT;
Step 3: Create BEFORE UPDATE Trigger
CREATE OR REPLACE TRIGGER update_last_modified
BEFORE UPDATE ON products
FOR EACH ROW
BEGIN
    :NEW.last_modified := SYSTIMESTAMP;
END;
/
Step 4: Update a Record
UPDATE products
SET price = 55000
WHERE product_id = 101;

COMMIT;
Step 5: Check the Updated Record
SELECT * FROM products;
```
OUTPUT:
<img width="906" height="132" alt="image" src="https://github.com/user-attachments/assets/9745e031-ac17-4b97-b280-fefff9dfe188" />


---

## 4. Write a trigger to keep track of the number of updates made to a table.
**Steps:**
- Create an `audit_log` table with a counter column.
- Write an **AFTER UPDATE** trigger on the `customer_orders` table to increment the counter in the `audit_log` table every time a record is updated.

**Expected Output:**
- The `audit_log` table will maintain a count of how many updates have been made to the `customer_orders` table.
PROGRAM:
```sql
CREATE TABLE customer_orders (
    order_id NUMBER,
    customer_name VARCHAR2(50),
    amount NUMBER
);

CREATE TABLE audit_log (
    update_count NUMBER
);

INSERT INTO audit_log VALUES (0);
COMMIT;

CREATE OR REPLACE TRIGGER count_updates
AFTER UPDATE ON customer_orders
BEGIN
    UPDATE audit_log
    SET update_count = update_count + 1;
END;
/

INSERT INTO customer_orders
VALUES (101, 'Ravi', 5000);

COMMIT;

UPDATE customer_orders
SET amount = 6000
WHERE order_id = 101;

COMMIT;

SELECT * FROM audit_log;
```
OUTPUT:
<img width="348" height="140" alt="image" src="https://github.com/user-attachments/assets/87c4138f-8dc5-4594-abd8-6bf09f171e83" />


---

## 5. Write a trigger that checks a condition before allowing insertion into a table.
**Steps:**
- Write a **BEFORE INSERT** trigger on the `employees` table to check if the inserted salary meets a specific condition (e.g., salary must be greater than 3000).
- If the condition is not met, raise an error to prevent the insert.

**Expected Output:**
- If the inserted salary in the `employees` table is below the condition (e.g., salary < 3000), the insert operation is blocked, and an error message is raised, such as: `ERROR: Salary below minimum threshold.`

PROGRAM:
```
CREATE OR REPLACE TRIGGER check_salary
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
    IF :NEW.salary < 3000 THEN
        RAISE_APPLICATION_ERROR(
            -20001,
            'Salary below minimum threshold.'
        );
    END IF;
END;
/

INSERT INTO employees
VALUES (102, 'Kumar', 2500);

COMMIT;
```
OUTPUT:
<img width="646" height="311" alt="image" src="https://github.com/user-attachments/assets/4716efe4-1b87-4877-8ff9-03cf4e0e473b" />


## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.
