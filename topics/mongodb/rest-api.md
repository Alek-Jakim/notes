### Setting up Mongoose

Mongoose makes it easy to model and
manage your application data. This includes data sanitization, data validation, and more.
Mongoose will serve as a replacement for the native driver, providing for a more object-oriented interface.

```bash
npm i mongoose
```

```javascript
const mongoose = require('mongoose');

mongoose.connect('mongodb://127.0.0.1:27017/task-manager-api', {
useNewUrlParser: true,
useCreateIndex: true
})
```

### Defining a model

The model definition is where you define what makes up a user. This would include all the pieces of data you want to store in the database.

```javascript
const User = mongoose.model('User', 
{
    name: {
    type: String
},
    age: {
    type: Number
}
})


const me = new User({
name: 'Alek',
age: 26
})

//The new model instance can be saved to the database using the save method.

me.save().then(() => {
console.log(me)
}).catch((error) => {
console.log('Error!', error)
})
```

### Data Validation and Sanitization

The validator library provides useful methods for validating data such as email addresses,
phone numbers, zip codes, and more...

```bash
npm i validator
```

```javascript
const mongoose = require('mongoose')
const validator = require('validator')
const User = mongoose.model('User', {
name: {
type: String,
required: true,
trim: true
},
email: {
type: String,
required: true,
trim: true,
lowercase: true,
validate(value) {
if (!validator.isEmail(value)) {
throw new Error('Email is invalid')
}
}
}
})
```

### REST API

An API is an application programming interface. It is a set of rules that allow programs to talk to each other. The developer creates the API on the server and allows the client to talk to it.

REST determines how the API looks like. It stands for “Representational State Transfer”. It is a set of rules that developers follow when they create their API. One of these rules states that you should be able to get a piece of data (called a resource) when you link to a specific URL.

It’s important to know that a request is made up of four things:

* The endpoint (root-endpoint/?)

* The method

* The headers

* The data (or body)

The root-endpoint is the starting point of the API you’re requesting from. The root-endpoint of Github’s API is `https://api.github.com` while the root-endpoint Twitter’s API is `https://api.twitter.com`.

The path determines the resource you’re requesting for. Think of it like an automatic answering machine that asks you to press 1 for a service, press 2 for another service, 3 for yet another service and so on.

![](rest.png)

### Resource Creation Endpoints

Resource creation endpoints use the POST HTTP method. The URL structure is
`/resources`. If you wanted to create a user, it would be `POST /users`. If you wanted to
create a task, it would be `POST /tasks`.

The code below uses `app.post` to set up a POST request handler for `/users`. The handler
function creates a new instance of the user model and saves it to the database.

`express.json` is also setup to parse incoming JSON into a JavaScript object which you
can access on `req.body`.

```javascript
app.use(express.json())
app.post('/users', (req, res) => {
const user = new User(req.body)
user.save().then(() => {
res.status(201).send(user)
}).catch((e) => {
res.status(400).send(e)
})
})
```


### Resource Reading Endpoint

Resource reading endpoints use the GET HTTP method. The URL structure is `/resources`
for a list of resources and `/resources/:id` for fetching an individual resource by its ID. If
you wanted to fetch all your tasks, it would be `GET /tasks`. If you wanted to fetch an
individual task with the ID of 198, it would be `GET /tasks/198`.

The code below uses `app.get` to set up a GET request handler for `/users/:id`. `:id` serves
as a placeholder for the ID of the user to fetch. If the request is `GET /users/321`, then the
ID will be 321. This is known as a URL parameter, and you can access the value for URL
parameters on `req.params`.

```javascript
app.get('/users/:id', (req, res) => {
const _id = req.params.id // Access the id provided
User.findById(_id).then((user) => {
if (!user) {
return res.status(404).send()
}
res.send(user)
}).catch((e) => {
res.status(500).send()
})
})
```

```javascript
app.get('/users', (req, res) => {
    User.find({})
        .then((users) => {
            res.send(users)
        })
        .catch((e) => {
            res.status(500).send()
        })
})
```