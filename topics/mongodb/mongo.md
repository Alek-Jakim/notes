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
MongoClient.connect(connectionURL, { useNewUrlParser: true, useUnifiedTopology: true }, (error, client)
=> {
if (error) {
return console.log('Unable to connect to database!')
}
const db = client.db(databaseName)
// Start to interact with the database
})
```

[Node.js MondoDB Driver API](https://mongodb.github.io/node-mongodb-native/2.0/api/)

#### Object ID

MongoDB uses ObjectIDs to create unique
identifiers for all the documents in the database. It’s different than the traditional autoincrementing
integer ID, but it comes with its own set of advantages.

MongoDB provides ObjectID which can be used to generate new ObjectIDs. The
example below generates a new ID and prints it to the console:

```javascript
const { MongoClient, ObjectID } = require('mongodb')
const id = new ObjectID()
console.log(id) // Print new id to the console
```

An ObjectID is a GUID (Globally Unique Identifier). GUIDs are generated randomly via an
algorithm to ensure uniqueness. These IDs can be generated on the server, but as seen in
the snippet above, they can be generated on the client as well. That means a client can
generate the ID for a document it’s about to insert in to the database.

----
#### **CREATE**
```javascript
// insertOne
const db = client.db(databaseName)

db.collection('users').insertOne({
    name: 'Alek',
    age: 26
}, (err, res) => {
    if(err) {
        return console.log(err)
    }
    console.log(res.ops)
})

//insertMany
db.collection('tasks').insertMany([
    {
        description: 'Task One',
        completed: true
    },
    {
        description: 'Task Two',
        completed: false
    }
], (err, res) => {
    if(err) {
        return console.log(err)
    }
    console.log(res.ops)
})
```

#### **READ**

You can search for documents in a given collection using find or findOne. find can be
used to fetch multiple documents, while findOne can be used to fetch a single document.

The example below uses find to search for documents in the tasks collection. You can
provide an object as the first argument to find to filter the documents. The example below
sets completed equal to false to fetch only those tasks that haven’t been completed.

```javascript
db.collection('tasks').find({ completed: false }).toArray((error, tasks) => {
console.log(tasks)
})
```

The next example uses findOne to find a single document by its ID. In this case, it’s
necessary to pass the string version of the ID to the ObjectID constructor function to
convert it to an ObjectID.

```javascript
db.collection('tasks').findOne({ _id: new
ObjectID("5c0fec243ef6bdfbe1d62e2f") }, (error, task) => {
console.log(task)
})
```

Documentation:
* [find](http://mongodb.github.io/node-mongodb-native/3.1/api/Collection.html#find)
* [findOne](http://mongodb.github.io/node-mongodb-native/3.1/api/Collection.html#findOne)