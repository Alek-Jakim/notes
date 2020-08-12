#### Installing Express

```bash
# mkdir myapp
# cd myapp
```
```bash
# npm init
```

```bash
# $ npm install express --save
          # OR
# $ npm install express --no-save
```

#### Simple Express Route

First create a directory named myapp, change to it and run npm init. Then install express as a dependency, as per the installation guide.

This app starts a server and listens on port 3000 for connections. The app responds with “Hello World!” for requests to the root URL (/) or route. For every other path, it will respond with a 404 Not Found.

```javascript
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(port, () => {
  console.log(`Example app listening at http://localhost:${port}`)
})
```


#### Serving up Static Assets

The path that you provide to the `express.static` function is relative to the directory from where you launch your node process. If you run the express app from another directory, it’s safer to use the absolute path of the directory that you want to serve:

```javascript
app.use('/static', express.static(path.join(__dirname, 'public')))
```

```javascript
//My Example
const express = require('express');
const path = require('path')

let app = express();

let publicDir = path.join(__dirname, '../public');

app.use(express.static(publicDir));

app.get('', (req, res) => {
    res.send('hello')
})
```

## [my link](./node-course.md)