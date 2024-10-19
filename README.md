# Database Management System

I'm going to discuss and demonstrate how Joins work in SQL

#### **_TYPES OF SQL JOINS STATEMENTS_**

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
