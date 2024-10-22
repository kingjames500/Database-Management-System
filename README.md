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

The SQL ***FULL JOIN*** statement joins two tables based on a common column. It selects records that have matching values in these columns and the remaining rows from both of the tables.

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

 - ***Scenario***: A retail store updates its inventory when a purchase is made. If a customer buys the last item in stock, the inventory should reflect that change.
 - ***Importance***: If the database allows for inconsistent states (e.g., showing an item as available when it is not), it could lead to overselling, customer dissatisfaction, and financial loss. Consistency ensures that all transactions lead to a valid state.

### 3. Isolation

Each transaction is isolated from the other transactions to prevent data conflicts. This also helps database operations in relation to managing multiple entries and multi-level transactions. For example, if two users are trying to modify the same data (or even the same transaction), the DBMS uses a mechanism called a lock manager to suspend other users until the changes being made by the first user are complete.

<h4>
        <span style="color:yellow">
        Example about Isolation
        </span>
</h4>

  -  Suppose you and your friend are booking a train ticket for Delhi. While you check the number of seats available you find there is only a single seat available,your friend also sees the same thing from his IRCTC app. Now, if both of you simultaneously start booking the train seat, that should not be allowed by the database management system, else either of you will land in trouble. May be both will end up booking for the same seat, or may be both will pay but only one will have the seat confirmed.

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
 -  Normalization is the process to eliminate data redundancy and enhance data integrity in the table. Normalization also helps to organize the data in the database. It is a multi-step process that sets the data into tabular form and removes the duplicated data from the relational tables.

 - Normalization organizes the columns and tables of a database to ensure that database integrity constraints properly execute their dependencies. It is a systematic technique of decomposing tables to eliminate data redundancy (repetition) and undesirable characteristics like Insertion, Update, and Deletion anomalies.

 <h3>
 1.
        <span style="color:yellow">
       1st Normal Form (1NF)
        </span>
</h3>

 -  A table is referred to as being in its First Normal Form if atomicity of the table is 1.

 - Here, atomicity states that a single cell cannot hold multiple values. It must hold only a single-valued attribute.

- The First normal form disallows the multi-valued attribute, composite attribute, and their combinations.


<h3>
 2.
        <span style="color:yellow">
       Second Normal Form (2NF)
        </span>
</h3>

- The first condition for the table to be in Second Normal Form is that the table has to be in First Normal Form. 
- The table should not possess partial dependency. 
- The partial dependency here means the proper subset of the candidate key should give a non-prime attribute.




