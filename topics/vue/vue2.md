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
<!--TWO WAY DATA BINDING-->
    <div id="app">
        <button v-on:click="reverse()">Reverse Message</button>
        <!--syncs the state of the form input with the corresponding state in JS. It works like the  onChange event handler in React-->
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

### Keyboard Events

```html
<body>
    <div id="app">
        <label>Name</label>
        <input type="text" v-on:keyup="logName">
        <label>Age</label>
        <!--This will only execute on clicking Enter-->
        <input type="text" v-on:keyup.enter="logAge">
    </div>
<script>
    let app = new Vue({
        el: "#app",
        methods: {
            logName: function(e) {
                console.log(`Name: ${e.target.value}`)
            },
            logAge: function(e) {
                console.log(`Age: ${e.target.value}`)
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


## Computed Properties

For complex logic that includes reactive data, it is recommended to use a computed property.

```html
<body>
    <div id="app">
        <button v-on:click="a++">Increment A</button>
        <button v-on:click="b++">Increment B</button>
        <p>A - {{a}}</p>
        <p>B - {{b}}</p>
        <p>Age + A = {{addToA}}</p>
        <p>Age * B = {{multiplyByB}}</p>
    </div>
<script>
let app = new Vue({
    el: "#app",
    data: {
        age: 28,
        a: 0,
        b: 0
    },
    computed: {
        addToA: function() {
            return this.a + this.age;
        },
        multiplyByB: function() {
            return this.b * this.age;
        }
    }
});
</script>
</body>
```