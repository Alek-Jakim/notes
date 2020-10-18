## EJS - Embedded JavaScript templating

EJS is a simple templating language that lets you generate HTML markup with plain JavaScript. 

Installationg:
```bash
npm install ejs
```

Setting up the path directory:
```javascript
const path = require('path');

app.set('view engine', 'ejs');
app.set('views', path.join(__dirname, '/views'));
```

Render Content:

```javascript
    app.get('/cats', (req, res) => {
    const cats = ['Blue', 'Rocket', 'Monthy', 'Winston'];
    res.render('cats', { cats });
});
```

```html 
    <ul>
        <% for(let cat of cats) { %>
        <li><%=cat%></li>
        <%  } %>
    </ul>
```