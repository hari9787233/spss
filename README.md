Practical No1-Install and set up MySQL. Create a database and a table to store employee details. Perform basic operations like INSERT, UPDATE, and DELETE using SELECT queries.

step1-Create Database
       CREATE DATABASE company_db;

step2-Create Employee Table
    CREATE TABLE employees (
    emp_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    department VARCHAR(50),
    salary DECIMAL(10,2),
    join_date DATE
);

step3-INSERT Data
INSERT INTO employees (name, department, salary, join_date)
VALUES 
('Shreyas', 'AI', 50000, '2024-06-01'),
('Ravi', 'HR', 40000, '2023-08-15'),
('Priya', 'IT', 60000, '2022-01-10');

SELECT * FROM employees;

step4- UPDATE Data
   UPDATE employees
SET salary = 55000
WHERE name = 'Shreyas';

step5-DELETE Data
        DELETE FROM employees
WHERE name = 'Ravi';

step6-Useful SELECT Queries
SELECT name, salary FROM employees;
SELECT * FROM employees WHERE salary > 50000;
SELECT * FROM employees ORDER BY salary DESC;
SELECT COUNT(*) FROM employees;

Practical No-2-Create a table with columns for EmployeeID, Name, Salary, JoiningDate, and ActiveStatus using different data types. Insert sample data and perform queries to manipulate and retrieve data.

step1-Create the Table
   CREATE TABLE employees (
    EmployeeID INT PRIMARY KEY AUTO_INCREMENT,
    Name VARCHAR(100) NOT NULL,
    Salary DECIMAL(10,2),
    JoiningDate DATE,
    ActiveStatus BOOLEAN
);

step2-Insert Sample Data
    INSERT INTO employees (Name, Salary, JoiningDate, ActiveStatus)
VALUES
('Shreyas', 50000.00, '2024-06-01', TRUE),
('Ravi', 42000.50, '2023-03-15', TRUE),
('Priya', 61000.75, '2022-11-20', FALSE),
('Anjali', 48000.00, '2021-07-10', TRUE);

step3-Retrieve Data (SELECT Queries)
     SELECT * FROM employees;

     SELECT * FROM employees
    WHERE ActiveStatus = TRUE;
    
     SELECT Name, Salary FROM employees
     WHERE Salary > 50000;
     
     SELECT * FROM employees
    ORDER BY Salary DESC;

step4-Update Data
      UPDATE employees
      SET Salary = 55000
      WHERE Name = 'Shreyas';
  
     UPDATE employees
    SET ActiveStatus = FALSE
    WHERE Name = 'Ravi';

step5-Delete Data
          DELETE FROM employees
         WHERE ActiveStatus = FALSE;

step6- Useful Analytical Queries
🔹 Count total employees
SELECT COUNT(*) AS TotalEmployees FROM employees;
🔹 Average salary
SELECT AVG(Salary) AS AvgSalary FROM employees;
🔹 Highest salary
SELECT MAX(Salary) AS HighestSalary FROM employees;


Practical3-Create a table to store employee information with constraints like Primary Key, Foreign Key, and Unique. Insert valid and invalid data to test the constraints.

step1-Create Department Table (for Foreign Key)

CREATE TABLE departments (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(100) UNIQUE
);

step2-Create Employee Table with Constraints

CREATE TABLE employees (
    emp_id INT PRIMARY KEY AUTO_INCREMENT,
    email VARCHAR(100) UNIQUE,
    name VARCHAR(100) NOT NULL,
    salary DECIMAL(10,2) CHECK (salary > 0),
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES departments(dept_id)
);

step3-Insert VALID Data

INSERT INTO employees (email, name, salary, dept_id)
VALUES
('shreyas@gmail.com', 'Shreyas', 50000, 2),
('ravi@gmail.com', 'Ravi', 40000, 1),
('priya@gmail.com', 'Priya', 60000, 3);

step4-Insert INVALID Data (Testing Constraints)

INSERT INTO employees (email, name, salary, dept_id)
VALUES ('shreyas@gmail.com', 'Amit', 45000, 2);

INSERT INTO employees (email, name, salary, dept_id)
VALUES ('amit@gmail.com', 'Amit', 45000, 10);

INSERT INTO employees (email, name, salary, dept_id)
VALUES ('neha@gmail.com', 'Neha', -1000, 1);

INSERT INTO employees (email, name, salary, dept_id)
VALUES ('raj@gmail.com', NULL, 30000, 1);

step5-View Data
SELECT * FROM employees;

Practical4-Create a table for Customer details with various integrity constraints like NOT NULL, CHECK, and DEFAULT. Insert valid and invalid data to test these constraints and ensure data integrity.

step1-Create Customer Table with Constraints

CREATE TABLE customers (
    customer_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    age INT CHECK (age >= 18),
    city VARCHAR(50) DEFAULT 'Unknown',
    balance DECIMAL(10,2) CHECK (balance >= 0) DEFAULT 0.00,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

step2-Insert VALID Data

INSERT INTO customers (name, email, age, city, balance)
VALUES
('Shreyas', 'shreyas@gmail.com', 21, 'Pune', 1500.50),
('Ravi', 'ravi@gmail.com', 30, 'Mumbai', 2000.00);

->Using DEFAULT values
INSERT INTO customers (name, email, age)
VALUES ('Priya', 'priya@gmail.com', 25);

step3-Insert INVALID Data (to Test Constraints)

INSERT INTO customers (name, email, age)
VALUES (NULL, 'test@gmail.com', 22);

INSERT INTO customers (name, email, age)
VALUES ('Amit', 'shreyas@gmail.com', 28);

INSERT INTO customers (name, email, age)
VALUES ('Neha', 'neha@gmail.com', 15);

INSERT INTO customers (name, email, age, balance)
VALUES ('Raj', 'raj@gmail.com', 26, -500);

step4-Retrieve Data

SELECT * FROM customers;

Practical5-Use DDL commands to create tables and DML commands to insert, update, and delete data. Write SELECT queries to retrieve and verify data changes.

step1-DDL — Create Table

CREATE TABLE employees (
    emp_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    department VARCHAR(50),
    salary DECIMAL(10,2),
    join_date DATE
);

step2-DML — Insert Data

INSERT INTO employees (name, department, salary, join_date)
VALUES
('Shreyas', 'AI', 50000, '2024-06-01'),
('Ravi', 'HR', 40000, '2023-03-15'),
('Priya', 'IT', 60000, '2022-11-20');

step3-DML — Update Data

UPDATE employees
SET salary = 55000
WHERE name = 'Shreyas';

step4-DML — Delete Data

DELETE FROM employees
WHERE name = 'Ravi';

step5- Additional SELECT Queries (Verification + Insight)
🔹 Employees with salary > 50,000
SELECT * FROM employees
WHERE salary > 50000;
🔹 Sort by salary (descending)
SELECT * FROM employees
ORDER BY salary DESC;
🔹 Count employees
SELECT COUNT(*) AS total_employees FROM employees;

Practical6-Normalize an unnormalized schema for storing customer orders into 1NF, 2NF, 3NF, and BCNF. Apply key constraints like Primary Key and Foreign Key.

Step1-First Normal Form (1NF)

CREATE TABLE OrderDetails_1NF (
    OrderID INT,
    CustomerName VARCHAR(100),
    CustomerAddress VARCHAR(200),
    ProductID INT,
    ProductName VARCHAR(100),
    Quantity INT,
    Price DECIMAL(10,2)
);

step2-Second Normal Form (2NF)

-- Orders table
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerName VARCHAR(100),
    CustomerAddress VARCHAR(200)
);

-- Products table
CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR(100),
    Price DECIMAL(10,2)
);

-- Order Items table
CREATE TABLE OrderItems (
    OrderID INT,
    ProductID INT,
    Quantity INT,
    PRIMARY KEY (OrderID, ProductID),
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID),
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID)
);

step3-Third Normal Form (3NF)

CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    CustomerName VARCHAR(100),
    CustomerAddress VARCHAR(200)
);

-- Modify Orders table
CREATE TABLE Orders_3NF (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);

step4-Boyce-Codd Normal Form (BCNF)

 Rule: Every determinant must be a candidate key

Check all tables:

Customers → OK (CustomerID → all)
Products → OK (ProductID → all)
Orders_3NF → OK
OrderItems → (OrderID, ProductID) → Quantity ✔

No hidden functional dependency remains.

✔ Already in BCNF

step5-Final Structure (Clean Design)

You now have:

--Customers
CustomerID (PK), CustomerName, CustomerAddress
--Orders
OrderID (PK), CustomerID (FK)
--Products
ProductID (PK), ProductName, Price
--OrderItems
OrderID (FK), ProductID (FK), Quantity
PRIMARY KEY (OrderID, ProductID)

Practical7-Create a Sales table and use aggregate functions like COUNT, SUM, AVG, MIN, and MAX to summarize sales data and calculate statistics.

step1-Create Sales Table

CREATE TABLE Sales (
    sale_id INT PRIMARY KEY AUTO_INCREMENT,
    product_name VARCHAR(100),
    quantity INT,
    price DECIMAL(10,2),
    sale_date DATE
);

step2-Insert Sample Data

INSERT INTO Sales (product_name, quantity, price, sale_date)
VALUES
('Laptop', 2, 50000, '2025-01-10'),
('Mouse', 5, 500, '2025-01-11'),
('Keyboard', 3, 1500, '2025-01-12'),
('Laptop', 1, 52000, '2025-01-13'),
('Mouse', 10, 450, '2025-01-14');

step3-View Data

SELECT * FROM Sales;

step4-Aggregate Functions (Core Part)

COUNT — Total number of sales
SELECT COUNT(*) AS total_sales FROM Sales;

SUM — Total revenue
SELECT SUM(quantity * price) AS total_revenue FROM Sales;

AVG — Average price
SELECT AVG(price) AS avg_price FROM Sales;

MIN — Lowest price
SELECT MIN(price) AS lowest_price FROM Sales;

MAX — Highest price
SELECT MAX(price) AS highest_price FROM Sales;

step5-Group-Based Aggregation (More Realistic)

SELECT 
    product_name,
    COUNT(*) AS total_orders,
    SUM(quantity) AS total_quantity,
    SUM(quantity * price) AS total_revenue,
    AVG(price) AS avg_price,
    MIN(price) AS min_price,
    MAX(price) AS max_price
FROM Sales
GROUP BY product_name;

Practical8-Design and implement any 5-query using MongoDB.

step1-Create Database & Collection

use companyDB

step2-Insert Sample Documents

db.sales.insertMany([
  {
    customer: "Shreyas",
    product: "Laptop",
    quantity: 1,
    price: 50000,
    city: "Pune",
    date: new Date("2025-01-10")
  },
  {
    customer: "Ravi",
    product: "Mouse",
    quantity: 5,
    price: 500,
    city: "Mumbai",
    date: new Date("2025-01-11")
  },
  {
    customer: "Priya",
    product: "Keyboard",
    quantity: 2,
    price: 1500,
    city: "Delhi",
    date: new Date("2025-01-12")
  },
  {
    customer: "Shreyas",
    product: "Mouse",
    quantity: 3,
    price: 450,
    city: "Pune",
    date: new Date("2025-01-13")
  }
])

step3-
Query 1 — Retrieve All Documents

db.sales.find()

Query 2 — Filter Data (Condition)

db.sales.find({ city: "Pune" })

Query 3 — Projection (Select Specific Fields)

db.sales.find(
  { product: "Mouse" },
  { customer: 1, quantity: 1, _id: 0 }
)

Query 4 — Update Data

db.sales.updateOne(
  { customer: "Ravi" },
  { $set: { price: 550 } }
)

Query 5 — Delete Data

db.sales.deleteOne({ customer: "Priya" })








