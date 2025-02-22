# Project Title: Library Management System
## Project Overview

**Project Title:** Library Management System

**Level:** Intermediate

**Database:** `library_db`

This project demonstrates the implementation of a Library Management System using SQL. It includes creating and managing tables, performing CRUD operations, and executing advanced SQL queries. The goal is to showcase skills in database design, manipulation, and querying.


![library](https://github.com/user-attachments/assets/1440c86b-909c-4776-b59a-95d16cfa103e)

## Objectives

1. Set up the Library Management System Database: Create and populate the database with tables for branches, employees, members, books, issued status, and return status.

2. CRUD Operations: Perform Create, Read, Update, and Delete operations on the data.

3. CTAS (Create Table As Select): Utilize CTAS to create new tables based on query results.

4. Advanced SQL Queries: Develop complex queries to analyze and retrieve specific data.


## Project Structure

1. **Database Setup**

![library_erd](https://github.com/user-attachments/assets/e5573066-2bed-428e-9c3c-05d9fa217c47)

- **Database Creation:** Created a database named `library_db`.

- **Table Creation:** Created tables for branches, employees, members, books, issued status, and return status. Each table includes relevant columns and relationships.

```sql
CREATE DATABASE library_db;

DROP TABLE IF EXISTS branch;
CREATE TABLE branch
(
            branch_id VARCHAR(10) PRIMARY KEY,
            manager_id VARCHAR(10),
            branch_address VARCHAR(30),
            contact_no VARCHAR(15)
);


-- Create table "Employee"
DROP TABLE IF EXISTS employees;
CREATE TABLE employees
(
            emp_id VARCHAR(10) PRIMARY KEY,
            emp_name VARCHAR(30),
            position VARCHAR(30),
            salary DECIMAL(10,2),
            branch_id VARCHAR(10),
            FOREIGN KEY (branch_id) REFERENCES  branch(branch_id)
);


-- Create table "Members"
DROP TABLE IF EXISTS members;
CREATE TABLE members
(
            member_id VARCHAR(10) PRIMARY KEY,
            member_name VARCHAR(30),
            member_address VARCHAR(30),
            reg_date DATE
);



-- Create table "Books"
DROP TABLE IF EXISTS books;
CREATE TABLE books
(
            isbn VARCHAR(50) PRIMARY KEY,
            book_title VARCHAR(80),
            category VARCHAR(30),
            rental_price DECIMAL(10,2),
            status VARCHAR(10),
            author VARCHAR(30),
            publisher VARCHAR(30)
);



-- Create table "IssueStatus"
DROP TABLE IF EXISTS issued_status;
CREATE TABLE issued_status
(
            issued_id VARCHAR(10) PRIMARY KEY,
            issued_member_id VARCHAR(30),
            issued_book_name VARCHAR(80),
            issued_date DATE,
            issued_book_isbn VARCHAR(50),
            issued_emp_id VARCHAR(10),
            FOREIGN KEY (issued_member_id) REFERENCES members(member_id),
            FOREIGN KEY (issued_emp_id) REFERENCES employees(emp_id),
            FOREIGN KEY (issued_book_isbn) REFERENCES books(isbn) 
);



-- Create table "ReturnStatus"
DROP TABLE IF EXISTS return_status;
CREATE TABLE return_status
(
            return_id VARCHAR(10) PRIMARY KEY,
            issued_id VARCHAR(30),
            return_book_name VARCHAR(80),
            return_date DATE,
            return_book_isbn VARCHAR(50),
            FOREIGN KEY (return_book_isbn) REFERENCES books(isbn)
);



## 2. CRUD Operations

**Create:** Inserted sample records into the `books` table.

**Read:** Retrieved and displayed data from various tables.

**Update:** Updated records in the `employees` table.

**Delete:** Removed records from the `members` table as needed.

---

### Task 1. Create a New Book Record -- ISBN: 978-1-60129-456-2, Title: To Kill a Mockingbird, Category: Classic, Rental Price: 6.00, Status: yes, Author: Harper Lee, Publisher: J.B. Lippincott & Co.

```sql
INSERT INTO books (isbn, book_title, category, rental_price, status, author, publisher)
VALUES('978-1-60129-456-2', 'To Kill a Mockingbird', 'Classic', 6.00, 'yes', 'Harper Lee', 'J.B. Lippincott & Co.');
SELECT * FROM books;


---

### Task 2: Update an Existing Member's Address

**Details:** Update the address of the member with `member_id = 'C103'` to '125 Oak St'.

```sql
UPDATE members
SET member_address = '125 Oak St'
WHERE member_id = 'C103';


