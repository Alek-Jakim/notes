## MySQL

--------------

### **Best Practices**

#### Naming Convention

* Singular form. Both tables and columns.

* Be consistent! Doesn't matter if you use camelCase or snake_case. Use whatever the front-end uses.

* Avoid abbreviations or prefixes.

* Use unique names that cannot collude with SQL/RDBMS reserved words (avoid name, order, percent...) or use a trailing underscore.

* Do not use the table name followd by “id” (e.g. client_id) as your PK. id is more than enough and everyone will understand.

* Never use capital letters in your table or field names. Ever.


#### Performance

* Always foreign key to IDs, rather than column values.

* Try to stick to `where` clauses on indexed columns, instead of `like`. 

* Don't go crazy with `joins`.

* Don't use varchar(255). Try to use the lowest number possible.


## Install MySQL
-----

```bash
sudo apt install mysql-server

sudo mysql_secure_installation
# Change root password to more secure.
# Remove anonymous users.
# Disable remote root login. Root should only connect via `localhost`.
# Remove test database and access to it.
# Reload privilege tables.

sudo /etc/init.d/mysql start
# sudo service mysql start
# systemctl restart mysql
```


#### Remove MySQL

```bash
sudo apt remove --purge mysql*
sudo apt purge mysql*
sudo apt autoremove
sudo apt autoclean
sudo apt remove dbconfig-mysql
```


## Status 
```bash
sudo systemctl status mysql
sudo systemctl start mysql

sudo /etc/init.d/mysql status
sudo /etc/init.d/mysql start
```

## Login 

```bash
# Log into MySQL as root, with password. 
sudo mysql -u root -p
```

**Note:** Commands are not case sensitive, but table names are. All commands must end with `;`.

`;` - Execute/End current command.
`ENTER` - Starts a new line. `;` is expected.




# Syntax

#### Starting CLI

```sql
mysql-ctl cli
```
## Database: 
```sql
SHOW DATABASES;              -- List databases.
SELECT database();           -- Show current database.
USE dbName;                 -- Select a database.

CREATE DATABASE dbName;     -- Create a database.
DROP DATABASE dbName;       -- Delete a database.
```

## Tables: 

```sql
SHOW TABLES;                 -- List all tables.
DESCRIBE tableName;         -- Display columns and types.

-- Shows the query that creates the table.
SHOW CREATE TABLE tableName;

-- Create a table.
CREATE TABLE tableName (column1 DATATYPE, column2 DATATYPE);

-- Example
CREATE TABLE user (
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT, -- Important
    name VARCHAR(255),
    pass VARCHAR(255)
);
```

