# Experiment 9: PL/SQL – Procedures and Functions

## AIM
To understand and implement procedures and functions in PL/SQL for performing various operations such as calculations, decision-making, and looping.

---

## THEORY

PL/SQL (Procedural Language/SQL) extends SQL by adding procedural constructs like variables, conditions, loops, procedures, and functions. Procedures and functions are subprograms that help modularize the code and improve reusability.

### **Procedure**
A PL/SQL **procedure** is a subprogram that performs a specific action. It does not return a value directly but can return values using `OUT` parameters.

**Syntax:**
```sql
CREATE OR REPLACE PROCEDURE procedure_name (parameters)
IS
BEGIN
   -- statements
END;
```

To call the procedure

```sql
EXEC procedure_name(arguments);
```

### **Function**
A PL/SQL **function** is a subprogram that returns a single value using the RETURN keyword.

```sql
CREATE OR REPLACE FUNCTION function_name (parameters)
RETURN datatype
IS
BEGIN
   -- statements
   RETURN value;
END;
```

To call the function:

```sql
SELECT function_name(arguments) FROM DUAL;
```

Key Differences:

-A procedure does not return a value, whereas a function must return a value.
-Functions can be called from SQL queries, procedures cannot (in most cases).

## 1. Write a PL/SQL Procedure to Find the Square of a Number

### Steps:
- Create a procedure named `find_square`.
- Declare a parameter to accept a number.
- Inside the procedure, compute the square of the input number.
- Use `DBMS_OUTPUT.PUT_LINE` to display the result.
- Call the procedure with a number as input.

**Expected Output:**  
Square of 6 is 36

PROGRAM:
SET SERVEROUTPUT ON;

CREATE OR REPLACE PROCEDURE find_square(n NUMBER)
IS
    square_num NUMBER;
BEGIN
    square_num := n * n;
    DBMS_OUTPUT.PUT_LINE('Square of ' || n || ' is ' || square_num);
END;
/

BEGIN
    find_square(6);
END;
/

OUTPUT:
<img width="367" height="207" alt="image" src="https://github.com/user-attachments/assets/0d6548c8-f365-4a34-8627-498f52349349" />
<img width="415" height="145" alt="image" src="https://github.com/user-attachments/assets/e7f6c6ee-e6e3-4d5c-ae03-0e4c88b759cc" />


---

## 2. Write a PL/SQL Function to Return the Factorial of a Number

### Steps:
- Create a function named `get_factorial`.
- Declare a parameter to accept a number.
- Use a loop to calculate the factorial.
- Return the result using the `RETURN` statement.
- Call the function using a `SELECT` statement or in an anonymous block.

**Expected Output:**  
Factorial of 5 is 120
PROGRAM:

SET SERVEROUTPUT ON;

CREATE OR REPLACE FUNCTION get_factorial(n NUMBER)
RETURN NUMBER
IS
    fact NUMBER := 1;
BEGIN
    FOR i IN 1..n LOOP
        fact := fact * i;
    END LOOP;

    RETURN fact;
END;
/
BEGIN
    DBMS_OUTPUT.PUT_LINE('Factorial of 5 is ' || get_factorial(5));
END;
/
BEGIN
    DBMS_OUTPUT.PUT_LINE('Factorial of 5 is ' || get_factorial(5));
END;
/
---

OUTPUT:
<img width="350" height="115" alt="image" src="https://github.com/user-attachments/assets/fc478550-5344-42bb-9157-b9f21046ae1f" />
<img width="368" height="137" alt="image" src="https://github.com/user-attachments/assets/acbff955-9f29-42d5-b2be-e12c5b7c4d9e" />



## 3. Write a PL/SQL Procedure to Check Whether a Number is Even or Odd

### Steps:
- Create a procedure named `check_even_odd`.
- Accept an input parameter.
- Use the `MOD` function to check if the number is divisible by 2.
- Display whether it is Even or Odd using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
12 is Even
PROGRAM:
SET SERVEROUTPUT ON;

CREATE OR REPLACE PROCEDURE check_even_odd(n NUMBER)
IS
BEGIN
    IF MOD(n, 2) = 0 THEN
        DBMS_OUTPUT.PUT_LINE(n || ' is Even');
    ELSE
        DBMS_OUTPUT.PUT_LINE(n || ' is Odd');
    END IF;
END;
/
BEGIN
    check_even_odd(12);
END;
/
OUTPUT:
<img width="386" height="138" alt="image" src="https://github.com/user-attachments/assets/6978544f-1e80-47cd-9ec8-caad4c36ade4" />

---

## 4. Write a PL/SQL Function to Return the Reverse of a Number

### Steps:
- Create a function named `reverse_number`.
- Accept an input number as parameter.
- Use a loop to reverse the digits of the number.
- Return the reversed number.
- Call the function and display the output.

**Expected Output:**  
Reversed number of 1234 is 4321
PROGRAM:
SET SERVEROUTPUT ON;

CREATE OR REPLACE FUNCTION reverse_number(n NUMBER)
RETURN NUMBER
IS
    rev NUMBER := 0;
    rem NUMBER;
    num NUMBER := n;
BEGIN
    WHILE num > 0 LOOP
        rem := MOD(num, 10);
        rev := rev * 10 + rem;
        num := TRUNC(num / 10);
    END LOOP;

    RETURN rev;
END;
/
BEGIN
    DBMS_OUTPUT.PUT_LINE('Reversed number of 1234 is ' || reverse_number(1234));
END;
/

---
OUTPUT:
<img width="383" height="147" alt="image" src="https://github.com/user-attachments/assets/468d3c77-923d-4e48-84d1-4e075caf111e" />


## 5. Write a PL/SQL Procedure to Display the Multiplication Table of a Number

### Steps:
- Create a procedure named `print_table`.
- Accept an input number.
- Use a loop from 1 to 10 to multiply the input number.
- Display the multiplication results using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
Multiplication table of 5:  
5 x 1 = 5  
5 x 2 = 10  
5 x 3 = 15  
...  
5 x 10 = 50
PROGRAM:
SET SERVEROUTPUT ON;

CREATE OR REPLACE PROCEDURE print_table(n NUMBER)
IS
BEGIN
    FOR i IN 1..10 LOOP
        DBMS_OUTPUT.PUT_LINE(n || ' x ' || i || ' = ' || (n * i));
    END LOOP;
END;
/
BEGIN
    DBMS_OUTPUT.PUT_LINE('Multiplication table of 5:');
    print_table(5);
END;
/
---
OUTPUT:
<img width="376" height="265" alt="image" src="https://github.com/user-attachments/assets/1458504c-d879-42a5-9100-055181162f45" />


## RESULT
Thus, the PL/SQL programs using procedures and functions were written, compiled, and executed successfully.
