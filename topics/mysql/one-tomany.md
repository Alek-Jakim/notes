## One-to-many relationships

In a one-to-many relationship, one record in a table can be associated with one or more records in another table. For example, each customer can have many sales orders.

This is the most commonly used type of relationship. Consider an e-commerce website, with the following:

* Customers can make many orders.

* Orders can contain many items.

* Items can have descriptions in many languages.

In these cases we would need to create "One to Many" relationships. Here is an example:

![](https://cdn.tutsplus.com/net/uploads/legacy/538_sql3/ss_3.png)

Each customer may have zero, one or multiple orders. But an order can belong to only one customer.

---

When selecting data from multiple tables with relationships, we will be using the JOIN query. There are several types of JOIN's: 

* Cross Joins

* Natural Joins

* Inner Joins

* Left(Outer) Joins

* Right(Outer) Joins

---
1. Implicit Inner Join
```bash
SELECT * FROM customers, orders 
WHERE customers.id = orders.customer_id;

SELECT first_name, last_name, order_date, amount
FROM customers, orders 
    WHERE customers.id = orders.customer_id;
```

2. Explicit Inner Joins

```bash
SELECT * FROM customers
JOIN orders
    ON customers.id = orders.customer_id;

SELECT first_name, last_name, order_date, amount 
FROM customers
JOIN orders
    ON customers.id = orders.customer_id;
```