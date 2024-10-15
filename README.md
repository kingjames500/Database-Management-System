# Database Management  System
 I'm going to discuss and demonstrate how Joins work in SQL

#### ***TYPES OF SQL JOINS STATEMENTS***

The SQL JOIN statement is used to combine rows from two tables based on a common column and selects records that have matching values in these columns.

### 1. Inner Join
The SQL ***INNER JOIN*** statement joins two tables based on a common column and selects rows that have matching values in these columns. <br>


```sql
-- join Customers and Orders tables based on 
-- customer_id of Customers and customer column of Orders

select customer.id, customer.last_name, orders.order_date, orders.total_amount
from customer
join orders
on customer.id = orders.customer_id;
```
The  sql code above will output the above results on the image below.

![inner join statement results joining table customers and orders](./images/inner%20join%20images..png)

### Here, <br>



### 2. Left Join.



