# Sass

One feature of Sass that's different than CSS is it uses variables. They are declared and set to store data, similar to JavaScript.

In Sass, variables start with a `$` followed by the variable name.

```css
$main-fonts: Arial, sans-serif;
$headings-color: green;
```

And to use the variables: 

```css
h1 {
  font-family: $main-fonts;
  color: $headings-color;
}
```

### Nesting

```css
nav {
  background-color: red;

  ul {
    list-style: none;

    li {
      display: inline-block;
    }
  }
}
```

### Create Reusable CSS with Mixins

It's a lot of typing to re-write this rule for all the elements that have a `box-shadow`, or to change each value to test different effects. Mixins are like functions for CSS. Here is how to write one:

```css
@mixin box-shadow($x, $y, $blur, $c){ 
  -webkit-box-shadow: $x $y $blur $c;
  -moz-box-shadow: $x $y $blur $c;
  -ms-box-shadow: $x $y $blur $c;
  box-shadow: $x $y $blur $c;
}
```

The definition starts with `@mixin` followed by a custom name. The parameters (the `$x`, `$y`, `$blur`, and `$c` in the example above) are optional. Now any time a `box-shadow` rule is needed, only a single line calling the mixin replaces having to type all the vendor prefixes. A mixin is called with the `@include` directive:

```css
div {
  @include box-shadow(0px, 0px, 4px, #fff);
}
```

For example:

```css
  @mixin border-radius($radius){
    -webkit-border-radius:$radius;
    -moz-border-radius:$radius;
    -ms-border-radius:$radius;
    border-radius:$radius;
  }

  #awesome {
    width: 150px;
    height: 150px;
    background-color: green;
    @include border-radius(15px);
  }
```

### Use @if and @else to Add Logic To Your Styles

The `@if` directive in Sass is useful to test for a specific case - it works just like the `if` statement in JavaScript.

```css
@mixin text-effect($val) {
  @if $val == danger {
    color: red;
  }
  @else if $val == alert {
    color: yellow;
  }
  @else if $val == success {
    color: green;
  }
  @else {
    color: black;
  }
}
```

### Use @for to Create a Sass Loop

The `@for` directive adds styles in a loop, very similar to a for loop in JavaScript.

`@for` is used in two ways: "start through end" or "start to end". The main difference is that the "start to end" excludes the end number as part of the count, and "start through end" includes the end number as part of the count.


```css
@for $i from 1 through 12 {
  .col-#{$i} { width: 100%/12 * $i; }
}
```

The `#{$i}` part is the syntax to combine a variable (`i`) with text to make a string. When the Sass file is converted to CSS, it looks like this:

```css
.col-1 {
  width: 8.33333%;
}

.col-2 {
  width: 16.66667%;
}

...

.col-12 {
  width: 100%;
}
```

### Use @each to Map Over Items in a List

Sass also offers the `@each` directive which loops over each item in a list or map. On each iteration, the variable gets assigned to the current value from the list or map.

```css
@each $color in blue, red, green {
  .#{$color}-text {color: $color;}
}
```
A map has slightly different syntax. Here's an example:


```css
$colors: (color1: blue, color2: red, color3: green);

@each $key, $color in $colors {
  .#{$color}-text {color: $color;}
}
```

Note that the `$key` variable is needed to reference the keys in the map. Otherwise, the compiled CSS would have `color1`, `color2`... in it. Both of the above code examples are converted into the following CSS:

```css
.blue-text {
  color: blue;
}

.red-text {
  color: red;
}

.green-text {
  color: green;
}
```

### Apply a Style Until a Condition is Met with @while

The `@while` directive is an option with similar functionality to the JavaScript `while` loop. It creates CSS rules until a condition is met.

The `@for` challenge gave an example to create a simple grid system. This can also work with `@while`.

```css
$x: 1;
@while $x < 13 {
  .col-#{$x} { width: 100%/12 * $x;}
  $x: $x + 1;
}
```

First, define a variable `$x` and set it to 1. Next, use the `@while` directive to create the grid system while `$x` is less than 13. After setting the CSS rule for `width`, `$x` is incremented by 1 to avoid an infinite loop.

### Split Your Styles into Smaller Chunks with Partials

Partials in Sass are separate files that hold segments of CSS code. These are imported and used in other Sass files. This is a great way to group similar code into a module to keep it organized.

Names for partials start with the underscore (`_`) character, which tells Sass it is a small segment of CSS and not to convert it into a CSS file. Also, Sass files end with the `.scss` file extension. To bring the code in the partial into another Sass file, use the `@import` directive.

```css
@import 'mixins'
```

### Extend One Set of CSS Styles to Another Element

Sass has a feature called `extend` that makes it easy to borrow the CSS rules from one element and build upon them in another.

For example, the below block of CSS rules style a .panel class. It has a background-color, height and border.

```css
.panel{
  background-color: red;
  height: 70px;
  border: 2px solid green;
}
```
Now you want another panel called `.big-panel`. It has the same base properties as `.panel`, but also needs a `width` and `font-size`. It's possible to copy and paste the initial CSS rules from `.panel`, but the code becomes repetitive as you add more types of panels. The `extend` directive is a simple way to reuse the rules written for one element, then add more for another:

```css
.big-panel{
  @extend .panel;
  width: 150px;
  font-size: 2em;
}
```
The .big-panel will have the same properties as .panel in addition to the new styles.