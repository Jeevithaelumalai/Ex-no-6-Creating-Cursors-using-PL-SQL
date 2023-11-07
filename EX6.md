# Ex. No: 6 Creating Cursors using PL/SQL
## DATE:7/9/2023
### AIM: To create a cursor using PL/SQL.

### Steps:
1. Create employee table with following attributes (empid NUMBER, empname VARCHAR(10), dept VARCHAR(10),salary NUMBER);
2. Create a cursor named as employee_cursor
3. Using cursor read each record and display the result
4. Close the cursor

### Program:
### Create employee table
```
 empname VARCHAR(10),' at line 1
mysql> CREATE TABLE employee (
    ->   empid INT,
    ->   empname VARCHAR(10),
    ->   dept VARCHAR(10),
    ->   salary DECIMAL(10, 2)
    -> );
INSERT INTO employee VALUES (1, 'Jeevitha', 'Sales', 100000);
INSERT INTO employee VALUES (1, 'priya', 'marketing', 120000);
```

### PLSQL Cursor code
```
DELIMITER //

CREATE PROCEDURE fetch_employee_data()
BEGIN
  DECLARE v_empid INT;
  DECLARE v_empname VARCHAR(10);
  DECLARE v_dept VARCHAR(10);
  DECLARE v_salary DECIMAL(10, 2);
  
  DECLARE emp_cursor CURSOR FOR
    SELECT empid, empname, dept, salary
    FROM employee;
  
  DECLARE CONTINUE HANDLER FOR NOT FOUND SET @finished = 1;
  

  OPEN emp_cursor;
  

  SET @finished = 0;
  
  FETCH_NEXT: LOOP
    FETCH emp_cursor INTO v_empid, v_empname, v_dept, v_salary;
    IF @finished = 1 THEN
      LEAVE FETCH_NEXT; -- Exit the loop when no more rows
    END IF;

    SELECT v_empid, v_empname, v_dept, v_salary;
  END LOOP FETCH_NEXT;
  
 
  CLOSE emp_cursor;
END //

DELIMITER ;

CALL fetch_employee_data();
```
### Output:
![image](https://github.com/Jeevithaelumalai/Ex-no-6-Creating-Cursors-using-PL-SQL/assets/118708245/5cadc86a-22ef-443f-941a-2cec3837af5b)


### Result:
THE PROGRAM HAS BEEN IMPLEMENTED SUCCESSFULLY.
