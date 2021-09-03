# SASS

* we can define variables in SASS by typing `$` followed by the variable name: `$headings-color: green;`, then we can use them later: 

```
h1 {
  font-family: $main-fonts;
  color: $headings-color;
}
```

* nesting in SASS is different than that of CSS: 

This is how we do it in CSS:
```
nav {
  background-color: red;
}

nav ul {
  list-style: none;
}

nav ul li {
  display: inline-block;
}
```
And this is how we do it with SASS:

```
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
This helps a lot when the number or lines and rules.

* A **mixin** is a group of CSS declarations that can be reused throughout the style sheet. For example consider using or adding properties that are not supported by all browsers, you will need to use vendor prefixes, and your code might look like that, but you will also need to copy the same rules for every div that will have a box-shadow property:

```
div {
  -webkit-box-shadow: 0px 0px 4px #fff;
  -moz-box-shadow: 0px 0px 4px #fff;
  -ms-box-shadow: 0px 0px 4px #fff;
  box-shadow: 0px 0px 4px #fff;
}
```
Mixins are like funcitons, they start with `@mixin`, and they can take parameters, which are optional, they look like this:

```
@mixin box-shadow($x, $y, $blur, $c){ 
  -webkit-box-shadow: $x $y $blur $c;
  -moz-box-shadow: $x $y $blur $c;
  -ms-box-shadow: $x $y $blur $c;
  box-shadow: $x $y $blur $c;
}
```
Now when the box-shadow is needed again we can just use the mixin we defined using the `@include` directive: 
```
div {
  @include box-shadow(0px, 0px, 4px, #fff);
}
```

* we can use the `@if` directive to test for specific cases:

```
@mixin make-bold($bool) {
  @if $bool == true {
    font-weight: bold;
  }
}
```
and we can also use `@else` and `@else if` as in JavaScript:

```
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
notice that the if/else statement here does not need parantheses, and the values are not surrounded by quotation marks.

* We can also use the `@for` directive to loop in SASS, here we have two ways, where the firt one is **start to end** which means that it excludes the end number as part of the count, while the **start though end** includes the end number as part of the count:

```
@for $i from 1 through 12 {
  .col-#{$i} { width: 100%/12 * $i; }
}
```
Notice that in this code above, it actually creates classes and gives them properties.

The `#{$i}` part is the syntax to combine a variable (i) with text to make a string. When compiled to CSS, this will look like this:

```
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
this is useful for grid layouts and animations.


* the `@each` directive allows us to loop over items in a list or a map. On each iteration, the variable gets assigned to the current value from the list or map:
```
@each $color in blue, red, green {
  .#{$color}-text {color: $color;}
}
```
a **map** has a different syntax:
```
$colors: (color1: blue, color2: red, color3: green);

@each $key, $color in $colors {
  .#{$color}-text {color: $color;}
}
```
the `$key` variable is needed to reference the keys in the map just like destrucuring dictionaries in Python.

The code above will look like this when compiled to normal CSS:

```
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
* The `@while` directive allows you to create rules until a condition is met:
```
@while $x < 13 {
  .col-#{$x} { width: 100%/12 * $x;}
  $x: $x + 1;
}
```

* **Partials** in Sass are separate files that hold segments of CSS code. These are imported and used in other Sass files. This is a great way to group similar code into a module to keep it organized. Names for partials start with the underscore (_) character, which tells Sass it is a small segment of CSS and not to convert it into a CSS file. Also, Sass files end with the .scss file extension.

For example, say we have a main SASS file with the name "main.scss", and we need to import all of our mixins that are stored in file called "_mixins.scss", we do the following in the main file:

```
@import 'mixins'
```
we do not need to add the underscore, SASS understands that this is a partial.

* The **extend** feature makes it easy to borrow the CSS rules from one element and build upon them in another (inheritance). Say we have a block of CSS that has a set of rules:

```
.panel{
  background-color: red;
  height: 70px;
  border: 2px solid green;
}
```

We can extend or build upon these rules in another element by using the `@extend` directive:

```
.big-panel{
  @extend .panel;
  width: 150px;
  font-size: 2em;
}
```




