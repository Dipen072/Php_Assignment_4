# 1 INTRODUCTION TO SQL



## LAB EXECRISES :





Lab 1: Create a new database named school\_db and a table called students with the following columns: student\_id, student\_name, age, class, and address.



CREATE DATABASE school\_db;



CREATE TABLE students (

    student\_id INT PRIMARY KEY,

    student\_name VARCHAR(100),

    age Big INT,

    class VARCHAR(50),

    address VARCHAR(255)

);





Lab 2: Insert 5 Records and Retrieve All



INSERT INTO students (student\_id, student\_name, age, class, address) VALUES

(1, 'Alice Johnson', 14, '8A', '123 Maple St'),

(2, 'Bob Smith', 15, '9B', '456 Oak Ave'),

(3, 'Charlie Lee', 13, '7C', '789 Pine Rd'),

(4, 'Diana Prince', 14, '8A', '321 Elm St'),

(5, 'Ethan Hunt', 15, '9B', '654 Cedar Blvd');



-- Retrieve all records

SELECT \* FROM students;





# 2 SQL SYNTAX

LAB EXECRISES :





Lab 1: Write SQL queries to retrieve specific columns (student\_name and age) from the students table.



SELECT student\_name, age

FROM students;



Lab 2: Write SQL queries to retrieve all students whose age is greater than 10.



SELECT \*

FROM students

WHERE age > 10;







# 3 SQL CONSTRAINT



LAB EXCRISES:





Lab 1: Create a table teachers with the following columns: teacher\_id (Primary Key), teacher\_name (NOT NULL), subject (NOT NULL), and email (UNIQUE).



CREATE TABLE teachers (

    teacher\_id INT PRIMARY KEY AUTO\_INCREMENT,

    teacher\_name VARCHAR(100) NOT NULL,

    subject VARCHAR(100) NOT NULL,

    email VARCHAR(100) UNIQUE

);



Lab 2: Implement a FOREIGN KEY constraint to relate the teacher\_id from the teachers table with the students table.



ALTER TABLE students

ADD COLUMN teacher\_id INT;



ALTER TABLE students

ADD CONSTRAINT fk\_teacher

FOREIGN KEY (teacher\_id) REFERENCES teachers(teacher\_id);







# 4 Main SQL Commands and Sub-commands (DDL)



LAB EXCERSIES :





Lab 1: Create a table courses with columns: course\_id, course\_name, and

course\_credits. Set the course\_id as the primary key.





CREATE TABLE courses (

    course\_id INT PRIMARY KEY,

    course\_name VARCHAR(100),

    course\_credits INT

);





Lab 2: Use the CREATE command to create a database university\_db



CREATE DATABASE university\_db;





# 5 ALTER Command





LAB EXCERSIES:



Lab 1: Modify the courses table by adding a column course\_duration using the ALTER command.



ALTER TABLE courses

ADD course\_duration INT;



Lab 2: Drop the course\_credits column from the courses table



ALTER TABLE courses

DROP COLUMN course\_credits;





# 6 DROP Command





LAB EXCERSIES:





Lab 1: Drop the teachers table from the school\_db database



DROP TABLE teachers;



Lab 2: Drop the students table from the school\_db database and verify that the table has been removed



-- Drop the table

DROP TABLE students;



-- Verify that it is removed

SHOW TABLES;





# 7 Data Manipulation Language (DML)





LAB EXCERSIES :



Lab 1: Insert three records into the courses table using the INSERT command.





INSERT INTO courses (course\_id, course\_name, course\_duration)

VALUES

(1, 'Computer Science', 4),

(2, 'Mathematics', 3),

(3, 'Physics', 2);





Lab 2: Update the course duration of a specific course using the UPDATE command.





UPDATE courses

SET course\_duration = 5

WHERE course\_id = 1;





Lab 3: Delete a course with a specific course\_id from the courses table using the DELETE command



DELETE FROM courses

WHERE course\_id = 3;





# 8 Data Query Language (DQL)



LAB EXCERSIES:





Lab 1: Retrieve all courses from the courses table using the SELECT statement.





SELECT \* FROM courses;





Lab 2: Sort the courses based on course\_duration in descending order using ORDER BY





SELECT \* FROM courses

ORDER BY course\_duration DESC;





Lab 3: Limit the results of the SELECT query to show only the top two courses using LIMIT.



SELECT \* FROM courses

ORDER BY course\_duration DESC

LIMIT 2;





# 9 Data Control Language (DCL)



LAB EXCRESIES:





Lab 1: Create two new users user1 and user2 and grant user1 permission to SELECT from the courses table.





-- Create user1 and user2 (with passwords)

CREATE USER 'user1'@'localhost' IDENTIFIED BY 'password1';

CREATE USER 'user2'@'localhost' IDENTIFIED BY 'password2';



-- Grant SELECT privilege on courses table to user1

GRANT SELECT ON university\_db.courses TO 'user1'@'localhost';



-- Apply changes

FLUSH PRIVILEGES;





Lab 2: Revoke the INSERT permission from user1 and give it to user2.



-- Revoke INSERT privilege from user1

REVOKE INSERT ON university\_db.courses FROM 'user1'@'localhost';



-- Grant INSERT privilege to user2

GRANT INSERT ON university\_db.courses TO 'user2'@'localhost';



-- Apply changes

FLUSH PRIVILEGES;





# 10 Transaction Control Language (TCL)





LAB EXCERSIES:





Lab 1: Insert a few rows into the courses table and use COMMIT to save the changes



-- Start transaction

START TRANSACTION;



-- Insert a few rows

INSERT INTO courses (course\_id, course\_name, course\_duration)

VALUES

(4, 'Chemistry', 3),

(5, 'Biology', 2);



-- Save changes permanently

COMMIT;





Lab 2: Insert additional rows, then use ROLLBACK to undo the last insert operation.





-- Start transaction

START TRANSACTION;



-- Insert additional rows

INSERT INTO courses (course\_id, course\_name, course\_duration)

VALUES

(6, 'Economics', 4),

(7, 'History', 3);



-- Undo the above inserts

ROLLBACK;





Lab 3: Create a SAVEPOINT before updating the courses table, and use it to roll back specific changes.





-- Start transaction

START TRANSACTION;



-- Create a SAVEPOINT before making updates

SAVEPOINT before\_update;



-- Update course duration

UPDATE courses SET course\_duration = 5 WHERE course\_id = 4;

UPDATE courses SET course\_duration = 6 WHERE course\_id = 5;



-- Roll back only to the SAVEPOINT (undo updates after it)

ROLLBACK TO before\_update;



-- Save remaining changes

COMMIT;







# 11 SQL Joins



LAB EXCERSIES:





lab 1 : Create two tables: departments and employees. Perform an INNER JOIN to display employees along with their respective departments.





-- Create departments table

CREATE TABLE departments (

    dept\_id INT PRIMARY KEY,

    dept\_name VARCHAR(100)

);



-- Create employees table

CREATE TABLE employees (

    emp\_id INT PRIMARY KEY,

    emp\_name VARCHAR(100),

    dept\_id INT,

    FOREIGN KEY (dept\_id) REFERENCES departments(dept\_id)

);



-- Insert sample departments

INSERT INTO departments (dept\_id, dept\_name) VALUES

(1, 'HR'),

(2, 'Finance'),

(3, 'IT');



-- Insert sample employees

INSERT INTO employees (emp\_id, emp\_name, dept\_id) VALUES

(101, 'Alice', 1),

(102, 'Bob', 2),

(103, 'Charlie', 3),

(104, 'David', 1);



-- Perform INNER JOIN (only matching records)

SELECT employees.emp\_id, employees.emp\_name, departments.dept\_name

FROM employees

INNER JOIN departments ON employees.dept\_id = departments.dept\_id;





Lab 2: Use a LEFT JOIN to show all departments, even those without employees



SELECT departments.dept\_id, departments.dept\_name, employees.emp\_name

FROM departments

LEFT JOIN employees ON departments.dept\_id = employees.dept\_id;





# 12 SQL Group By



LAB EXCERSIES:





Lab 1: Group employees by department and count the number of employees in each department using GROUP BY.





SELECT dept\_id, COUNT(emp\_id) AS total\_employees

FROM employees

GROUP BY dept\_id;



Lab 2: Use the AVG aggregate function to find the average salary of employees in each department.



SELECT d.dept\_name, COUNT(e.emp\_id) AS total\_employees

FROM departments d

LEFT JOIN employees e ON d.dept\_id = e.dept\_id

GROUP BY d.dept\_name;







# 13 SQL Stored Procedure



LAB EXCERSISES:



Lab 1: Write a stored procedure to retrieve all employees from the employees table based on department.





DELIMITER $$



CREATE PROCEDURE GetEmployeesByDepartment(IN deptId INT)

BEGIN

    SELECT emp\_id, emp\_name, dept\_id

    FROM employees

    WHERE dept\_id = deptId;

END $$



DELIMITER ;





CALL GetEmployeesByDepartment(2);





Lab 2: Write a stored procedure that accepts course\_id as input and returns the course details.



DELIMITER $$



CREATE PROCEDURE GetCourseDetails(IN c\_id INT)

BEGIN

    SELECT course\_id, course\_name, course\_duration

    FROM courses

    WHERE course\_id = c\_id;

END $$



DELIMITER ;





CALL GetCourseDetails(1);







# 14 SQL View





LAB EXCERSISES :







Lab 1: Create a view to show all employees along with their department names.





CREATE VIEW EmployeeDepartmentView AS

SELECT e.emp\_id, e.emp\_name, e.salary, d.dept\_name

FROM employees e

INNER JOIN departments d ON e.dept\_id = d.dept\_id;





SELECT \* FROM EmployeeDepartmentView;







Lab 2: Modify the view to exclude employees whose salaries are below $50,000.





CREATE OR REPLACE VIEW EmployeeDepartmentView AS

SELECT e.emp\_id, e.emp\_name, e.salary, d.dept\_name

FROM employees e

INNER JOIN departments d ON e.dept\_id = d.dept\_id

WHERE e.salary >= 50000;





SELECT \* FROM EmployeeDepartmentView;







# 15 SQL Triggers



LAB EXCERSISES :



Lab 1: Create a trigger to automatically log changes to the employees table when a new employee is added.





CREATE TABLE employee\_log (

    log\_id INT AUTO\_INCREMENT PRIMARY KEY,

    emp\_id INT,

    emp\_name VARCHAR(100),

    action\_type VARCHAR(50),

    action\_time TIMESTAMP DEFAULT CURRENT\_TIMESTAMP

);





Now Create a Trigger:





DELIMITER $$



CREATE TRIGGER after\_employee\_insert

AFTER INSERT ON employees

FOR EACH ROW

BEGIN

    INSERT INTO employee\_log (emp\_id, emp\_name, action\_type)

    VALUES (NEW.emp\_id, NEW.emp\_name, 'INSERT');

END $$



DELIMITER ;







Lab 2: Create a trigger to update the last\_modified timestamp whenever an employee record is updated.







ALTER TABLE employees

ADD last\_modified TIMESTAMP DEFAULT CURRENT\_TIMESTAMP ON UPDATE CURRENT\_TIMESTAMP;





Now Create a trigger:



DELIMITER $$



CREATE TRIGGER before\_employee\_update

BEFORE UPDATE ON employees

FOR EACH ROW

BEGIN

    SET NEW.last\_modified = CURRENT\_TIMESTAMP;

END $$



DELIMITER ;







# 16 Introduction to PL/SQL



LAB EXCERSIES :





Lab 1: Write a PL/SQL block to print the total number of employees from the employees table





SET SERVEROUTPUT ON;



DECLARE

    total\_employees NUMBER;

BEGIN

    SELECT COUNT(\*) INTO total\_employees

    FROM employees;

 

    DBMS\_OUTPUT.PUT\_LINE('Total Employees: ' || total\_employees);

END;

/







Lab 2: Create a PL/SQL block that calculates the total sales from an orders table.





SET SERVEROUTPUT ON;



DECLARE

    total\_sales NUMBER;

BEGIN

    SELECT SUM(total\_amount) INTO total\_sales

    FROM orders;

 

    DBMS\_OUTPUT.PUT\_LINE('Total Sales: $' || total\_sales);

END;

/





# 17 PL/SQL Control Structures



LAB EXCERSIES :





Lab 1: Write a PL/SQL block using an IF-THEN condition to check the department of an employee.







SET SERVEROUTPUT ON;



DECLARE

    v\_emp\_id   employees.emp\_id%TYPE := 101;  -- example employee ID

    v\_dept\_id  employees.dept\_id%TYPE;

BEGIN

    SELECT dept\_id INTO v\_dept\_id

    FROM employees

    WHERE emp\_id = v\_emp\_id;



    IF v\_dept\_id = 1 THEN

        DBMS\_OUTPUT.PUT\_LINE('Employee ' || v\_emp\_id || ' works in HR.');

    ELSIF v\_dept\_id = 2 THEN

        DBMS\_OUTPUT.PUT\_LINE('Employee ' || v\_emp\_id || ' works in Finance.');

    ELSE

        DBMS\_OUTPUT.PUT\_LINE('Employee ' || v\_emp\_id || ' works in another department.');

    END IF;

END;

/







Lab 2: Use a FOR LOOP to iterate through employee records and display their names.







SET SERVEROUTPUT ON;



BEGIN

    FOR emp\_rec IN (SELECT emp\_name FROM employees) LOOP

        DBMS\_OUTPUT.PUT\_LINE('Employee Name: ' || emp\_rec.emp\_name);

    END LOOP;

END;

/









# 18 SQL Cursors



LAB EXCERSISES :





Lab 1: Write a PL/SQL block using an explicit cursor to retrieve and display employee details.





SET SERVEROUTPUT ON;



DECLARE

    -- Declare the cursor

    CURSOR emp\_cursor IS

        SELECT emp\_id, emp\_name, dept\_id, salary

        FROM employees;



    -- Variables to store fetched values

    v\_emp\_id   employees.emp\_id%TYPE;

    v\_emp\_name employees.emp\_name%TYPE;

    v\_dept\_id  employees.dept\_id%TYPE;

    v\_salary   employees.salary%TYPE;

BEGIN

    -- Open the cursor

    OPEN emp\_cursor;



    LOOP

        -- Fetch data into variables

        FETCH emp\_cursor INTO v\_emp\_id, v\_emp\_name, v\_dept\_id, v\_salary;



        -- Exit loop when no more rows

        EXIT WHEN emp\_cursor%NOTFOUND;



        -- Display the data

        DBMS\_OUTPUT.PUT\_LINE('ID: ' || v\_emp\_id ||

                             ', Name: ' || v\_emp\_name ||

                             ', Dept: ' || v\_dept\_id ||

                             ', Salary: ' || v\_salary);

    END LOOP;



    -- Close the cursor

    CLOSE emp\_cursor;

END;

/





Lab 2: Create a cursor to retrieve all courses and display them one by one.







SET SERVEROUTPUT ON;



DECLARE

    -- Declare the cursor

    CURSOR course\_cursor IS

        SELECT course\_id, course\_name, duration

        FROM courses;



    -- Variables to store fetched values

    v\_course\_id   courses.course\_id%TYPE;

    v\_course\_name courses.course\_name%TYPE;

    v\_duration    courses.duration%TYPE;

BEGIN

    -- Open the cursor

    OPEN course\_cursor;



    LOOP

        -- Fetch data into variables

        FETCH course\_cursor INTO v\_course\_id, v\_course\_name, v\_duration;



        -- Exit when no more rows

        EXIT WHEN course\_cursor%NOTFOUND;



        -- Display the data

        DBMS\_OUTPUT.PUT\_LINE('Course ID: ' || v\_course\_id ||

                             ', Name: ' || v\_course\_name ||

                             ', Duration: ' || v\_duration);

    END LOOP;



    -- Close the cursor

    CLOSE course\_cursor;

END;

/







# 19 Rollback and Commit Savepoint



LAB EXCERSIES :





Lab 1: Perform a transaction where you create a savepoint, insert records, then rollback to the savepoint.





-- Start transaction

BEGIN;



-- Insert first record

INSERT INTO employees (emp\_id, emp\_name, dept\_id, salary)

VALUES (101, 'John Doe', 10, 55000);



-- Create a savepoint

SAVEPOINT sp1;



-- Insert another record

INSERT INTO employees (emp\_id, emp\_name, dept\_id, salary)

VALUES (102, 'Jane Smith', 20, 60000);



-- Rollback to the savepoint (Jane's record will be undone)

ROLLBACK TO sp1;



-- Commit remaining changes (only John's record will be saved)

COMMIT;









Lab 2: Commit part of a transaction after using a savepoint and then rollback the remaining changes.







-- Start transaction

BEGIN;



-- Insert first record

INSERT INTO employees (emp\_id, emp\_name, dept\_id, salary)

VALUES (103, 'Alice Brown', 30, 50000);



-- Create savepoint

SAVEPOINT sp2;



-- Insert second record

INSERT INTO employees (emp\_id, emp\_name, dept\_id, salary)

VALUES (104, 'Bob Green', 40, 65000);



-- Commit the first part (Alice will be saved)

COMMIT;



-- Insert another record after commit

INSERT INTO employees (emp\_id, emp\_name, dept\_id, salary)

VALUES (105, 'Charlie White', 50, 70000);



-- Rollback changes made after the commit (Charlie will be undone)

ROLLBACK;



-- End transaction (optional if already committed/rolled back)

COMMIT;







### EXTRA LAB EXCERSIES





#### 1\. Introduction to SQL





Lab 3: Create a database called library\_db and a table books with columns: book\_id, title, author, publisher, year\_of\_publication, and price. Insert five records into the table.







-- Create the database

CREATE DATABASE library\_db;



-- Use the database

USE library\_db;



-- Create the books table

CREATE TABLE books (

    book\_id INT PRIMARY KEY,

    title VARCHAR(100) NOT NULL,

    author VARCHAR(100),

    publisher VARCHAR(100),

    year\_of\_publication INT,

    price DECIMAL(8,2)

);



-- Insert five records

INSERT INTO books (book\_id, title, author, publisher, year\_of\_publication, price)

VALUES

(1, 'To Kill a Mockingbird', 'Harper Lee', 'J.B. Lippincott \& Co.', 1960, 350.00),

(2, '1984', 'George Orwell', 'Secker \& Warburg', 1949, 299.99),

(3, 'The Great Gatsby', 'F. Scott Fitzgerald', 'Charles Scribner''s Sons', 1925, 400.50),

(4, 'Pride and Prejudice', 'Jane Austen', 'T. Egerton', 1813, 250.00),

(5, 'The Hobbit', 'J.R.R. Tolkien', 'George Allen \& Unwin', 1937, 500.00);







Lab 4: Create a table members in library\_db with columns: member\_id, member\_name, date\_of\_membership, and email. Insert five records into this table.







-- Create the members table

CREATE TABLE members (

    member\_id INT PRIMARY KEY,

    member\_name VARCHAR(100) NOT NULL,

    date\_of\_membership DATE,

    email VARCHAR(100) UNIQUE

);



-- Insert five records

INSERT INTO members (member\_id, member\_name, date\_of\_membership, email)

VALUES

(1, 'Rahul Sharma', '2023-01-15', 'rahul.sharma@example.com'),

(2, 'Priya Patel', '2022-06-20', 'priya.patel@example.com'),

(3, 'Amit Verma', '2023-03-10', 'amit.verma@example.com'),

(4, 'Neha Gupta', '2021-09-05', 'neha.gupta@example.com'),

(5, 'Ravi Kumar', '2022-12-25', 'ravi.kumar@example.com');







#### 2 SQL Syntax





Lab 3: Retrieve all members who joined the library before 2022. Use appropriate SQL syntax with WHERE and ORDER BY.





-- Select members who joined before 1st Jan 2022, sorted by joining date

SELECT \*

FROM members

WHERE date\_of\_membership < '2022-01-01'

ORDER BY date\_of\_membership ASC;



Lab 4: Write SQL queries to display the titles of books published by a specific author. Sort the results by year\_of\_publication in descending order.



SELECT title, year\_of\_publication

FROM books

WHERE author = 'George Orwell'

ORDER BY year\_of\_publication DESC;







#### 3 SQL Constraints





##### Lab 3: Add a CHECK constraint to ensure that the price of books in the books table is greater than 0.





ALTER TABLE books

ADD CONSTRAINT chk\_price\_positive

CHECK (price > 0);





##### Lab 4: Modify the members table to add a UNIQUE constraint on the email column, ensuring that each member has a unique email address





ALTER TABLE members

ADD CONSTRAINT unique\_email

UNIQUE (email);





#### 4 Main SQL Commands and Sub-commands (DDL)



##### Lab 3: Create a table authors with the following columns: author\_id, first\_name, last\_name, and country. Set author\_id as the primary key







CREATE TABLE authors (

    author\_id INT PRIMARY KEY,

    first\_name VARCHAR(50),

    last\_name VARCHAR(50),

    country VARCHAR(50)

);



##### 

##### Lab 4: Create a table publishers with columns: publisher\_id, publisher\_name, contact\_number, and address. Set publisher\_id as the primary key and contact\_number as unique.





CREATE TABLE publishers (

    publisher\_id INT PRIMARY KEY,

    publisher\_name VARCHAR(100),

    contact\_number VARCHAR(15) UNIQUE,

    address VARCHAR(255)

);







#### 5 ALTER Command





##### Lab 3: Add a new column genre to the books table. Update the genre for all existing records.

##### 



-- Add a new column 'genre'

ALTER TABLE books

ADD genre VARCHAR(50);



-- Update genre for all existing records

UPDATE books

SET genre = 'Fiction';  -- You can set different genres based on book\_id if needed







##### Lab 4: Modify the members table to increase the length of the email column to 100 characters.

##### 

ALTER TABLE members

MODIFY email VARCHAR(100);







#### 6 DROP Command





##### Lab 3: Drop the publishers table from the database after verifying its structure.

##### 

-- Verify the structure of the publishers table

DESC publishers;   -- In MySQL

-- or

-- SELECT \* FROM publishers LIMIT 5;  -- Optional, to preview data



-- Drop the table

DROP TABLE publishers;



##### 

##### Lab 4: Create a backup of the members table and then drop the original members table.







-- Create a backup table with the same structure and data

CREATE TABLE members\_backup AS

SELECT \* FROM members;



-- Verify backup

SELECT \* FROM members\_backup;



-- Drop the original members table

DROP TABLE members;







#### 7 Data Manipulation Language (DML)





##### Lab 4: Insert three new authors into the authors table, then update the last name of one of the authors.

##### 

-- Insert three new authors

INSERT INTO authors (author\_id, first\_name, last\_name, country)

VALUES

(1, 'George', 'Orwell', 'United Kingdom'),

(2, 'Harper', 'Lee', 'United States'),

(3, 'J.K.', 'Rowling', 'United Kingdom');



-- Update the last name of one author

UPDATE authors

SET last\_name = 'Smith'

WHERE author\_id = 2;

##### 

##### Lab 5: Delete a book from the books table where the price is higher than $100.





DELETE FROM books

WHERE price > 100;





#### 8 UPDATE Command





##### Lab 3: Update the year\_of\_publication of a book with a specific book\_id.





UPDATE books

SET year\_of\_publication = 2020

WHERE book\_id = 3;  -- Change 3 to the actual book\_id you want to update

##### 

##### 

##### Lab 4: Increase the price of all books published before 2015 by 10%.





UPDATE books

SET price = price \* 1.10

WHERE year\_of\_publication < 2015;









#### 9 DELETE Comand





##### Lab 3: Remove all members who joined before 2020 from the members table.



DELETE FROM members

WHERE join\_date < '2020-01-01';

##### 

##### Lab 4: Delete all books that have a NULL value in the author column.



DELETE FROM books

WHERE author IS NULL;





#### 10 Data Query Language (DQL)



##### Lab 4: Write a query to retrieve all books with price between $50 and $100



SELECT \*

FROM books

WHERE price BETWEEN 50 AND 100;



##### 

##### Lab 5: Retrieve the list of books sorted by author in ascending order and limit the results to the top 3 entries.



SELECT \*

FROM books

ORDER BY author ASC

LIMIT 3;





#### 11 Data Control Language (DCL)



##### Lab 3: Grant SELECT permission to a user named librarian on the books table.



GRANT SELECT

ON books

TO 'librarian';

##### 

##### Lab 4: Grant INSERT and UPDATE permissions to the user admin on the members table.



GRANT INSERT, UPDATE

ON members

TO 'admin';





#### 12 REVOKE Command



##### Lab 3: Revoke the INSERT privilege from the user librarian on the books table.



REVOKE INSERT

ON books

FROM 'librarian';

##### 

##### Lab 4: Revoke all permissions from user admin on the members table.



REVOKE ALL PRIVILEGES

ON members

FROM 'admin';





#### 13 Transaction Control Language (TCL)

#### 

#### Lab 3: Use COMMIT after inserting multiple records into the books table, then make another insertion and perform a ROLLBACK.



-- Start transaction

START TRANSACTION;



-- Insert multiple books

INSERT INTO books (title, author, price) VALUES ('Book A', 'Author A', 55);

INSERT INTO books (title, author, price) VALUES ('Book B', 'Author B', 75);

INSERT INTO books (title, author, price) VALUES ('Book C', 'Author C', 95);



-- Commit the above changes

COMMIT;



-- Start another transaction

START TRANSACTION;



-- Insert another book

INSERT INTO books (title, author, price) VALUES ('Book D', 'Author D', 65);



-- Rollback the last insertion

ROLLBACK;



#### Lab 4: Set a SAVEPOINT before making updates to the members table, perform some updates, and then roll back to the SAVEPOINT





-- Start transaction

START TRANSACTION;



-- Create a SAVEPOINT

SAVEPOINT before\_updates;



-- Perform updates

UPDATE members SET join\_date = '2023-01-01' WHERE member\_id = 1;

UPDATE members SET join\_date = '2024-05-05' WHERE member\_id = 2;



-- Rollback to the savepoint (undo the above updates, but keep earlier changes in transaction)

ROLLBACK TO before\_updates;



-- Commit remaining changes

COMMIT;





#### 14 SQL Joins





##### Lab 3: Perform an INNER JOIN between books and authors tables to display the title of books and their respective authors' names.



SELECT b.title, a.name AS author\_name

FROM books b

INNER JOIN authors a

&nbsp;   ON b.author\_id = a.author\_id;



##### 

##### Lab 4: Use a FULL OUTER JOIN to retrieve all records from the books and authors tables, including those with no matching entries in the other table





SELECT b.title, a.name AS author\_name

FROM books b

FULL OUTER JOIN authors a

&nbsp;   ON b.author\_id = a.author\_id;







#### 15 SQL Group By



##### Lab 3: Group books by genre and display the total number of books in each genre



SELECT genre, COUNT(\*) AS total\_books

FROM books

GROUP BY genre;

##### 

##### 

##### Lab 4: Group members by the year they joined and find the number of members who joined each year.





-- MySQL

SELECT YEAR(join\_date) AS join\_year, COUNT(\*) AS total\_members

FROM members

GROUP BY YEAR(join\_date);





#### 16 SQL Stored Procedure





#### Lab 3: Write a stored procedure to retrieve all books by a particular author.





DELIMITER $$



CREATE PROCEDURE GetBooksByAuthor(IN authorName VARCHAR(100))

BEGIN

&nbsp;   SELECT b.book\_id, b.title, b.genre, b.price

&nbsp;   FROM books b

&nbsp;   INNER JOIN authors a ON b.author\_id = a.author\_id

&nbsp;   WHERE a.name = authorName;

END $$



DELIMITER ;



Call :



CALL GetBooksByAuthor('J.K. Rowling');



#### 

#### 

#### Lab 4: Write a stored procedure that takes book\_id as an argument and returns the price of the book.



DELIMITER $$



CREATE PROCEDURE GetBookPrice(IN p\_book\_id INT)

BEGIN

&nbsp;   SELECT price

&nbsp;   FROM books

&nbsp;   WHERE book\_id = p\_book\_id;

END $$



DELIMITER ;





Call :



CALL GetBookPrice(5);





#### 17 SQL View



##### Lab 3: Create a view to show only the title, author, and price of books from the books table 



CREATE VIEW BookDetails AS

SELECT b.title, a.name AS author, b.price

FROM books b

JOIN authors a ON b.author\_id = a.author\_id;





SELECT \* FROM BookDetails;

##### 

##### Lab 4: Create a view to display members who joined before 2020



CREATE VIEW MembersBefore2020 AS

SELECT \*

FROM members

WHERE YEAR(join\_date) < 2020;





SELECT \* FROM MembersBefore2020;





#### 18 SQL Trigger

##### 

##### Lab 3: Create a trigger to automatically update the last\_modified timestamp of the books table whenever a record is updated.



DELIMITER $$



CREATE TRIGGER UpdateLastModified

BEFORE UPDATE ON books

FOR EACH ROW

BEGIN

&nbsp;   SET NEW.last\_modified = NOW();

END $$



DELIMITER ;



##### 

##### Lab 4: Create a trigger that inserts a log entry into a log\_changes table whenever a DELETE operation is performed on the books table



DELIMITER $$



CREATE TRIGGER LogBookDeletion

AFTER DELETE ON books

FOR EACH ROW

BEGIN

&nbsp;   INSERT INTO log\_changes (book\_id, title, deleted\_at)

&nbsp;   VALUES (OLD.book\_id, OLD.title, NOW());

END $$



DELIMITER ;





#### 19 Introduction to PL/SQL





##### Lab 3: Write a PL/SQL block to insert a new book into the books table and display a confirmation message.



SET SERVEROUTPUT ON;



DECLARE

&nbsp;   v\_book\_id   books.book\_id%TYPE := 101;  -- Example ID

&nbsp;   v\_title     books.title%TYPE := 'The New Era';

&nbsp;   v\_author\_id books.author\_id%TYPE := 5;

&nbsp;   v\_price     books.price%TYPE := 499;

BEGIN

&nbsp;   INSERT INTO books (book\_id, title, author\_id, price)

&nbsp;   VALUES (v\_book\_id, v\_title, v\_author\_id, v\_price);

&nbsp;   

&nbsp;   DBMS\_OUTPUT.PUT\_LINE('Book "' || v\_title || '" inserted successfully.');

END;

/



##### 

##### Lab 4: Write a PL/SQL block to display the total number of books in the books table



SET SERVEROUTPUT ON;



DECLARE

&nbsp;   v\_total\_books NUMBER;

BEGIN

&nbsp;   SELECT COUNT(\*) INTO v\_total\_books

&nbsp;   FROM books;

&nbsp;   

&nbsp;   DBMS\_OUTPUT.PUT\_LINE('Total number of books: ' || v\_total\_books);

END;

/



#### 20 PL/SQL Syntax



#### Lab 3: Write a PL/SQL block to declare variables for book\_id and price, assign values, and display the results.



SET SERVEROUTPUT ON;



DECLARE

&nbsp;   v\_book\_id  NUMBER;

&nbsp;   v\_price    NUMBER(8,2);

BEGIN

&nbsp;   -- Assign values

&nbsp;   v\_book\_id := 101;

&nbsp;   v\_price := 499.99;



&nbsp;   -- Display the results

&nbsp;   DBMS\_OUTPUT.PUT\_LINE('Book ID: ' || v\_book\_id);

&nbsp;   DBMS\_OUTPUT.PUT\_LINE('Price: ₹' || v\_price);

END;

/





#### 

#### Lab 4: Write a PL/SQL block using constants and perform arithmetic operations on book prices.





SET SERVEROUTPUT ON;



DECLARE

&nbsp;   c\_price1 CONSTANT NUMBER(8,2) := 300.00;

&nbsp;   c\_price2 CONSTANT NUMBER(8,2) := 450.00;

&nbsp;   v\_total   NUMBER(8,2);

&nbsp;   v\_diff    NUMBER(8,2);

BEGIN

&nbsp;   -- Perform arithmetic

&nbsp;   v\_total := c\_price1 + c\_price2;

&nbsp;   v\_diff  := c\_price2 - c\_price1;



&nbsp;   -- Display results

&nbsp;   DBMS\_OUTPUT.PUT\_LINE('Price 1: ₹' || c\_price1);

&nbsp;   DBMS\_OUTPUT.PUT\_LINE('Price 2: ₹' || c\_price2);

&nbsp;   DBMS\_OUTPUT.PUT\_LINE('Total Price: ₹' || v\_total);

&nbsp;   DBMS\_OUTPUT.PUT\_LINE('Price Difference: ₹' || v\_diff);

END;

/





#### 

#### 21 PL/SQL Control Structures



##### 

##### Lab 3: Write a PL/SQL block using IF-THEN-ELSE to check if a book's price is above $100 and print a message accordingly.



SET SERVEROUTPUT ON;



DECLARE

&nbsp;   v\_price NUMBER(8,2) := 120;  -- Example price

BEGIN

&nbsp;   IF v\_price > 100 THEN

&nbsp;       DBMS\_OUTPUT.PUT\_LINE('The book price is above $100.');

&nbsp;   ELSE

&nbsp;       DBMS\_OUTPUT.PUT\_LINE('The book price is $100 or below.');

&nbsp;   END IF;

END;

/



##### 

##### Lab 4: Use a FOR LOOP in PL/SQL to display the details of all books one by one.



SET SERVEROUTPUT ON;



DECLARE

&nbsp;   CURSOR book\_cursor IS

&nbsp;       SELECT book\_id, title, price

&nbsp;       FROM books;

BEGIN

&nbsp;   FOR rec IN book\_cursor LOOP

&nbsp;       DBMS\_OUTPUT.PUT\_LINE('Book ID: ' || rec.book\_id ||

&nbsp;                            ', Title: ' || rec.title ||

&nbsp;                            ', Price: $' || rec.price);

&nbsp;   END LOOP;

END;

/



#### 22 SQL Cursors



##### Lab 3: Write a PL/SQL block using an explicit cursor to fetch and display all records from the members table.



SET SERVEROUTPUT ON;



DECLARE

&nbsp;   -- Declare cursor

&nbsp;   CURSOR member\_cursor IS

&nbsp;       SELECT member\_id, name, join\_date

&nbsp;       FROM members;



&nbsp;   -- Declare variables for fetched data

&nbsp;   v\_member\_id members.member\_id%TYPE;

&nbsp;   v\_name      members.name%TYPE;

&nbsp;   v\_join\_date members.join\_date%TYPE;

BEGIN

&nbsp;   OPEN member\_cursor;



&nbsp;   LOOP

&nbsp;       FETCH member\_cursor INTO v\_member\_id, v\_name, v\_join\_date;

&nbsp;       EXIT WHEN member\_cursor%NOTFOUND;



&nbsp;       DBMS\_OUTPUT.PUT\_LINE('Member ID: ' || v\_member\_id ||

&nbsp;                            ', Name: ' || v\_name ||

&nbsp;                            ', Joined: ' || v\_join\_date);

&nbsp;   END LOOP;



&nbsp;   CLOSE member\_cursor;

END;

/



##### 

##### Lab 4: Create a cursor to retrieve books by a particular author and display their titles.



SET SERVEROUTPUT ON;



DECLARE

&nbsp;   v\_author\_name VARCHAR2(100) := 'J.K. Rowling';  -- Change as needed



&nbsp;   -- Declare cursor with parameter

&nbsp;   CURSOR books\_by\_author IS

&nbsp;       SELECT b.title

&nbsp;       FROM books b

&nbsp;       JOIN authors a ON b.author\_id = a.author\_id

&nbsp;       WHERE a.name = v\_author\_name;



&nbsp;   v\_title books.title%TYPE;

BEGIN

&nbsp;   OPEN books\_by\_author;



&nbsp;   LOOP

&nbsp;       FETCH books\_by\_author INTO v\_title;

&nbsp;       EXIT WHEN books\_by\_author%NOTFOUND;



&nbsp;       DBMS\_OUTPUT.PUT\_LINE('Title: ' || v\_title);

&nbsp;   END LOOP;



&nbsp;   CLOSE books\_by\_author;

END;

/



#### 23 Rollback and Commit Savepoint





##### Lab 3: Perform a transaction that includes inserting a new member, setting a SAVEPOINT, and rolling back to the savepoint after making updates.



-- Start transaction

INSERT INTO members (member\_id, name, join\_date)

VALUES (301, 'Alice Johnson', SYSDATE);



-- Set a savepoint after the insert

SAVEPOINT after\_insert;



-- Make some updates

UPDATE members

SET name = 'Alice J.'

WHERE member\_id = 301;



UPDATE members

SET join\_date = TO\_DATE('2022-01-15', 'YYYY-MM-DD')

WHERE member\_id = 301;



-- Roll back to savepoint (undo updates, keep the insert)

ROLLBACK TO after\_insert;



-- Commit the insert

COMMIT;



##### 

##### 

##### Lab 4: Use COMMIT after successfully inserting multiple books into the books table, then use ROLLBACK to undo a set of changes made after a savepoint.





-- Insert multiple books

INSERT INTO books (book\_id, title, author\_id, price)

VALUES (601, 'Database Systems', 1, 450);



INSERT INTO books (book\_id, title, author\_id, price)

VALUES (602, 'Advanced SQL', 2, 500);



INSERT INTO books (book\_id, title, author\_id, price)

VALUES (603, 'PL/SQL Programming', 3, 550);



-- Commit successful inserts

COMMIT;



-- Set savepoint

SAVEPOINT before\_changes;



-- Make changes after the savepoint

UPDATE books

SET price = price + 50

WHERE book\_id = 601;



DELETE FROM books

WHERE book\_id = 603;



-- Rollback to savepoint (undo updates \& deletes after savepoint)

ROLLBACK TO before\_changes;



-- Final commit

COMMIT;





&nbsp;                        



##### 

#### 



##### 

#### 





