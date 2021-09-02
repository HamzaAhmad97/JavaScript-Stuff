## General and Buttons

- Bootstrap figures out how wide your screen is.
- We add
  `<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous"/>`
  on top of the HTML file.
- We add all HTML tags in a _div_ with the class **container-fluid**.
- We can make images responsive, for example to fit the view port width, we should add the class **img-responsive** to the image.
- To center text we add the class **text-center** to the text element like headings.
- Bootstrap has its own styles for button elements, we add the classes **btn** and **btn-default**, the button here will be as wide as the text inside it.
- Adding the class **btn-block**, the button will stretch to fill the page's entire horizontal space, meaning that is becomes a block level element, but still these buttons will need the **btn** class.
- By replacing the class **btn-default** with **btn-primary** the color of the button will change, this the main color you are gonna use in your app, and it is useful for highlighting user actions, this button will still need the **btn** and **btn-block** classes.
- Bootstrap comes with a set of predefined colors for buttons, **btn-info** is used to bring attention to optional user actions, like checking information or details of something.
- To notify a user that clicking this button has some destructive actions, like deleting something, use the class **btn-danger**.
- **text-primary** is also for changing the color of text elements like headings.
- By using the inline _span_ element, you can put several elements on the same line, and even style different parts of the same line differently.
- Class **form-control** can be given to form fields of type input text, they will have a width of 100%.

---

## Grids

- Divs with class **row** construct a Bootstrap row, and we split it using other divs with classes like **col-md-\***.
- Bootstrap uses a responsive _12-column_ grid system, which makes it easier to to destribute elements into rows with a specific _relative width_.
- Most of Bootsrap's classes can be applies to divs.
- Bootstrap has different column width attributes that it uses depending on how wide the user's screen is.
- For example, the class **col-md-\***, _md_ means medium, and *is the number specifying how many columns wide the element should be. So, here, this class specifies the column width of an element on a medium-sized screen such as a laptop. There are other values like*xs\* which stands for extra small.
- The **row** class is applied to a div, and the elements can be nested within it.
- We can use **col-xs-\*** classes on form elements.
- It looks like you always have to put an element inside another div to maintain consistancy, like so:

```
<div class="row">
      <div class="col-xs-4">
        <label><input type="checkbox" name="personality"> Loving</label>
      </div>
      <div class="col-xs-4">
        <label><input type="checkbox" name="personality"> Lazy</label>
      </div>
      <div class="col-xs-4">
        <label><input type="checkbox" name="personality"> Crazy</label>
      </div>
</div>
```

---

## Others

- To include **Font Awesome** icons you should put this link element on top of the HTML file `<link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.8.1/css/all.css" integrity="sha384-50oBUHEmvpQ+1lW4y57PTFmhCaXp0ML5d60M1M7uH2+nqUivzIebhndOJK28anvf" crossorigin="anonymous">`.
- The _i_ element is used for icons, we can add Font Awesome classes to the i element to turn it into an icon. We can also use the span element for icons. It seems like we have to always include the 'fas' part, I am still not sure yet.

```
<i class="fas fa-info-circle"></i>
```

We have to include the 'fas' and the 'fa' parts as in the example.

- Bootstrap has a class called **well** that can create a visual sense of depth for your columns, so in case we add this class to a div and nest it inside another one that is inside a row div, it will look like this div is deeper.
- You still can use the attribute _id_ as usual.
