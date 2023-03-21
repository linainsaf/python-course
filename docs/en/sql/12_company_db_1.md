# Company Database Introduction 

In the modern era of technology, most businesses depend on software to manage and track various aspects of their operations. One of the most important types of software that businesses rely on is the database management system (DBMS). A DBMS allows companies to store, manage, and retrieve information in a structured and organized way. A company database is a type of DBMS that is specifically designed to help organizations store and manage information about their employees, customers, products, and services.

<br />

A company database can be used for a wide range of purposes, such as tracking inventory, processing transactions, generating reports, and analyzing data. By keeping all the relevant information in a centralized location, a company database provides a more efficient and accurate way to manage and analyze data. This, in turn, enables businesses to make informed decisions based on reliable and up-to-date information.

<br />

Having a well-designed and properly maintained company database is vital to the success of any business. A good company database can help to improve operational efficiency, streamline processes, and enhance customer satisfaction. It can also help organizations to identify trends, analyze performance, and make strategic decisions based on real data.

<br />

In this chapter, we will explore the various components of a company database, including tables, fields, and relationships. We will also learn how to design and build a company database from scratch, as well as how to use SQL to retrieve, analyze, and manipulate data. By the end of this tutorial, you should have a good understanding how to build a database from scratch for your own business or project.

## Summary of the project 

This project will focus on building a company database that includes seven tables:

* employees
* departments
* projects
* department_projects
* employee_projects
* jobs
* location

These tables will be linked together using foreign keys and relationships, allowing organizations to easily access and manage information. The project will also include the creation of primary keys, indexes, and constraints to ensure the integrity and consistency of the data. This database will provide a robust platform for companies to store, organize, and access data in a way that enhances their ability to make data-driven decisions.

## Set up the project 

Start by opening your MySQL client and connecting to your server. In our case just start MySQL Workbench like in the installation section. 

### Database creation 
Create a new database call `company` with the graphic interface like in the installation section or with the SQL command line : 

```sql
CREATE DATABASE company;
```

if you used the command line option run also this command :

```slq
USE company;
``` 
like you've guess it just tell to MySQL to use our database for the futur queries.

### Tables creation

This is the SQL script that creates the necessary tables : 

```sql
CREATE DATABASE company;
USE company;

-- Create the jobs table
CREATE TABLE jobs (
    job_id INT PRIMARY KEY,
    job_title VARCHAR(50),
    min_salary DECIMAL(10,2),
    max_salary DECIMAL(10,2)
);

-- Create the locations table
CREATE TABLE locations (
    location_id INT PRIMARY KEY,
    city VARCHAR(50),
    state VARCHAR(50),
    country VARCHAR(50),
);


-- Create the departments table
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(50),
    location_id INT,
    FOREIGN KEY (location_id) REFERENCES locations (location_id)
);

-- Create the employees table
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(50),
    phone_number VARCHAR(20),
    hire_date DATE,
    job_id INT,
    salary DECIMAL(10,2),
    department_id INT,
    FOREIGN KEY (job_id) REFERENCES jobs (job_id),
    FOREIGN KEY (department_id) REFERENCES departments (department_id)
);



-- Create the projects table
CREATE TABLE projects (
    project_id INT PRIMARY KEY,
    project_name VARCHAR(50),
    start_date DATE,
    end_date DATE,
    estimated_cost DECIMAL(10,2)
);

-- Create the department_projects table
CREATE TABLE department_projects (
    department_id INT,
    project_id INT,
    PRIMARY KEY (department_id, project_id),
    FOREIGN KEY (department_id) REFERENCES departments (department_id),
    FOREIGN KEY (project_id) REFERENCES projects (project_id)
);

-- Create the employee_projects table
CREATE TABLE employee_projects (
    employee_id INT,
    project_id INT,
    PRIMARY KEY (employee_id, project_id),
    FOREIGN KEY (employee_id) REFERENCES employees (employee_id),
    FOREIGN KEY (project_id) REFERENCES projects (project_id)
);
```

Note that the foreign keys are created using the `CONSTRAINT` keyword and the `REFERENCES` keyword to specify the table and column to which the key refers. The `AUTO_INCREMENT` keyword is used to specify that the primary key column should automatically increment for each new row.


### Insert data

Then populate the tables with this script : 

```sql
-- insert 10 rows into jobs table
INSERT INTO jobs (job_id, job_title, min_salary, max_salary)
VALUES
  (1, 'Manager', 70000, 120000),
  (2, 'Salesperson', 20000, 40000),
  (3, 'Developer', 50000, 100000),
  (4, 'Accountant', 35000, 60000),
  (5, 'HR Manager', 45000, 80000),
  (6, 'Marketing Specialist', 40000, 75000),
  (7, 'Administrative Assistant', 25000, 35000),
  (8, 'Designer', 45000, 80000),
  (9, 'Writer', 30000, 50000),
  (10,'Engineer', 55000, 90000);
  
-- insert 10 rows into location table
INSERT INTO locations (location_id, city, state, country)
VALUES
  (1, 'New York', 'NY', 'USA'),
  (2, 'Los Angeles', 'CA', 'USA'),
  (3, 'San Francisco', 'CA', 'USA'),
  (4, 'Chicago', 'IL', 'USA'),
  (5, 'Houston', 'TX', 'USA'),
  (6, 'London', NULL, 'England'),
  (7, 'Paris', NULL, 'France'),
  (8, 'Berlin', NULL, 'Germany'),
  (9, 'Sydney', NULL, 'Australia'),
  (10, 'Tokyo', NULL, 'Japan');

-- insert 5 rows into departments table
INSERT INTO departments (department_id, department_name, location_id)
VALUES
(1, 'Engineering', 1),
(2, 'Sales', 2),
(3, 'Administration', 2),
(4, 'Marketing', 3),
(5, 'Data pole', 1);

-- Insert 10 employees
INSERT INTO employees ( employee_id, first_name, last_name, email, phone_number, hire_date, job_id, salary, department_id)
VALUES
  (1, 'John', 'Doe', 'johndoe@example.com', '555-555-1234', '2022-01-01', 1, 50000, 1),
  (2, 'Jane', 'Doe', 'janedoe@example.com', '555-555-5678', '2022-01-01', 2, 60000, 1),
  (3, 'Bob', 'Smith', 'bobsmith@example.com', '555-555-9012', '2022-02-01', 3, 75000, 2),
  (4, 'Alice', 'Johnson', 'alicejohnson@example.com', '555-555-3456', '2022-02-01', 4, 85000, 2),
  (5, 'Mark', 'Lee', 'marklee@example.com', '555-555-7890', '2022-03-01', 5, 95000, 3),
  (6, 'Emily', 'Chen', 'emilychen@example.com', '555-555-2345', '2022-03-01', 5, 80000, 3),
  (7, 'Sara', 'Kim', 'sarakim@example.com', '555-555-6789', '2022-04-01', 6, 70000, 4),
  (8, 'Michael', 'Wu', 'michaelwu@example.com', '555-555-0123', '2022-04-01', 7, 65000, 4),
  (9, 'David', 'Nguyen', 'davidnguyen@example.com', '555-555-4567', '2022-05-01', 8, 55000, 5),
  (10, 'Jennifer', 'Garcia', 'jennifergarcia@example.com', '555-555-8901', '2022-05-01', 9, 60000, 5);


-- Insert 4 projects
INSERT INTO projects (project_id, project_name, start_date, end_date, estimated_cost)
VALUES
(1, 'Website Redesign', '2022-01-01', '2022-06-30', 50000),
(2, 'Sales Campaign', '2022-02-01', '2022-04-30', 120000),
(3, 'Database Migration', '2022-03-01', '2022-08-31', 140000),
(4, 'NLP', '2022-04-01', '2022-07-01', 8000);


-- insert 10 rows into department_projects table
INSERT INTO department_projects (department_id, project_id)
VALUES
  (1, 1),
  (1, 2),
  (2, 1),
  (2, 3),
  (3, 2),
  (3, 3),
  (4, 1),
  (4, 2),
  (5, 1),
  (5, 3);


-- Insert 10 rows into the employee_projects table
INSERT INTO employee_projects (employee_id, project_id)
VALUES (1, 1),
       (1, 2),
       (2, 1),
       (2, 3),
       (3, 2),
       (3, 3),
       (4, 2),
       (4, 1),
       (5, 3),
       (5, 1);
```
## Tests some queries for verification --> TO TEST 
Let's take a look to ten example queries to verify the data in the seven tables:

* Retrieve all employees who work in the "Sales" department:
```
SELECT e.first_name, e.last_name, d.department_name
FROM employees e
JOIN departments d ON e.department_id = d.department_id
WHERE d.department_name = 'Sales';
```
* Retrieve all projects that are assigned to the "Marketing" department:
```
SELECT p.project_name, d.department_name
FROM projects p
JOIN department_projects dp ON p.project_id = dp.project_id
JOIN departments d ON dp.department_id = d.department_id
WHERE d.department_name = 'Marketing';
```
* Retrieve all projects that have an estimated cost greater than $100,000:
```
SELECT project_name, estimated_cost
FROM projects
WHERE estimated_cost > 100000;
```
* Retrieve all employees who are working on the "Database Migration":
```
SELECT e.first_name, e.last_name, p.project_name
FROM employees e
JOIN employee_projects ep ON e.employee_id = ep.employee_id
JOIN projects p ON ep.project_id = p.project_id
WHERE p.project_name = 'Database Migration';
```
* Retrieve all job titles and the number of employees who hold each job title:
```
SELECT j.job_title, COUNT(*) AS num_employees
FROM employees e
JOIN jobs j ON e.job_id = j.job_id
GROUP BY j.job_title;
```
* List all employees and their department:
```
SELECT e.employee_id, e.first_name, e.last_name, d.department_name 
FROM employees e 
INNER JOIN departments d ON e.department_id = d.department_id;
```
* List all departments and their location:
```
SELECT d.department_name, l.city, l.state 
FROM departments d 
INNER JOIN locations l ON d.location_id = l.location_id;
```
* List all projects and their department:
```
SELECT p.project_id, p.project_name, d.department_name 
FROM projects p 
INNER JOIN department_projects dp ON p.project_id = dp.project_id 
INNER JOIN departments d ON dp.department_id = d.department_id;
```
* List all employees and the projects they are working on:
```
SELECT e.first_name, e.last_name, p.project_name 
FROM employees e 
INNER JOIN employee_projects ep ON e.employee_id = ep.employee_id 
INNER JOIN projects p ON ep.project_id = p.project_id;
```
* List all employees, their job title, and salary:
```
SELECT e.first_name, e.last_name, j.job_title, e.salary 
FROM employees e 
INNER JOIN jobs j ON e.job_id = j.job_id;
```


## The importance of schema and organization

Creating a schema and diagrams for a database is critical, especially when dealing with large databases with many tables and relationships. Without proper organization and documentation, it can be challenging to understand the structure and relationships between different tables. 

<br />

This is particularly true when many people are working on the database or when there is a lot of data being added and updated regularly. Having a clear schema and diagrams can help developers and users understand the structure and relationships of the data, leading to more efficient and effective use of the database. Additionally, it can help to identify and prevent errors in the data or in the database design itself. Overall, investing time in creating a clear schema and diagrams can save time and resources in the long run and make the database easier to manage and use.


## Wrap-up 

* In this project, we learned how to create a company database using MySQL.
* We created 7 tables: employees, departments, projects, department_projects, employee_projects, jobs, and location.
* We added primary keys to all tables with auto-increment options for unique identification and added foreign keys to establish relationships between tables.
* We inserted data into each table and test some queries.
* We also learned about the importance of schema and diagrams for databases, especially as the number of tables and relationships grows, and the significance of foreign keys in ensuring data integrity and consistency.



