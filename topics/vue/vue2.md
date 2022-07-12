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
