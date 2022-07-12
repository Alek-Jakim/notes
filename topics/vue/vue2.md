# Vue2

Vue is a progressive framework for building user interfaces. Unlike other monolithic frameworks, Vue is designed from the ground up to be incrementally adoptable. The core library is focused on the view layer only, and is easy to pick up and integrate with other libraries or existing projects.

## Hello World Example

```js
<!DOCTYPE html>
<html>
<head>
  <title>My first Vue app</title>
      <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>

</head>
<body>
  <div id="app">
    {{ message }}
  </div>

  <script>
    var app = new Vue({
      el: '#app',
      data: {
        message: 'Hello Vue!'
      }
    })
  </script>
</body>
</html>

```

## Conditionals & Loops

```html
  <div id="app">
    <button v-on:click="toggle()">{{btnText}}</button>
    <span v-if="seen">Now you see me</span>

    <ol>
        <li v-for="task in tasks" :class="{completed: task.completed}">{{task.text}}</li>
    </ol>
  </div>
```

```js
  let app = new Vue({
    el: '#app',
    data: {
      seen: false,
      btnText: "Show",
      tasks: [
        {
            text: "learn vue",
            completed: false
        },
        {
            text: "not fly with ryanair",
            completed: true
        },        
        {
            text: "read some books",
            completed: false
        }
      ]
    },
    methods: {
        toggle: function(){
            this.seen = !this.seen

            if(this.seen) {
                this.btnText = "Hide"
            } else {
                this.btnText = "Show"
            }
            console.log(this.seen)
        }
    } 
  })
```

## User Input

```html
    <div id="app">
        <button v-on:click="reverse()">Reverse Message</button>
        <input type="text" v-model="message">
        <h3>{{message}}</h3>
    </div>
```

```js
let app = new Vue({
    el: "#app",
    data: {
        message: ""
    },
    methods: {
        reverse: function() {
            if(this.message === "") {
                alert("Message empty")
                return
            } else {
                this.message = this.message.split("").reverse().join("");
            }
        }
    }
});
```

## Events


### Click Events

```html
 <body>

    <div id="app">
        <h1>Events</h1>
        <button v-on:click="add">Add a year</button>
        <button v-on:click="subtract">Subtract a year</button>
        <!--double click event-->
        <button v-on:dblclick="addTen">Add 10 years</button>
        <button v-on:dblclick="subtractTen">Subtract a year</button>

        <p>{{age}}</p>
    </div>
    
<script>

    let app = new Vue({
        el: "#app",
        data: {
            age: 28
        },
        methods: {
            add: function() {
                this.age += 1;
            },
            subtract: function() {
                this.age -= 1;
            },
            addTen: function() {
                this.age += 10;
            },
            subtractTen: function() {
                this.age -= 10;
            }
        }
    })
</script>
</body>
```

### Mouse Events


```html
<style>
      #canvas {
            width: 600px;
            padding: 200px 20px;
            text-align: center;
            border: 1px solid #333;
        }
</style>

<div id="app">
  <div id="canvas" v-on:mousemove="updatePosition">{{x}}, {{y}}</div>
</div>

<script>

    let app = new Vue({
        el: "#app",
        data: {
            x: 0,
            y: 0
        },
        methods: {
            updatePosition: function(event) {
                this.x = event.offsetX
                this.y = event.offsetY
            }
        }
    })
</script>
```

### Event Modifiers

It is a very common need to call `event.preventDefault()` or `event.stopPropagation()` inside event handlers. Although we can do this easily inside methods, it would be better if the methods can be purely about data logic rather than having to deal with DOM event details.

To address this problem, Vue provides event modifiers for v-on. Recall that modifiers are directive postfixes denoted by a dot:

* `.stop`

* `.prevent`

* `.capture`

* `.self`

* `.once`

* `.passive`

```html
<body>

    <div id="app">
        <h1>Events</h1>
        <!-- the click event will be triggered at most once -->
        <button v-on:click.once="add">Add a year</button>
        <button v-on:click="subtract">Subtract a year</button>

        <!--Prevents default behaviour, in this case, it won't redirect you to page url, it will just perform the click function-->
        <a href="https://www.google.com/" v-on:click.prevent="click">Some website</a>

        <p>{{count}}</p>
    </div>
    
<script>

    let app = new Vue({
        el: "#app",
        data: {
            count: 28
        },
        methods: {
          click: function() {
            //do something
          }
    })
</script>
</body>
```