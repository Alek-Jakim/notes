## jQuery

jQuery is one of the most widely used JavaScript libraries in the world.

In 2006 when it was released, all major browsers handled JavaScript slightly differently. jQuery simplified the process of writing client-side JavaScript, and also ensured that your code worked the same way in all browsers.



```javascript
//Code you put inside this function will run as soon as your browser has loaded your page.

//This is important because without your document ready function, your code may run before your HTML is rendered, which would cause bugs.

$(document).ready(function() {
    
});
```

All jQuery functions start with a `$`, usually referred to as a dollar sign operator, or as bling.

jQuery often selects an HTML element with a selector, then does something to that element.

### Selecting, styling, disabling

```javascript
$(document).ready(function() {
    //Target Elements by Type
    $("button").addClass("animated bounce");

    //Target Elements by Class
    $(".well").addClass("animated shake");

    //Target Elements by id Using jQuery
    $("#target3").addClass("animated fadeOut");

    //Remove Class
    $("button").removeClass("btn-primary");

    //Directly change styles
    $("#target1").css("color", "red");

    //Disable an Element
    $("#target").prop("disabled", true);
});
```

jQuery has a function called `.html() `that lets you add HTML tags and text within an element. Any content previously within the element will be completely replaced with the content you provide using this function.

```javascript
$("h3").html("<em>jQuery Playground</em>");
```

### Text & HTML

jQuery also has a similar function called `.text()` that only alters text without adding tags. In other words, this function will not evaluate any HTML tags passed to it, but will instead treat it as the text you want to replace the existing content with.

### Remove

jQuery has a function called `.remove()`that will remove an HTML element entirely

```javascript
$("#target4").remove();
```

### Moving Elements

jQuery has a function called `appendTo()` that allows you to select HTML elements and append them to another element.

```javascript
$("#target4").appendTo("#left-well");
```

### Clone an Element

jQuery has a function called `clone() `that makes a copy of an element.

```javascript
$("#target2").clone().appendTo("#right-well");
```

### Target the Parent of an Element

Every HTML element has a parent element from which it inherits properties.

jQuery has a function called `parent()` that allows you to access the parent of whichever element you've selected.

```javascript
$("#left-well").parent().css("background-color", "blue")
```

### Target the Children of an Element

When HTML elements are placed one level below another they are called children of that element. 

jQuery has a function called `children()` that allows you to access the children of whichever element you've selected.

```javascript
$("#left-well").children().css("color", "blue")
```

### Target a Specific Child of an Element

jQuery uses CSS Selectors to target elements. The `target:nth-child(n)` CSS selector allows you to select all the nth elements with the target class or element type.

```javascript
$(".target:nth-child(3)").addClass("animated bounce");
```

### Target Even Elements

You can also target elements based on their positions using `:odd` or `:even` selectors.

Note that jQuery is zero-indexed which means the first element in a selection has a position of 0.

```javascript
$(".target:odd").addClass("animated shake");
```

### Use jQuery to Modify the Entire Page

Here's how we would make the entire body fade out: 

```javascript
$("body").addClass("animated fadeOut");
```


