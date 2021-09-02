* `$(document).ready(function() {...});` code put inside this function is going to run as soon as the browser loads the page.

* All jQuery functions start with a dollar sign character `$`, then we select an element with a selector just like we do with normal css, and this is an example of how we select a button and add a class to it: `$("button").addClass("animated bounce");`.

* target with a class: `$(".text-primary").addClass("animated shake");`.

* target with an id: `$("#target6").addClass("animated fadeOut");`.

* it is preferred to add classes for every single element separetely.

* delete or remove a class: `$("#target2").removeClass("btn-default");`.

* changing the css: `$("#target1").css("color", "blue");`, where we add the property followed by the new value.

* You can also change the non-CSS properties of HTML elements: `$("button").prop("disabled", true);`, using the **.prop()** function, we add the property or attribute followed by the value for that property.

* we can change the inner HTML of an element like the text between the tags or even add HTML tage using the **.html()** function: `$("h3").html("<em>jQuery Playground</em>");`, we can also use the **.text()** function to specifically change the text inside a tag.

* remove an element using the **.remove()** function: `$("#target4").remove();`.

* using the function **.appendTo()** we can append or add elements to other elements: `$("#target4").appendTo("#left-well");`, where this will remove the element form its current position/ parent and add it to the new one.

* there is a function called **.clone()** that allows you to make a copy of an element, which is useful when you want to append the element to another parent without actually removing it from the current one: `$("#target2").clone().appendTo("#right-well");`, notice here that we used *function chaining*.

* we can access the parent of an element with the **.parent()** function: `$("#left-well").parent().css("background-color", "blue")`.

* similarly, we use the **.children()** function to target the children of an element: `$("#left-well").children().css("color", "blue")`.

* since jQuery is based on the normal css selectors, we can target a specific child of an element for example: `$(".target:nth-child(3)").addClass("animated bounce");`.

* using the *:odd* and *:even* selectors we can target elements based on thier order: `$(".target:odd").addClass("animated shake");`.

* you can target the whole body element as well, just pass it as it is inside the selector.





