### Logical Operators

In SQL, all logical operators evaluate to TRUE, FALSE, or NULL (UNKNOWN). In MySQL, these are implemented as 1 (TRUE), 0 (FALSE), and NULL. For example:

```sql
SELECT 99 > 1; # Returns 1 (true)

SELECT 1 > 99 # Returns 0 (false)

100 > 5
-- true
 
-15 > 15
-- false
 
9 > -10
-- true
 
1 > 1
-- false
 
'a' > 'b'
-- false
 
'A' > 'a'
-- false
 
'A' >=  'a'
-- true
```

#### Not Equal

```sql
SELECT title FROM books WHERE released_year != 2017;

SELECT title, author_lname FROM books WHERE author_lname != 'Harris';
```

#### Not Like
---
```sql
 SELECT title FROM books WHERE title LIKE 'W%';
```

* Greater Than
---
```sql
SELECT title FROM books WHERE title NOT LIKE 'W%';

SELECT title, released_year FROM books WHERE released_year >= 2005;

SELECT title, stock_quantity FROM books WHERE stock_quantity > 100;
```
#### Less Than
---
```sql
SELECT title, released_year FROM books
WHERE released_year < 2000;
 
SELECT title, released_year FROM books
WHERE released_year <= 2000;

SELECT 3 < -10;
-- false
 
SELECT -10 < -9;
-- true
 
SELECT 42 <= 42;
-- true
 
SELECT 'h' < 'p';
-- true
 
SELECT 'Q' <= 'q';
-- true
```

#### Logical AND
---
Logical AND. Evaluates to 1 if all operands are nonzero and not NULL, to 0 if one or more operands are 0, otherwise NULL is returned.

**Note:** The && operator is deprecated and support for it will be removed in a future MySQL version. Applications should be adjusted to use the standard SQL AND operator.

```sql
SELECT title FROM books WHERE author_lname="Eggers" && released_year > 2010;

SELECT 1 < 5 && 7 = 9;
-- false
 
SELECT -10 > -20 && 0 <= 0;
-- true
 
SELECT -40 <= 0 AND 10 > 40;
--false
 
SELECT 54 <= 54 && 'a' = 'A';
-- true
 
SELECT * 
FROM books
WHERE author_lname='Eggers' 
    AND released_year > 2010 
    AND title LIKE '%novel%';
```

#### Logical OR
---
Logical OR. When both operands are non-NULL, the result is 1 if any operand is nonzero, and 0 otherwise. With a NULL operand, the result is 1 if the other operand is nonzero, and NULL otherwise. If both operands are NULL, the result is NULL.

**Note:** As of MySQL 8.0.17, the || operator is deprecated. In newer versions of MySQL (8.0.17 and newer) you will need to replace || with OR.



#### Between
---
```sql
SELECT title, released_year FROM books WHERE released_year >= 2003 AND released_year <= 2013;

# The same can be accomplished like this: 

SELECT title, released_year FROM books WHERE released_year BETWEEN 2003 AND 2013;

# Not Between
SELECT title, released_year FROM books WHERE released_year NOT BETWEEN 2000 AND 2010;



SELECT name, birthdt FROM people WHERE birthdt BETWEEN '1980-01-01' AND '2000-01-01';
 
SELECT 
    name, 
    birthdt 
FROM people
WHERE 
    birthdt BETWEEN CAST('1980-01-01' AS DATETIME)
    AND CAST('2000-01-01' AS DATETIME);
```