# PostgreSQL

## What is PostgreSQL

PostgreSQL is an object-relational database management system (ORDBMS) based on POSTGRES, Version 4.2, developed at the University of California at Berkeley Computer Science Department. POSTGRES pioneered many concepts that only became available in some commercial database systems much later.

PostgreSQL is an open-source descendant of this original Berkeley code. It supports a large part of the SQL standard and offers many modern features:

* complex queries

* foreign keys

* triggers

* updatable views

* transactional integrity

* multiversion concurrency control

Also, PostgreSQL can be extended by the user in many ways, for example by adding new: 

* data types

* functions

* operators

* aggregate functions

* index methods

* procedural languages
---
## Architectural Fundamentals

In database jargon, PostgreSQL uses a **client/server model**. A PostgreSQL session consists of the following cooperating processes (programs):

* A server process, which manages the database files, accepts connections to the database from client applications, and performs database actions on behalf of the clients. The database server program is called postgres.

* The user's client (frontend) application that wants to perform database operations. Client applications can be very diverse in nature: a client could be a text-oriented tool, a graphical application, a web server that accesses the database to display web pages, or a specialized database maintenance tool. Some client applications are supplied with the PostgreSQL distribution; most are developed by users.

As is typical of client/server applications, the client and the server can be on different hosts. In that case they communicate over a TCP/IP network connection. You should keep this in mind, because the files that can be accessed on a client machine might not be accessible (or might only be accessible using a different file name) on the database server machine.

The PostgreSQL server can handle multiple concurrent connections from clients. To achieve this it starts (“forks”) a new process for each connection. From that point on, the client and the new server process communicate without intervention by the original postgres process. Thus, the master server process is always running, waiting for client connections, whereas client and associated server processes come and go. (All of this is of course invisible to the user.)

---
## Creating a database

### How To Install and Use PostgreSQL on Ubuntu


```bash
$ sudo apt update  

$ sudo apt install postgresql postgresql-contrib
```
### Switching Over to the postgres Account

```bash
sudo -u postgres psql -p 5432 -h 127.0.0.1
```

### Use a specific database

```sql

/*
-h is for Host
-p is for port and 5432 is the default one
-u is for User
Then you enter your password for the specified user
test - the name of my db
*/

psql -h localhost -p 5432 -U postgres test
```

### Exit the database

```sql
\q
```


### List all databases:

```sql
$\l
```

### Switch between databases

```sql
\c dbname
```
---

[Basic Commands](./basic.md)