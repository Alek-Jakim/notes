# Props

Props are declared using the `props` option.

```javascript
export default {
  props: ['foo'],
  created() {
    // props are exposed on `this`
    console.log(this.foo)
  }
}
```

```javascript
export default {
  props: {
    title: String,
    likes: Number
  }
}
```


### Passing Different Value Types

```html
<!--NUMBER-->
<!-- Even though `42` is static, we need v-bind to tell Vue that -->
<!-- this is a JavaScript expression rather than a string.       -->
<BlogPost :likes="42" />

<!-- Dynamically assign to the value of a variable. -->
<BlogPost :likes="post.likes" />



<!--BOOLEAN-->
<!-- Including the prop with no value will imply `true`. -->
<BlogPost is-published />

<!-- Even though `false` is static, we need v-bind to tell Vue that -->
<!-- this is a JavaScript expression rather than a string.          -->
<BlogPost :is-published="false" />

<!-- Dynamically assign to the value of a variable. -->
<BlogPost :is-published="post.isPublished" />




<!--ARRAY-->
<!-- Even though the array is static, we need v-bind to tell Vue that -->
<!-- this is a JavaScript expression rather than a string.            -->
<BlogPost :comment-ids="[234, 266, 273]" />

<!-- Dynamically assign to the value of a variable. -->
<BlogPost :comment-ids="post.commentIds" />




<!--OBJECT-->
<!-- Even though the object is static, we need v-bind to tell Vue that -->
<!-- this is a JavaScript expression rather than a string.             -->
<BlogPost
  :author="{
    name: 'Veronica',
    company: 'Veridian Dynamics'
  }"
 />

<!-- Dynamically assign to the value of a variable. -->
<BlogPost :author="post.author" />
```

### Binding Multiple Properties Using an Object


If you want to pass all the properties of an object as props, you can use `v-bind` **without an argument** (v-bind instead of :prop-name). 


```html
<BlogPost v-bind="post" />

<!--
    This is equivalent to:
    <BlogPost :id="post.id" :title="post.title" />
-->
```

All props form a **one-way-down binding** between the child property and the parent one: when the parent property updates, it will flow down to the child, but not the other way around. 