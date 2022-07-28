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

Template Syntax:

```html
 <span> {{ msg }} </span> 
 <span v-text='msg'></span>
```

Setting Inner HTML:

```html
<span v-html='rawHTML'></span>
```

Can use JS Expressions; NOT JS Statements:

```html
<!--This is ok-->
<span> {{ msg.reverse() }} </span> 

<!--This is not ok-->
<span> {{ let msg = 'hi' }} </span>
```