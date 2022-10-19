# Vue 3

## Installation

Install Vue CLI:

```bash
# Node is required, obviously.

npm install -g @vue/cli
```

Create a build-tool-enabled Vue project:

```bash
npm init vue@latest

# cd <project-name>
# npm install
# npm run dev
```

Creating a project with Vite:

```bash
npm init vite-app <project-name>
# cd <project-name>
# npm install
# npm run dev
```

When you are ready to ship your app to production:

```bash
npm run build
```

---

## Basics

#### **Template Syntax**

```html
<span> {{ msg }} </span>
<span v-text="msg"></span>
```

#### **Setting Inner HTML**

```html
<span v-html="rawHTML"></span>
```

#### **Can use JS Expressions; NOT JS Statements**

```html
<!--This is ok-->
<span> {{ msg.reverse() }} </span>

<!--This is not ok-->
<span> {{ let msg = 'hi' }} </span>
```

#### **Conditional rendering**

```html
<div v-if="date == today">...</div>

<div v-else-if="!done">...</div>

<div v-else>...</div>
```

You could use `v-show` for conditional rendering, the difference is that an element with `v-show` will always be rendered and remain in the DOM; `v-show` only toggles the display CSS property of the element. Doesn't work with `v-else`.

```html
<div v-show="date == today">...</div>
```

#### **Handling Events**

```html
<div v-on:click="count">Increase</div>
<!-- SHORTHAND -->
<div @click="count">Increase</div>
```

```javascript
// Method is passed a Native DOM Event
const count = (event) => {
  console.log(event.target);
};
```

Event modifiers

`.stop` - Stops event propagation

`.once` - Can only trigger event once

`.prevent` - Calls evt.preventDefault

`.self` - Don't send if target = child

#### **Directives**

`v-if` - Puts el in DOM if true

`v-else-if` - Like a usual conditional

`v-else` - Like a usual conditional

`v-show` - Toggles display CSS value

`v-text` - Sets the inner text

`v-html` - Sets the inner HTML

`v-for` - Loop through an array/obj

`v-on` - or `@` Listens to DOM events

`v-bind` - or `:` Reactive updates attribute

`v-model` - Two way data binding

`v-once` - Sets val once; Never update

#### **List rendering**

```html
<!--Basic Loop Over Array-->
<li v-for="item in items" :key="item">{{ item }}</li>

<!--Loop and Track Index-->
<li v-for="(item, index) in items">{{ index }} : {{ item }}</li>

<!--Loop Values in Object-->
<li v-for="obj in objects">{{ obj }}</li>
```

---

# Vue Topics

## [Template Refs](./vue-topics/template-refs.md)

## [Props](./vue-topics/props.md)

## [Slots](./vue-topics/slots.md)
