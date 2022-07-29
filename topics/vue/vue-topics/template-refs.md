# Template Refs in Vue

To get direct access to the underlying DOM elements, use the `ref` attribute.

```html
<input ref="input" />
```

`ref` is a special attribute, similar to `key`. It allows us to obtain a direct reference to a specific DOM element or child component instance after it's mounted. 

```html
<template>
  <div>
    <input class="border border-w-4 border-sky-500" type="text" ref="name" />
    <button @click="handleClick">Click me</button>
  </div>
</template>

<script>
export default {
  name: "TemplateRefs",
  methods: {
    handleClick() {
      console.log(this.$refs.name);
      this.$refs.name.classList.toggle("border-red-400");
      this.$refs.name.focus();
    },
  },
};
</script>
```

### Ref on Component

`ref` can also be used on a child component. In this case the reference will be that of a component instance:


```html
<script>
import Child from './Child.vue'

export default {
  components: {
    Child
  },
  mounted() {
    // this.$refs.child will hold an instance of <Child />
  }
}
</script>

<template>
  <Child ref="child" />
</template>
```