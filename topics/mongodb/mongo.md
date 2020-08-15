## NoSQL
 
NoSQL databases (aka "not only SQL") are non tabular, and store data differently than relational tables. NoSQL databases come in a variety of types based on their data model. The main types are document, key-value, wide-column, and graph. They provide flexible schemas and scale easily with large amounts of data and high user loads.

When people use the term “NoSQL database”, they typically use it to refer to any non-relational database. Some say the term “NoSQL” stands for “non SQL” while others say it stands for “not only SQL.” Either way, most agree that NoSQL databases are databases that store data in a format other than relational tables.

A common misconception is that NoSQL databases or non-relational databases don’t store relationship data well. NoSQL databases can store relationship data—they just store it differently than relational databases do. In fact, when compared with SQL databases, many find modeling relationship data in NoSQL databases to be easier than in SQL databases, because related data doesn’t have to be split between tables.

### Installing MongoDB

Download and install MongoDB Community Server from download page. Create a “mongodb-data” directory in
your user directory to store the database data.

```bash
/c/Users/Alex/mongodb/mongo-db/bin/mongod.exe --dbpath=/c/Users/Alex/mongodb-data
```

After that, install [Robo 3T](https://robomongo.org/), which is a MongoDB admin tool that makes it easy
to manage and visualize the data in your database.

### Connecting and inserting documents

Connecting to MongoDB: MongoDB provides a native driver that allows you to connect to your database from Node.
You can grab the driver by installing the mongodb npm module as shown below.

```bash
npm i mongodb
```

After the driver is installed, you need to provide 2 pieces of info. The first is the connection URL and the
second is the name of the database.

```javascript
const mongodb = require('mongodb')
const MongoClient = mongodb.MongoClient
const connectionURL = 'mongodb://127.0.0.1:27017'
const databaseName = 'task-manager'
MongoClient.connect(connectionURL, { useNewUrlParser: true }, (error, client)
=> {
if (error) {
return console.log('Unable to connect to database!')
}
const db = client.db(databaseName)
// Start to interact with the database
})
```