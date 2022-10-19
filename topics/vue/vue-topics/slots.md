# Slots

Vue slots let us pass template content to a child component, allowing us to make more general components and cut down on repeated code.

```html
<!--./components/CaptionedContent.vue-->
<template>
  <div>
    <img src="https://i.stack.imgur.com/y9DpT.jpg" alt="placeholder-photo" />
    <p>
      <slot>Caption</slot>
    </p>
  </div>
</template>
```

```html
<!--./components/CaptionedContent.vue-->
<template>
  <div>
    <img src="https://i.stack.imgur.com/y9DpT.jpg" alt="placeholder-photo" />
    <p>
      <slot>Caption</slot>
    </p>
  </div>
</template>
```

```html
<!--./App.vue-->
<template>
  <div>
    <h1>Hello</h1>
    <!--this will display the image and the text entered below-->
    <CaptionedContent>Something</CaptionedContent>

    <!--this will display the image and the fallback text, in this case 'Caption'-->
    <CaptionedContent />
  </div>
</template>
```

## Named Slots

Sometimes we need to use multiple slots in a single component. This is where names slots come in. These are the 2 steps to using them:

1. Name the slot with the `name` attribute.

2. Specify which slot we are targeting with `v-slot`.

```html
<!--./components/CaptionedContent.vue-->

<template>
  <div>
    <slot name="content">
      <img src="https://i.stack.imgur.com/y9DpT.jpg" alt="placeholder-photo" />
    </slot>
    <p>
      <slot name="caption">Caption</slot>
    </p>
  </div>
</template>
```

```html
<!--./App.vue-->

<template>
  <div>
    <div style="background: red">
      <CaptionedContent>
        <!--you can also use #caption instead of v-slot:caption -->

        <template v-slot:caption> </template>
      </CaptionedContent>
    </div>
    <div style="background: green">
      <CaptionedContent>
        <template v-slot:content>
          <img
            src="https://i.picsum.photos/id/805/536/354.jpg?hmac=RXC0ZMMUOP40AcmXEFwCVG94YG2LZEs9DQyoEYHLF0k"
          />
        </template>
      </CaptionedContent>
    </div>
  </div>
</template>
```

## Scoped Slots

Slot content does not have access to state in the child component. There are cases where it could be useful if a slot's content can make use of data from both the parent scope and the child scope.
