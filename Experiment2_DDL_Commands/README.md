# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1:
```
Insert all products from Discontinued_products into Products.

Table attributes are ProductID, ProductName, Price, Stock
PROGRAM:
INSERT INTO Products select * from  Discontinued_products;
```


**Output:

<img width="1051" height="265" alt="image" src="https://github.com/user-attachments/assets/22a26774-a7f1-4790-ac2f-c7fd655dfdf7" />


**Question 2**
```
Insert a record with EmployeeID 001, Name Sarah Parker, Position Manager, Department HR, and Salary 60000 into the Employee table.

PROGRAM:

INSERT INTO Employee(EmployeeID,Name,Position,Department,Salary) VALUES(1,'Sarah Parker','Manager','HR','60000');

```

**Output:

<img width="1305" height="256" alt="image" src="https://github.com/user-attachments/assets/febf23c6-c930-4dba-8c95-4271b4a7cab7" />


**Question 3**
```
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should cascade updates and deletes.
item_desc and rate should not accept NULL.

PROGRAM:

CREATE TABLE item(
item_id TEXT primary keY,
item_desc TEXT NOT NULL,
rate INTEGER,
icom_id TEXT(4), 
FOREIGN KEY(icom_id) references company(com_id) ON UPDATE CASCADE ON DELETE CASCADE
);

```

**Output:
<img width="1292" height="337" alt="image" src="https://github.com/user-attachments/assets/25204e92-56a3-44f2-aecb-b5e1e5770e13" />


**Question 4**
```
Write a SQL Query  to Rename attribute "name" to "first_name"  and add mobilenumber as number ,DOB as Date,State as varchar(30) in the table Companies. 

PROGRAM:
ALTER TABLE Companies RENAME COLUMN name TO first_name;
ALTER TABLE Companies ADD COLUMN mobilenumber number;
ALTER TABLE Companies ADD COLUMN DOB Date; 
ALTER TABLE Companies ADD COLUMN State varchar(30);

```

**Output:
<img width="1295" height="375" alt="image" src="https://github.com/user-attachments/assets/3d36bce7-31e1-4994-8851-39d33b042054" />

**Question 5**
```
Insert all customers from Old_customers into Customers

Table attributes are CustomerID, Name, Address, Email

PROGRAM:

Insert into Customers select * from Old_customers;
```

**Output:**
<img width="1286" height="273" alt="image" src="https://github.com/user-attachments/assets/642f52f5-f534-4ec9-b9fa-05fd50e79dec" />





**Question 6**
```
In the Products table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

ProductID   Name              Category    Price       Stock
----------  ---------------   ----------  ----------  ----------
106         Fitness Tracker   Wearables
107         Laptop            Electronics  999.99      50
108         Wireless Earbuds  Accessories              100
 

PROGRAM:
INSERT INTO Products(ProductID,Name,Category,Price,Stock) values(106,'Fitness Tracker','Wearables',NULL,NULl),(107,'Laptop','Electronic',999.99,50),
(108,'Wireless Earbud','Accessorie',Null,100);

```

**Output:**

![Output6](output.png)

**Question 7**
```
Create a table named Invoices with the following constraints:

InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
DueDate as DATE should be greater than the InvoiceDate.
Amount as REAL should be greater than 0.
PROGRAM:
Create table Invoices(
InvoiceID INTEGER primary key,
InvoiceDate DATE,
DueDate DATE Check(DueDate>InvoiceDate),
Amount REAL check(Amount>0));

```

**Output:**
<img width="1272" height="298" alt="image" src="https://github.com/user-attachments/assets/b2bd6115-d8f1-4a6b-a7af-993d27def4a8" />




**Question 8**
```
Create a table named Products with the following constraints:

ProductID should be the primary key.
ProductName should be NOT NULL.
Price is of real datatype and should be greater than 0.
Stock is of integer datatype and should be greater than or equal to 0.

PROGRAM:
Create table Products(
ProductID INT primary key,
ProductName TEXT NOT NULL,
Price real CHECK(Price>0),
Stock integer Check(Stock>=0));
```

**Output:**

<img width="1178" height="208" alt="image" src="https://github.com/user-attachments/assets/9e007680-87e1-4050-b74a-961095c256cb" />


**Question 9**

```
Insert a new product with ProductID 101, Name Laptop, Category Electronics, Price 1500, and Stock 50 into the Products table.

PROGRAM:
INSERT INTO PRODUCTS(ProductID,Name,Category,Price,Stock) VALUES(101,'Laptop','Electronics',1500,50);
```

**Output:**
<img width="1240" height="173" alt="image" src="https://github.com/user-attachments/assets/d4e0608a-120d-4b61-ba06-959fb562309d" />



**Question 10**

```
Write a SQL Query  to change the name of attribute "name" to "first_name"  and add mobilenumber as number ,DOB as Date in the table Companies. 

PROGRAM:
ALTER TABLE Companies rename column name to first_name;
ALTER TABLE Companies ADD mobilenumber number;
ALTER TABLE Companies ADD DOB Date;
```
**Output:**

<img width="1267" height="297" alt="image" src="https://github.com/user-attachments/assets/f5dc3c3f-9bd6-4fe6-b607-489cf55385ca" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
