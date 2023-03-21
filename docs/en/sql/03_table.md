# Tables & Keys

Tables and keys are fundamental concepts in relational database management systems. A table is a collection of related data, organized into rows and columns. Each row in a table represents a unique instance of the data, while each column represents a specific attribute or characteristic of that data.

<br />

Keys are used to uniquely identify each row in a table. A key is a column or set of columns in a table that contains values that are unique across all the rows in the table. Keys are used to enforce data integrity, to ensure that data is not duplicated or inconsistent, and to enable efficient searching and sorting of data.

<br />

In this course, we'll explore the different types of keys that can be used in MySQL, and how they can be used to create tables with well-defined relationships between them.




## Creating Tables in MySQL

Creating a table is the first step in building a database. To create a table in MySQL, we use the CREATE TABLE statement, followed by the table name and a list of columns and their data types. Here's an example of creating a simple table to store information about customers:


```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100)
);
```

This creates a table called customers with four columns: customer_id, first_name, last_name, and email. The customer_id column is defined as the primary key, which means it will contain unique values that identify each row in the table.


## Keys 

Keys are an important concept in database design. They are used to ensure data integrity and to establish relationships between tables. There are several types of keys in a database:

### Primary Key

A primary key is a column or set of columns that uniquely identifies each row in a table. The primary key is used to enforce data integrity and to ensure that there are no duplicate rows in the table. We can define a primary key using the PRIMARY KEY constraint, as shown in the example above. Here's another example, this time with a table called orders that has a composite primary key made up of two columns:

```sql
CREATE TABLE orders (
    order_id INT  PRIMARY KEY,
    customer_id INT,
    order_date DATE,
);
```
This creates a table called orders with three columns: order_id, customer_id, and order_date. The PRIMARY KEY constraint is used to define a composite primary key made up of the order_id and customer_id columns.

### Foreign Key

A foreign key is a column in one table that refers to the primary key of another table. Foreign keys are used to create relationships between tables, and to enforce referential integrity between them. In MySQL, we can define a foreign key using the FOREIGN KEY constraint.

<br />

Here's an example of creating a table called orders that has a foreign key that references the customer_id column in the customers table:

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);
```

This creates a table called orders with three columns: order_id, customer_id, and order_date. The FOREIGN KEY constraint is used to define a foreign key that references the customer_id column in the customers table.

### Unique Keys 

A unique key is a column or set of columns in a table that contains unique values, but is not the primary key. Unique keys are used to enforce data integrity, and to enable efficient searching and sorting of data. In MySQL, we can define a unique key using the UNIQUE constraint.

<br />

Here's an example of creating a table called products that has a unique key on the `product_code` column:


```sql
CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_code VARCHAR(20) UNIQUE,
    product_name VARCHAR(50),
    price DECIMAL(10,2)
);
```

This creates a table called products with four columns: product_id, product_code, product_name, and price. The product_code column is defined as a unique key using the UNIQUE constraint, which means that it will contain unique values across all the rows in the table.

### Composite Key
A composite key, also known as a composite primary key, is a primary key that consists of two or more columns in a table. In other words, it is a unique identifier made up of multiple columns. A composite key is used when a single column cannot uniquely identify each row in a table, but a combination of columns can.

<br />

For example, consider a table called orders that tracks the orders made by customers. Each order is identified by a unique order number, but a customer can make multiple orders, so the order number alone cannot uniquely identify each row in the table. Instead, we can use a composite key made up of the order number and the customer ID to uniquely identify each row:

```sql
CREATE TABLE orders (
    order_number INT,
    customer_id INT,
    order_date DATE,
    PRIMARY KEY (order_number, customer_id)
);
```

In this example, the primary key for the orders table is a composite key made up of the order_number and customer_id columns. This ensures that each row in the table is uniquely identified by a combination of these two columns. Using a composite key can improve the performance of queries that search or filter data based on a combination of columns. However, it can also make updates and deletions more complicated, since multiple columns must be taken into account.

<br />

 **PS** : A unique key is used to enforce uniqueness of data within a table, while a composite key is used to uniquely identify each row in a table.

## Conclusion

Tables and keys are essential concepts in relational database management systems, and understanding them is crucial for designing efficient and well-organized databases. In MySQL, we can use the CREATE TABLE statement to create tables with different types of keys and indexes, and enforce data integrity and relationships between tables. By using these features effectively, we can create databases that are easy to query, maintain, and scale to meet the needs of any application.