* `$(document).ready(function() {...});` code put inside this function is going to run as soon as the browser loads the page. As a shortcut, it can be written as follows: `$(function() {// jQuery code goes here});`.

* All jQuery functions start with a dollar sign character `$`, then we select an element with a selector just like we do with normal css, and this is an example of how we select a button and add a class to it: `$("button").addClass("animated bounce");`.

* target with a class: `$(".text-primary").addClass("animated shake");`.

* target with an id: `$("#target6").addClass("animated fadeOut");`.

* it is preferred to add classes for every single element separetely.

* delete or remove a class: `$("#target2").removeClass("btn-default");`.

* changing the css: `$("#target1").css("color", "blue");`, where we add the property followed by the new value.This function can also be used to get the value of the provided attribute if not given the second argument. To set multiple properties, pass the function a json containing the css rules: `css({"property":"value","property":"value",...});`.

* You can also change the non-CSS properties of HTML elements: `$("button").prop("disabled", true);`, using the **.prop()** function, we add the property or attribute followed by the value for that property.

* we can change the inner HTML of an element like the text between the tags or even add HTML tage using the **.html()** function: `$("h3").html("<em>jQuery Playground</em>");`, we can also use the **.text()** function to specifically change the text inside a tag. Note that both can be also used to get the text/ innerHTML of the selected element not only to change those values. When these methods are used to set content, the existing content is lost/completely replaced.

* remove an element using the **.remove()** function: `$("#target4").remove();`.

* using the function **.appendTo()** we can append or add elements to other elements: `$("#target4").appendTo("#left-well");`, where this will remove the element form its current position/ parent and add it to the new one.

* there is a function called **.clone()** that allows you to make a copy of an element, which is useful when you want to append the element to another parent without actually removing it from the current one: `$("#target2").clone().appendTo("#right-well");`, notice here that we used *function chaining*.

* we can access the parent of an element with the **.parent()** function: `$("#left-well").parent().css("background-color", "blue")`.

* similarly, we use the **.children()** function to target the children of an element: `$("#left-well").children().css("color", "blue")`.

* since jQuery is based on the normal css selectors, we can target a specific child of an element for example: `$(".target:nth-child(3)").addClass("animated bounce");`.

* using the *:odd* and *:even* selectors we can target elements based on thier order: `$(".target:odd").addClass("animated shake");`.

* you can target the whole body element as well, just pass it as it is inside the selector.

* `.show()` is used to set a time for an animation and to specify an action after that animation is complete.

* `.attr()` is used to get the value of an attibute: `let href = $("a").attr("href")`, including href, src, id, class, style. You can also use it to set the value of an attribute by providing it as the second argument: `$("a").attr("href", "https://www.google.com")`.

* to remove an attribute use the function `.removeAttr()`: `$("table").removeAttr("class");`.

* the function `.val()` allows you to get and set the value of a form element like a text area: `$("#name").val("Hamza")`, also to get the value of the value attribute but without passing any value to the function.

* `.append()`, `.prepend()`, `.after()` and `.before()` are used to add new content to an element without deleting the existing content.

1. append() inserts content at the end of the selected elements.
2. prepend() inserts content at the beginning of the selected elements.
3. after() inserts content after the selected elements.
4. before() inserts content before the selected elements.

You can also specify multiple elements as arguments for these functions, but they should be separated by commas.

* the easiest way to create a new HTML element with jQuery is like this: `let txt = $("<p></p>").text("Hi");`.

* The `.toggleClass()` method toggles between adding/removing classes from the selected elements, meaning that if the specified class exists for the element, it is removed, and if it does not exist, it is added, example: 

```
$(function()  {
  $("button").click(function() {
    $("p").toggleClass("red");
  });
});
```

* `.width()` and `.height()` can be used to set the width and height of an element: `$(div).width(100)`, but they only set and get the inner height and width of that element. The `innerWidth()` and `innerHeight()` methods also include the padding. The `outerWidth()` and `outerHeight()` methods include the padding and borders.

![](https://api.sololearn.com/DownloadFile?id=3120)

