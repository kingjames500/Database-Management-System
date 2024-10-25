# Database Management System

I'm going to discuss and demonstrate how Joins work in SQL

## **_TYPES OF SQL JOINS STATEMENTS_**

The SQL JOIN statement is used to combine rows from two tables based on a common column and selects records that have matching values in these columns.

### 1. Inner Join

The SQL **_INNER JOIN_** statement joins two tables based on a common column and selects rows that have matching values in these columns. <br>

```sql
-- join Customers and Orders tables based on
-- customer_id of Customers and customer column of Orders

select customer.id, customer.last_name, orders.order_date, orders.total_amount
from customer
join orders
on customer.id = orders.customer_id;
```

The sql code above will output the above results on the image below.

![inner join statement results joining table customers and orders](./images/inner%20join%20images..png)

### Here, <br>

The SQl command join the **_customers_** and **_orders_** tables. <br>
The result includes customer_id (from customer) and item (from orders) of rows where customer IDs match (Customer.id = orders.customer_id).

### 2. Left Join.

The SQL **LEFT JOIN** combines two tables based on a common column. It then selects records having matching values in these columns and the remaining rows from the left table.

```sql

-- left join Customers and Orders tables based on their shared customer_id columns
-- Customers is the left table
-- Orders is the right table

select customer.id, customer.first_name, orders.order_date
from customer
left join orders
on customer.id = orders.customer_id
;
```

![left join statement results](./images/left%20join%20images.png)

### 3. Right Join.

The SQL **RIGHT JOIN\*** statement joins two tables based on a common column. It selects records that have matching values in these columns and the remaining rows from the right table.

```sql

-- join Customers and Orders tables
-- based on their shared customer_id columns
-- Customers is the left table
-- Orders is the right table

SELECT Customers.customer_id, Customers.first_name, Orders.item
FROM Customers
RIGHT JOIN Orders
ON Customers.customer_id = Orders.customer_id;
```

![right join statement results](./images/left%20join%20images.png)

### 3. Full join.

The SQL **_FULL JOIN_** statement joins two tables based on a common column. It selects records that have matching values in these columns and the remaining rows from both of the tables.

```sql
-- full join Customers and Orders tables
-- based on their shared customer_id columns
-- Customers is the left table
-- Orders is the right table

SELECT customer.id, customer.first_name, customer.last_name, Orders.order_date
FROM customer
FULL OUTER JOIN Orders
ON customer.id = Orders.customer_id;
```

![full join statement results](./images/full%20join.png)

Here, the SQL query performs a <b>FULL JOIN</b> on two tables, <i>customers</i> and <i>Orders</i>. This means that the result set contains all the rows from both tables, including the ones that don't have common customer_id values.

## **_ACID PROPERTIES OF A DATABASE TRANSACTION_**

### 1. Atomicity

Atomicity guarantees that all of the commands that make up a transaction are treated as a single unit and either succeed or fail together. This is important in the event of a system failure or power outage, in that if a transaction wasn't completely processed, it will be discarded and the database maintains its data integrity.

<h4>
        <span style="color:yellow">
Example about Atomicity
        </span>
</h4>

- Suppose,you are transferring money from your bank account to your friend’s bank account. This transaction to transfer funds from one account to another involves making a withdrawal operation from the first account and a deposit operation on the second. If the deposit operation failed, you don’t want the withdrawal operation to happen either. Otherwise that money would disappear!

- Lumping both operations into a single atomic transaction ensures data integrity. This is what is called atomicity in DBMS. It is the property that a transaction is a single indivisible transaction. The individual operations within a transaction either all have to be performed or none will be performed. If any single operation fails then the whole transaction fails. This ensures that the databases are in a valid state at all times.

### 2. Consistency

Consistency guarantees that changes made within a transaction are populated across the database system (e.g., nodes) and in alignment with DBMS constraints. If data consistency is going to be negatively impacted by a transaction in an inconsistent state, the entire transaction will fail.

<h4>
        <span style="color:yellow">
        Example about Consistency
        </span>
</h4>

- **_Scenario_**: A retail store updates its inventory when a purchase is made. If a customer buys the last item in stock, the inventory should reflect that change.
- **_Importance_**: If the database allows for inconsistent states (e.g., showing an item as available when it is not), it could lead to overselling, customer dissatisfaction, and financial loss. Consistency ensures that all transactions lead to a valid state.

### 3. Isolation

Each transaction is isolated from the other transactions to prevent data conflicts. This also helps database operations in relation to managing multiple entries and multi-level transactions. For example, if two users are trying to modify the same data (or even the same transaction), the DBMS uses a mechanism called a lock manager to suspend other users until the changes being made by the first user are complete.

<h4>
        <span style="color:yellow">
        Example about Isolation
        </span>
</h4>

- Suppose you and your friend are booking a train ticket for Delhi. While you check the number of seats available you find there is only a single seat available,your friend also sees the same thing from his IRCTC app. Now, if both of you simultaneously start booking the train seat, that should not be allowed by the database management system, else either of you will land in trouble. May be both will end up booking for the same seat, or may be both will pay but only one will have the seat confirmed.

- Thus, the database should either perform your entire transaction first before executing your friend’s or vice-versa. So if your transaction is done first, then your friend will find available no. of seats as zero, which is absolutely okay.

- The concurrency control unit of a database management system is responsible for maintaining isolation among transactions on a database.

### 4. Durability

Durability guarantees that once the transaction completes and changes are written to the database, they are persisted. This ensures that data within the system will persist even in the case of system failures like crashes or power outages. The concept of durability is a key element in data reliability.

<h4>
        <span style="color:yellow">
       Examples of Durability
        </span>
</h4>

- Imagine you have 10 lakh amount in your bank account. The bank database server goes down, all data stored on that server is gone and so your money is gone! So you need durability, a fault free system.

- This property ensures that once the transaction has completed execution, the updates and modifications to the database are stored in and written to the disk(of the database server) and they persist permanently even if a system failure occurs.

# Database Normalization

- Normalization is the process to eliminate data redundancy and enhance data integrity in the table. Normalization also helps to organize the data in the database. It is a multi-step process that sets the data into tabular form and removes the duplicated data from the relational tables.

- Normalization organizes the columns and tables of a database to ensure that database integrity constraints properly execute their dependencies. It is a systematic technique of decomposing tables to eliminate data redundancy (repetition) and undesirable characteristics like Insertion, Update, and Deletion anomalies.

<h3>
 1.
        <span style="color:yellow">
       First Normal Form (1NF)
        </span>
</h3>

- A table is in First Normal Form (1NF) if it contains only atomic (indivisible) values. This means that each cell in the table must hold a single value, and each record needs to be unique.

**Example:**

Consider a table with the following columns: `StudentID`, `StudentName`, `Courses`.

To convert this table to 1NF:

1. Ensure that each cell contains only a single value.
2. Remove any repeating groups or arrays.

```sql
-- Original table
CREATE TABLE StudentCourses (
    StudentID INT,
    StudentName VARCHAR(100),
    Courses VARCHAR(100) -- This column contains multiple values
);

-- Convert to 1NF
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    StudentName VARCHAR(100)
);

CREATE TABLE Courses (
    StudentID INT,
    CourseName VARCHAR(100),
    PRIMARY KEY (StudentID, CourseName),
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID)
);
```

<h3>
 2.
        <span style="color:yellow">
       Second Normal Form (2NF)
        </span>
</h3>

- A table is in Second Normal Form (2NF) if it is in First Normal Form (1NF) and all non-key attributes are fully functional dependent on the primary key. This means that there should be no partial dependency of any column on the primary key.

**Example:**

Consider a table with the following columns: `StudentID`, `CourseID`, `StudentName`, `CourseName`.

To convert this table to 2NF:

1. Ensure it is in 1NF.
2. Remove partial dependencies by creating separate tables.

```sql
-- Original table
CREATE TABLE StudentCourses (
    StudentID INT,
    CourseID INT,
    StudentName VARCHAR(100),
    CourseName VARCHAR(100)
);

-- Convert to 2NF
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    StudentName VARCHAR(100)
);

CREATE TABLE Courses (
    CourseID INT PRIMARY KEY,
    CourseName VARCHAR(100)
);

CREATE TABLE StudentCourses (
    StudentID INT,
    CourseID INT,
    PRIMARY KEY (StudentID, CourseID),
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID),
    FOREIGN KEY (CourseID) REFERENCES Courses(CourseID)
);
```

<h3>
 3.
        <span style="color:yellow">
       Third Normal Form (3NF)
        </span>
</h3>

- The first condition for the table to be in Third Normal Form is that the table has to be in Second Normal Form.
- The table should not possess transitive dependency.
- Transitive dependency means that non-prime attributes should not depend on other non-prime attributes.

**Example:**

Consider a table with the following columns: `StudentID`, `StudentName`, `CourseID`, `CourseName`, `InstructorName`.

To convert this table to 3NF:

1. Ensure it is in 2NF.
2. Remove transitive dependencies by creating separate tables.

```sql
-- Original table
CREATE TABLE StudentCourses (
    StudentID INT,
    StudentName VARCHAR(100),
    CourseID INT,
    CourseName VARCHAR(100),
    InstructorName VARCHAR(100)
);

-- Convert to 3NF
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    StudentName VARCHAR(100)
);

CREATE TABLE Courses (
    CourseID INT PRIMARY KEY,
    CourseName VARCHAR(100),
    InstructorName VARCHAR(100)
);

CREATE TABLE StudentCourses (
    StudentID INT,
    CourseID INT,
    PRIMARY KEY (StudentID, CourseID),
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID),
    FOREIGN KEY (CourseID) REFERENCES Courses(CourseID)
);
```

<h3>
 4.
        <span style="color:yellow">
       Boyce-Codd Normal Form (BCNF)
        </span>
</h3>

- The first condition for the table to be in Boyce-Codd Normal Form is that the table has to be in Third Normal Form.
- For every functional dependency (X → Y), X should be a super key.

**Example:**

Consider a table with the following columns: `CourseID`, `InstructorName`, `InstructorOffice`.

To convert this table to BCNF:

1. Ensure it is in 3NF.
2. Ensure that for every functional dependency, the left side is a super key.

```sql
-- Original table
CREATE TABLE CourseInstructors (
    CourseID INT,
    InstructorName VARCHAR(100),
    InstructorOffice VARCHAR(100)
);

-- Convert to BCNF
CREATE TABLE Courses (
    CourseID INT PRIMARY KEY,
    InstructorName VARCHAR(100)
);

CREATE TABLE Instructors (
    InstructorName VARCHAR(100) PRIMARY KEY,
    InstructorOffice VARCHAR(100)
);
```

<h3>
 5.
        <span style="color:yellow">
       Fourth Normal Form (4NF)
        </span>
</h3>

- The first condition for the table to be in Fourth Normal Form is that the table has to be in Boyce-Codd Normal Form.
- The table should not have any multi-valued dependencies.

**Example:**

Consider a table with the following columns: `StudentID`, `CourseID`, `Hobby`.

To convert this table to 4NF:

1. Ensure it is in BCNF.
2. Remove multi-valued dependencies by creating separate tables.

```sql
-- Original table
CREATE TABLE StudentHobbies (
    StudentID INT,
    CourseID INT,
    Hobby VARCHAR(100)
);

-- Convert to 4NF
CREATE TABLE Students (
    StudentID INT PRIMARY KEY
);

CREATE TABLE Courses (
    CourseID INT PRIMARY KEY
);

CREATE TABLE Hobbies (
    StudentID INT,
    Hobby VARCHAR(100),
    PRIMARY KEY (StudentID, Hobby),
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID)
);

CREATE TABLE StudentCourses (
    StudentID INT,
    CourseID INT,
    PRIMARY KEY (StudentID, CourseID),
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID),
    FOREIGN KEY (CourseID) REFERENCES Courses(CourseID)
);
```

<h3>
 6.
        <span style="color:yellow">
       Fifth Normal Form (5NF)
        </span>
</h3>

- The first condition for the table to be in Fifth Normal Form is that the table has to be in Fourth Normal Form.
- The table should not have any join dependency and should be lossless.

**Example:**

Consider a table with the following columns: `ProjectID`, `EmployeeID`, `RoleID`.

To convert this table to 5NF:

1. Ensure it is in 4NF.
2. Remove join dependencies by creating separate tables.

```sql
-- Original table
CREATE TABLE ProjectAssignments (
    ProjectID INT,
    EmployeeID INT,
    RoleID INT
);

-- Convert to 5NF
CREATE TABLE Projects (
    ProjectID INT PRIMARY KEY
);

CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY
);

CREATE TABLE Roles (
    RoleID INT PRIMARY KEY
);

CREATE TABLE ProjectEmployees (
    ProjectID INT,
    EmployeeID INT,
    PRIMARY KEY (ProjectID, EmployeeID),
    FOREIGN KEY (ProjectID) REFERENCES Projects(ProjectID),
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
);

CREATE TABLE EmployeeRoles (
    EmployeeID INT,
    RoleID INT,
    PRIMARY KEY (EmployeeID, RoleID),
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID),
    FOREIGN KEY (RoleID) REFERENCES Roles(RoleID)
);
```

<h3>
 7.
        <span style="color:yellow">
       Sixth Normal Form (6NF)
        </span>
</h3>

- The first condition for the table to be in Sixth Normal Form is that the table has to be in Fifth Normal Form.
- The table should be free of any non-trivial join dependencies.

**Example:**

Consider a table with the following columns: `OrderID`, `ProductID`, `Quantity`, `Price`.

To convert this table to 6NF:

1. Ensure it is in 5NF.
2. Decompose the table to eliminate non-trivial join dependencies.

```sql
-- Original table
CREATE TABLE OrderDetails (
    OrderID INT,
    ProductID INT,
    Quantity INT,
    Price DECIMAL(10, 2)
);

-- Convert to 6NF
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY
);

CREATE TABLE Products (
    ProductID INT PRIMARY KEY
);

CREATE TABLE OrderQuantities (
    OrderID INT,
    ProductID INT,
    Quantity INT,
    PRIMARY KEY (OrderID, ProductID),
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID),
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID)
);

CREATE TABLE OrderPrices (
    OrderID INT,
    ProductID INT,
    Price DECIMAL(10, 2),
    PRIMARY KEY (OrderID, ProductID),
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID),
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID)
);
```
