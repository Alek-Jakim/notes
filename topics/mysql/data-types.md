## Data Types

SQL data types can be broadly divided into following categories: 

* Numeric data types such as int, tinyint, bigint, float, real etc.

* Date and Time data types such as Date, Time, Datetime etc.

* Character and String data types such as char, varchar, text etc.

* Unicode character string data types, for example nchar, nvarchar, ntext etc.

* Binary data types such as binary, varbinary etc.

* Miscellaneous data types – clob, blob, xml, cursor, table etc.


![](sql-data-types.png)

### Char and Varchar

VARCHAR is variable length, while CHAR is fixed length. CHAR is a fixed length string data type, so any remaining space in the field is padded with blanks. CHAR takes up 1 byte per character. ... VARCHAR is a variable length string data type, so it holds only the characters you assign to it.

Char is faster for fixed length text.

### Decimals

```sql
decimal [(p [,s])]

# p stands for Precision, the total number of digits in the value, i.e. on both sides of the decimal point

# s stands for Scale, number of digits after the decimal point

# Example
INSERT INTO shop(item, price) VALUES('goat', 252.33);

```


### Float and Double

Float data can hold 8 bytes, or 15 places after the decimal point. Double data is similar to float, except that it allows for much larger numbers. They're used to specify precision, that is the number of whole numbers and number of digits shown after the decimal point of a complex number.


### Date, Time and Datetime

* The DATE type is used for values with a date part but no time part. MySQL retrieves and displays DATE values in 'YYYY-MM-DD' format. The supported range is '1000-01-01' to '9999-12-31'.

* The DATETIME type is used for values that contain both date and time parts. MySQL retrieves and displays DATETIME values in 'YYYY-MM-DD hh:mm:ss' format. The supported range is '1000-01-01 00:00:00' to '9999-12-31 23:59:59'.

* MySQL retrieves and displays TIME values in 'hh:mm:ss' format (or 'hhh:mm:ss' format for large hours values). TIME values may range from '-838:59:59' to '838:59:59'. The hours part may be so large because the TIME type can be used not only to represent a time of day (which must be less than 24 hours), but also elapsed time or a time interval between two events (which may be much greater than 24 hours, or even negative).

### Currdate, Curtime and Now

* `CURDATE()` - Returns the current date as a value in 'YYYY-MM-DD' or YYYYMMDD format, depending on whether the function is used in string or numeric context.

```sql
SELECT CURRDATE();
```

* `CURTIME()` - Returns the current time as a value in 'hh:mm:ss' or hhmmss format, depending on whether the function is used in string or numeric context. The value is expressed in the session time zone.

```sql
SELECT CURRTIME();
```

* `NOW()` returns a constant time that indicates the time at which the statement began to execute. (Within a stored function or trigger, NOW() returns the time at which the function or triggering statement began to execute.) This differs from the behavior for SYSDATE(), which returns the exact time at which it executes

```sql
SELECT NOW();

INSERT INTO people(name, birthdate, birthtime, birthdt)
    -> VALUES('Myself', CURDATE(), CURTIME(), NOW());
```

### Formating Dates

```sql
# Selects the days
SELECT name, DAY(birthdate) FROM people;

# Gives you the day of the week; ex: Friday, Saturday etc
SELECT name, DAYNAME(birthdate) FROM people;
```

* **USEFUL**  - `DATE_FORMAT(date,format)` - Formats the date value according to the format string.

```sql
SELECT CONCAT(name, ' ', DATE_FORMAT(birthdt, 'Was born on a %W')) FROM
people;

SELECT DATE_FORMAT('1993-11-20 22:23:00', '%W %M %Y');
```

### Date Math

* DATEDIFF() - The MySQL DATEDIFF function returns the difference in days between two date values.

```sql
SELECT CONCAT(name, ' has been alive for ',DATEDIFF(NOW(), birthdate), ' days.') FROM people;
```

* DATE_ADD() & DATE_SUB() - These functions perform date arithmetic. 

```sql
DATE_ADD(date,INTERVAL expr unit)DATE_SUB(date,INTERVAL expr unit)
```

```sql
SELECT birthdt, birthdt + INTERVAL 15 MONTH + INTERVAL 10 HOUR FROM people;
```


### Timestamps

* The TIMESTAMP data type is used for values that contain both date and time parts. TIMESTAMP has a range of '1970-01-01 00:00:01' UTC to '2038-01-19 03:14:07' UTC. **This** is important and is the main difference between TIMESTAMP and DATETIME. **USE DATETIME FOR EVERYTHING** except for the following case:

```sql
CREATE TABLE comments (
    content VARCHAR(100),
    created_at TIMESTAMP DEFAULT NOW()
);


CREATE TABLE comments2 (
    content VARCHAR(100),
    changed_at TIMESTAMP DEFAULT NOW() ON UPDATE CURRENT_TIMESTAMP
);
```