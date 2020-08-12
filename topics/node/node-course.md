## Asynchronous Node.js

### Async 101

When running asynchronous code, your code won’t always execute in the order you might
expect.For example, setTimeout is a function that allows you to run some code after a specific amount of time
has passed. setTimeout accepts two arguments, the callback func and the amount of time in milliseconds. 

The setTimeout call doesn’t block Node.js from running
other code while it’s waiting for the 2 seconds to pass.
This asynchronous and non-blocking nature makes Node.js ideal for backend
development. Your server can wait for data from a database while also processing an
incoming HTTP request.

### How Node.js and V8 manage  asynchronous code: 

![](./node_event_loop.jpeg)
![](./call-stack.png)

### Making HTTP Requests (using request)

```bash
npm i request
```

----
## Web Servers

Node.js is commonly used as a web server to serve up websites, JSON, and more.

### Using Express

```bash
# Initialize Dir
npm init -y

#Install Express inside the dir
npm i express 
```

```javascript
//app.js
const express = require('express');
const app = express();

app.get('', (req, res) => {
    res.send('Hello Express')
})

const port = 3000;
app.listen(port, () => {
    console.log(`Server running on port ${port}`);
})
```

### Serving up a static directory

A modern website is more than just an HTML file. It’s styles, scripts, images, and fonts.
Everything needs to be exposed via the web server so the browser can load it in. With
Express, it’s easy to serve up an entire directory without needing to manually serve up
each asset. All Express needs is the path to the directory it should serve.
The example below uses Nodes’ path module to generate the absolute path. The call to
path.join allows you to manipulate a path by providing individual path segments. It starts
with __dirname which is the directory path for the current script. From there, the second
segment moves out of the src folder and into the public directory.

The path is then provided to express.static as shown below.

```javascript
const path = require('path')
const express = require('express')
const app = express()
const publicDirectoryPath = path.join(__dirname, '../public')
app.use(express.static(publicDirectoryPath))
app.get('/weather', (req, res) => {
res.send({
forecast: 'It is snowing',
location: 'Philadelphia'
})
})
app.listen(3000, () => {
console.log('Server is up on port 3000.')
})
```

Start the server, and the browser will be able to access all assets in the public directory.