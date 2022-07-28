# What is Vue ?

- Front-end, JavaScript/TypeScript framework

- Used to create dynamic & data-driven websites (SPA's)

- Can also be used to create stand-alone widgets

## What is Vue used for ?

- Used to create a whole website with multiple pages & components

- These websites are calles SPA's

- All routing is done in the browser & not in the server

---
## [Vue 2](./vue2.md)

## [Vue 3](./vue3.md)
---

## Setup


1. Copy & Paste CDN link into `index.html`

```html

    <!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-->
    <script src="https://unpkg.com/vue@next"></script>
    <title>Vue</title>
    -->
</head>

<body>

    <div id="root"></div>

    <script src="app.js"></script>
</body>

</html>
```

2.

```javascript
const app = Vue.createApp({
    //data, functions
    //template: '<h2>I am the template</h2>'
})

app.mount("#root")
```

## Data & Templates

```javascript
const app = Vue.createApp({
    data() {
        return {
            title: 'The Final Empire',
            author: 'Brandon Sanderson'
        }
    }
})

app.mount("#root")
```

```html
<div id="root">
        <p>{{title}} - {{author}}</p>
</div>
```

## Click Events

```javascript
const app = Vue.createApp({
    data() {
        return {
            num: 10
        }
    }
})

app.mount("#root")
```

```html
<div id="root">
    <p>{{num}}</p>
    <button v-on:click="num++">Increment</button>
    <button @click="num--">Decrement</button>

    <!-- v-on:click and @click are the same thing -->
</div>
```

You can create a method property like so:

```html
<div id="root">
        <p>{{titles[random]}} - {{author}}</p>

        <button @click="changeTitle">Change</button>
</div>
```

```javascript
const app = Vue.createApp({
    data() {
        return {
            titles: ['The Way of Kings', 'The Final Empire', 'Elantris'],
            author: 'Brandon Sanderson',
            random: 0
        }
    },
    methods: {
        changeTitle() {
            this.random = Math.floor(Math.random() * 3)
        }
    }
})

app.mount("#root")
```

## Conditional Rendering

```html
<div id="root">
        <div v-if="isHidden">
            <p>{{titles[0]}} - {{author}}</p>
        </div>

        <button @click="hideData">{{buttonText}}</button>
        <!--
            You can also do it like this
            <span v-if="isHidden">Hide Books</span>
            <span v-else>Show Books</span>
        -->
</div>
```

```javascript
const app = Vue.createApp({
    data() {
        return {
            titles: ['The Way of Kings', 'The Final Empire', 'Elantris', 'Warbreaker'],
            author: 'Brandon Sanderson',
            isHidden: true,
            buttonText: 'Hide Books'
        }
    },
    methods: {
        hideData() {
            if (!this.isHidden) {
                this.buttonText = 'Hide Books'
            } else {
                this.buttonText = 'Show Books'
            }
            this.isHidden = !this.isHidden
        }
    }
})

app.mount("#root")
```

You can also use the `v-show` directive:

```html
<div id="root">
        <div v-show="isHidden">currently showing books</div>
        <!--if the value evaluates to true, it shows the html element and doesn't if it's false-->
</div>
```