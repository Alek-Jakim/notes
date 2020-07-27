### Distinct 

* SELECT DISTINCT returns only distinct (i.e. different) values.

* SELECT DISTINCT eliminates duplicate records from the results.

```sql
SELECT DISTINCT CONCAT(author_fname,' ', author_lname) FROM books;
 
SELECT DISTINCT author_fname, author_lname FROM books;
```

### Order By

The ORDER BY statement in sql is used to sort the fetched data in either ascending or descending according to one or more columns.

* By default ORDER BY sorts the data in ascending order.

* We can use the keyword DESC to sort the data in descending order and the keyword ASC to sort in ascending order.

```sql

SELECT released_year FROM books ORDER BY released_year DESC;
 
SELECT released_year FROM books ORDER BY released_year ASC;

SELECT author_fname, author_lname FROM books 
ORDER BY author_lname, author_fname; 
--This will make sure if there are authors with same last names, it will sort them by their first name alphabetically (probably spelled that wrong)
```


### Limit 

The SQL SELECT LIMIT statement is used to retrieve records from one or more tables in a database and limit the number of records returned based on a limit value.

```sql
SELECT title FROM books LIMIT 3;
 
SELECT title FROM books LIMIT 1;


SELECT title, released_year FROM books 
ORDER BY released_year DESC LIMIT 0,5;
--returns results from 0 index to 5 index

SELECT * FROM tbl LIMIT 95,18446744073709551615;
-- it will select from the 95th until the end of the table since the number is much greater than the actual data
```


### Like 

The LIKE operator is used in a WHERE clause to search for a specified pattern in a column.

There are two wildcards often used in conjunction with the LIKE operator:

* % - The percent sign represents zero, one, or multiple characters

* _ - The underscore represents a single character


```sql
-- This gives results only STARTING with da...
SELECT title, author_fname FROM books WHERE author_fname LIKE 'da%';

--This will give results wherever the 'da' is...
SELECT title, author_fname FROM books WHERE author_fname LIKE '%da%';

-- Books that have 'the' in the title
SELECT title FROM books WHERE title LIKE '%the%';
```

```sql
-- it gives us titles with % in it (\ is an escape character)
SELECT title FROM books WHERE title LIKE '%\%%'


-- it gives us titles with _ in it (\ is an escape character)
SELECT title FROM books WHERE title LIKE '%\_%'
```