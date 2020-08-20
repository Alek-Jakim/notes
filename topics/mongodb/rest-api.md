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

### Resource Updating Endpoints

Resource updating endpoints use the PATCH HTTP method. The URL structure is `/resources/:id` for updating an individual resource by its ID. If you want to update an
individual task with the ID of 44, it would be `PATCH /tasks/44`.

`app.patch` is used to set up the Express route handler.

```javascript
app.patch('/users/:id', async (req, res) => {
    // Route handler code here
})
```


When working with updates, it’s a good idea to alert the user if they’re trying to update something that they can’t update. The code below checks that the user is only updating fields that can be updated, otherwise it will send back an error response.

```javascript
const updates = Object.keys(req.body)
const allowedUpdates = ['name', 'email', 'password', 'age']
const isValidOperation = updates.every((update) =>
allowedUpdates.includes(update))
if (!isValidOperation) {
return res.status(400).send({ error: 'Invalid updates!' })
}
```

If the provided updates are valid, `findByIdAndUpdate` can be used to update the document in the database. Try/catch is used here to send back an error if something goes wrong when updating the user. This would include the new data not passing the validation
defined for the model.


```javascript
try {
    const user = await User.findByIdAndUpdate(req.params.id, req.body, { new:
    true, runValidators: true })
    if (!user) {
    return res.status(404).send()
}
    res.send(user)
    } 
    catch (e) {
    res.status(400).send(e)
}
```

### Resource Deleting Endpoints

Resource deleting endpoints use the DELETE HTTP method. The URL structure is
`/resources/:id` for deleting an individual resource by its ID. If you want to delete an
individual task with the ID of 897, it would be `DELETE /tasks/897`.

`app.delete` is used to set up the Express route handler.

```javascript
app.delete('/users/:id', async (req, res) => {
// Route handler
})
```

The handler itself can delete the resource using findByIdAndDelete.

```javascript
try {
    const user = await User.findByIdAndDelete(req.params.id)
    if (!user) {
    return res.status(404).send()
}
    res.send(user)
} catch (e) {
    res.status(500).send()
}
```

### Creating Separate Routers

Express allows you to create as many routers as you want. These separate routers can
then be combined into a single Express application. You can create a new router using
`express.Router` as shown below. The example file below creates the router, adds routes,
and exports the router from the file.

```javascript
const router = new express.Router()
    router.post('/someEndpoint', (req, res) => {
    // Do something
})

module.exports = router
```

The router defined in the file above can be added into the Express application in
`index.js`. This is done by loading the router in with `require` and then passing the router
Version 1.0 78 to app.use. You can set up as many routers as you need for your application, though it’s common to have a router for each distinct resource your REST API has.

```javascript
// Register with existing application
app.use(router)
```