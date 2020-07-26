## String Functions

A string function is a function that takes a string value as an input regardless of the data type of the returned value. In SQL Server, there are many built-in string functions that can be used by developers.

Order is important when dealing with combining/wrapping certain string functions.

```sql
--This Works
SELECT UPPER(CONCAT(author_fname, ' ', author_lname)) AS "full name in caps"
FROM books;


--While this does not...
SELECT CONCAT(UPPER(author_fname, ' ', author_lname)) AS "full name in caps" 
FROM books;
```

* Running SQL files

   * Make sure you cd into the right directory before running the command.

```sql
SOURCE filename.sql;
```

### Concat

`CONCAT()` is a scalar SQL string function that takes multiple strings as input and returns on the string after concatenating all inputs. This function can take a maximum 254 of inputs.

```sql
SELECT CONCAT('Hello',' World');
-- Hello World
```

You can combine it with `SELECT`:

```sql
SELECT
  CONCAT(author_fname, ' ', author_lname)
  AS 'full name'
FROM books;

SELECT
  author_fname AS first,
  author_lname AS 'last',
  CONCAT(author_fname, ' ', author_lname) AS 'full'
FROM books;
```


### Substring

The SUBSTRING() function extracts some characters from a string.

```sql
SELECT SUBSTRING('Hello World', 1, 4);
-- Hell

SELECT CONCAT
    (
        SUBSTRING(title, 1, 10),
        '...'
    ) AS 'short title'
FROM books;
```


### Replace

Replaces all occurrences of a specified string value with another string value.

`REPLACE ( string_expression , string_pattern , string_replacement )  `

```sql
SELECT REPLACE('Hello World', 'Hell', '%$#@');
-- %$#@o World
``` 


### Reverse

Returns the reverse order of a string value.

`REVERSE ( string_expression )`

```sql
SELECT REVERSE('TCEPSER');
-- RESPECT
```

### Char_Length

The `CHAR_LENGTH()` function returns the length of a string (in bytes).

```sql
SELECT CHAR_LENGTH('Hello World') AS 'String Length';
-- 11
```

### Upper and Lower

* Returns a character expression with lowercase character data converted to uppercase.

* Returns a character expression after converting uppercase character data to lowercase.

```sql
SELECT UPPER('Hello World');
-- HELLO WORLD
SELECT LOWER('Hello World');
-- hello world
```