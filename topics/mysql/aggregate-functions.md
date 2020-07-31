## MySQL aggregate functions

An aggregate function performs a calculation on multiple values and returns a single value.

**Note:** Use the code below to disable strict mode
```sql
SET @@sql_mode ='';
```

1. COUNT()

* The `COUNT()` function is an aggregate function that returns the number of rows in a table. The `COUNT()` function allows you to count all rows or only rows that match a specified condition.

```sql
SELECT COUNT(DISTINCT author_fname) FROM books;

SELECT COUNT(DISTINCT author_fname, author_lname) FROM books;

SELECT COUNT(DISTINCT title) FROM books WHERE title LIKE '%the%';
```

2. GROUP BY

* The GROUP BY clause summarizes or aggregates identical data into single rows.

* Use the GROUP BY clause with aggregate functions such as SUM, AVG, MAX, MIN, and COUNT.

```sql
SELECT released_year, COUNT(*) FROM books GROUP BY released_year;

SELECT CONCAT('In ', released_year, ' ', COUNT(*), ' book(s) released') FROM books GROUP by
released_year;
```

3. MIN & MAX

* The `MAX()` function returns the largest value of the selected column.

* The `MIN()` function returns the smallest value of the selected column.

```sql
--gives you the earliest year
SELECT MIN(released_year) FROM books;

-- gives you the biggest number of pages
SELECT MAX(pages) FROM books;
```


#### Subqueries

A subquery is a query that is nested inside a SELECT , INSERT , UPDATE , or DELETE statement, or inside another subquery. A subquery can be used anywhere an expression is allowed. In this example a subquery is used as a column expression named MaxUnitPrice in a SELECT statement.

```sql
# You can do it this way however...
SELECT title, pages FROM books WHERE pages = (SELECT MAX(pages) FROM books);

#...this gives us the same result and it's faster
SELECT title, pages FROM books ORDER BY ASC LIMIT 1;
```


4. SUM

The SUM() function returns the total sum of a numeric column.

```sql
SELECT SUM(pages) AS 'total pages' FROM books;


SELECT author_fname, author_lname, SUM(pages)
    -> FROM books
    -> GROUP BY author_lname, author_fname;
```

5. AVG

The AVG() function returns the average value of a numeric column.

```sql
SELECT AVG(pages) FROM books;


SELECT released_year, AVG(stock_quantity) FROM books GROUP BY released_year;
```