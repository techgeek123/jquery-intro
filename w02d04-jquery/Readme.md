# W2.D9

# jQuery Methods

# Learning Competencies

- Define what jQuery is and include the jQuery library on an HTML page
- Explain what a jQuery object is and how it is different than an HTMLElement
- Use jQuery to select elements and make sure the DOM has loaded History/Future of jQuery
- What events are, compare-contrast preventDefault and stopPropagation
- Utilize jQuery animations to add additional dynamic behavior to a page
- Common jQuery methods like fade / slide / hide / show to animate elements jQuery Animations


# Overview

## History and Creator

jQuery was originally released in January 2006 at BarCamp NYC by John Resig and was influenced by Dean Edwards' earlier cssQuery library. It is currently maintained by a team of developers led by Timmy Willison (with the jQuery selector engine, Sizzle, being led by Richard Gibson). 

**John Resig now works at KhanAcademy as INSTRUCTOR & DEVELOPER**

There are so many browsers with difference DOM


## Intro to jQuery
 jQuery is easily one of the most popular JavaScript libraries out there. It is very helpful with DOM manipulation, AJAX, and much more. Instead of using the native DOM API to interact with elements on the page, we can use jQuery to acheive the same functionality, but with an interface which is a bit easier and more friendly.

## How to use it ??
In spite of its waning popularity, jQuery is still in constant development and in use by over 70% of the top 1,000,000 websites (you can learn more about it's usage [here](https://trends.builtwith.com/javascript/jQuery)), which makes it a really important library to learn!

Getting started You can either download the source code for jQuery at jquery.org or you can easily include it on a page using the CDN:

```<script src="http://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.js"></script>.```

## what's $

The first thing you will notice with jQuery is that all of the jQuery selectors and many functions begin with a $. This is just an alias (nickname) for jQuery, which is the main function we'll be using. So if you've installed jQuery, the expression jQuery === $ will always be true!

Now that we have jQuery on a page, let's learn how to use it.
```javascript
$(document).ready or $(function(){})
```
To make sure the DOM has loaded, we can use the 

$(document).ready function or use $(function(){}) 

as shorthand. This is
```javascript
$(document).ready(function(){ // the DOM has now loaded });

$(function() { // a shorter way to wait for the DOM to load });

document.addEventListener("DOMContentLoaded", function() { // a longer way to wait for the DOM to load, without jQuery. // jQuery's syntax is much shorter! }); It's critical that you wait for the DOM to load before using jQuery, otherwise you might try to manipulate DOM elements that aren't on the page yet!

}
```
jQuery objects / get / selectors To get started with jQuery, let's find some elements in the DOM! jQuery selects items from the DOM via CSS selectors (another good reason to know them well!), just like ``querySelector`` and ``querySelectorAll`` in vanilla JavaScript. One major difference between jQuery methods and the native JavaScript methods, however, is what they return to you. When you select something (in the example below this will be all the article tags), jQuery returns an (array-like) object called a jQuery object.
```javascript
$(document).ready(function(){ console.log($("article")); }); 
```
When you examine this in the Chrome console you will see that this looks like an array with [] notation around it. Just know that you can not directly use vanilla JavaScript methods like innerText, style etc. on these. But not to worry, jQuery has all of that covered for us! You can read more about jQuery objects [here](https://www.smashingmagazine.com/2014/05/mystery-jquery-object-syntax-basic-introduction/).

As you start learning jQuery, you may want to 'revert' back to using native DOM methods on jQuery objects. While you can do this, there is almost always a better way to do this with jQuery. So if you find yourself doing things like this, take a step back:
```javascript
$(document).ready(function(){ var mainElement = document.getElementById('main'); // THIS IS NOT GREAT! });
```
 Why is the code above not great? Because we are mixing jQuery with vanilla JavaScript, when jQuery offers us a more concise syntax! So let's use jQuery selectors instead of document.getElementbyId. A cleaner version would be:
```javascript
$(document).ready(function(){ var $mainElement = $('#main'); // THIS IS MUCH BETTER! });
```
 Notice that we added a $ to the definition of the mainElement variable. This is very common when working with jQuery to signify that the variable is a reference to a jQuery object.

 ## Manipulating and modifying elements and attributes
### html / text / val

To grab the innerHTML of a selected element(s) we can use the html function. To grab the innerText of a selected element(s) we can use the text function.
For input elements, we can get the values inside of them with the val function.
```javascript
$(document).ready(function(){
    $("article").html(); // innerHTML
    $("article").text(); // innerText
    $("input").val(); // value
});
```
If you pass strings into these methods, they'll work as setters instead of getters; in other words, they will set the text inside of the element to the string that is passed in.
```javascript
$(document).ready(function(){
    $("article").html("<h1>Here's some large text.</h1>"); // innerHTML
    $("li").text("hi!"); // innerText
    $("input").val("new value"); // value = new value
});
```

### addClass / removeClass / toggleClass

To add, remove, or toggle classes we can use the addClass, removeClass and toggleClass functions:
```javascript
$(document).ready(function(){
    $("article").addClass("hidden"); // add a class
    $("article").removeClass("hidden"); // remove a class
    $("article").toggleClass("hidden"); // toggle the class (if on -> off, if off -> on)
});
```

### css / data / attr

To access the styles of an element we can use the css function. To access the attributes of an element we can use the attr function. To access the data-attributes of an element we can use the data function. As with text, html, and val, these methods can be used as getters or setters. Pass in a single argument to use them as getters; pass in two to use them as setters.
```javascript
$(document).ready(function(){
    $("article").css("background-color", "red");
    $("article").css("background-color"); // "red"
    $("article").attr("style", "display:flex;");
    $("article").data("id", "1");
});
```
## Traversing the DOM with jQuery
### find / parent / children / prev / next

For DOM traversal we can use find, which accepts a CSS selector to find elements inside a selected element. To access the children of a selected element we can use children and to access a child's parent element we can use parent. To find the next element in a list of siblings we can use next and to find the previous sibling we can use prev.

Here's a quick example:
```javascript
$(document).ready(function(){
    var $childDivsInsideArticle = $("article").find("div").children();
});
```
## Filtering with jQuery

jQuery has quite a few helpful methods to select elements based on certain filters. These methods include ``is``, ``has``, ``not``, ``eq`` and many more. You can read more about them [here](http://api.jquery.com/category/traversing/filtering/).

The ``eq`` method is particularly important when accessing elements inside of a jQuery object.

For example:
```javascript
var $firstLi = $("li")[0];
$firstLi.text(); // What do you expect?
```
You might expect that the second line to return "Item 1," since that's the text inside of the first li. But the problem with accessing the first li using bracket notation is that the result is no longer a jQuery object! 

In this case, firstLi is just a plain old HTMLElement: firstLi === document.querySelector('li') returns true. And since text is a jQuery method, not a vanilla JavaScript one, trying to call it on firstLi results in a TypeError.

So how can we fix this? One way would be to use innerText instead of text:
```javascript
var $firstLi = $("li")[0];
$firstLi.innerText; // "Item 1"
```
But mixing vanilla JavaScript and jQuery for DOM access and manipulation is a little confusing. Since we've installed jQuery, it's best to go all in and use jQuery wherever we can.

This is what makes the ``eq`` function so useful. We can use it in place of bracket notation to access elements inside of a jQuery object. Unlike bracket notation, however, the result of eq will again be a jQuery object! So code like this works just fine:
```javascript
var $firstLi = $("li").eq(0);
var $secondLi = $("li").eq(1);
$firstLi.text(); // "Item 1"
$secondLi.text(); // "Item 2"
```

``eq`` also makes things easier when we want to do method chaining in jQuery (which we'll talk about more later on).

## Adding and removing elements from the DOM
### after / before / append / prepend

To add elements to the DOM we can place them after a selected element or before a selected element. We can also append them to a selected element (nested at the end of an element) or prepend them to a selected element (nested at the beginning).

When creating new elements, there are a couple of different options we can use to add attributes, text, and so on. Check out the difference between the way we create ``newParagraph`` and ``anotherParagraph`` below:
```javascript
$(document).ready(function(){
    var $newParagraph = $("<p>");
    $newParagraph.text("Another article");
    $newParagraph.css("color","red");

    var $anotherParagraph = $("<p>", {
        text:"Another approach",
        css: {
            color: "purple",
            // we have to use quotes because of the '-'
            "font-size": "2em"
        }
    });
    $("article").append($newParagraph);
    $("article").prepend($anotherParagraph);
});
```

In the first case, we just create an element, then we set attributes on it in subsequent lines. In the second case, we pass two arguments into the jQuery function: the new element, and an object with the attributes we'd like to set. Both of these approaches are valid ways to use jQuery to append new elements to the DOM.

### remove / empty

To remove elements from the DOM we can use the remove function on a selected element (or elements). If we want to just remove the content inside of the element(s), we can use the empty function.
```javascript
$(document).ready(function(){
     $("article").empty(); // remove all content inside the article
    $("article").remove(); // remove the article element itself from the DOM
});
```
## Adding and removing events with jQuery
### on / off

To add event listeners we can use the on function, which takes a selected element (or elements) and attaches an event listener on what has been selected. To remove event listeners we use the off function..

Just like addEventListener, the first parameter to on or off is the name of the event followed by a callback function. The second parameter is the callback, which specifies what we want to do when the event is fired. Also similar to addEventListener, the callback has access to an event object as its first parameter. This event object has a target property which is tied to the element which triggered the event. However, this is not a jQuery object! if you want to use jQuery methods on the event target, make sure to wrap it in the jQuery function!
```javascript
$(document).ready(function(){
    $("article").on("click", function(e){
        console.log($(e.target).val()); // This works great.
        console.log(e.target.val()); // TypeError! e.target isn't a jQuery object, so doesn't have a .val method.
    });
});
```

## Intro to Events delegation

Event delegation is a very commonly used feature of jQuery. But what is it? 

From learn.jQuery.com:

"```Event delegation refers to the process of using event propagation (bubbling) to handle events at a higher level in the DOM than the element on which the event originated. It allows us to attach a single event listener for elements that exist now or in the future.```"

We have the ability to create dynamic web pages by using events. Events are actions that can be detected by your WebApplication.

Following are the examples events −

 -    A mouse click
 -   A web page loading
 -   Taking mouse over an element
 -   Submitting an HTML form
 -   A keystroke on your keyboard
    etc.

When these events are triggered you can then use a custom function to do pretty much whatever you want with the event. These custom functions call Event Handlers.

### Why's and How's ??

Let's revisit the following HTML, and include jQuery:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <ul> Ingredients
        <li>Sugar</li>
        <li>Milk</li>
        <li>Eggs</li>
        <li>Flour</li>
        <li>Baking Soda</li>
    </ul>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.js"></script>
</body>
</html>
```

What we would like to do is console.log the text of an li when the user clicks on it. Moreover, we'd like to do this by adding a single event listener on the ul instead of one for each li. We did something very similar to this when we learned about the DOM with vanilla JavaScript. So what does it look like in jQuery? We still use the on method, but with one small addition:

```javascript
$(function(){
    // pay CLOSE attention to the 2nd parameter
    $("ul").on("click", "li", function(e){
        console.log("You just clicked on ", $(e.target).text());
    });
});
```

In this case, you can also refer to the event target using the keyword this:
```javascript
// an equivalent approach:
$(function(){
    // pay CLOSE attention to the 2nd parameter
    $("ul").on("click", "li", function(){
        console.log("You just clicked on ", $(this).text());
    });
});
```
The big difference here is that our on method is now accepting three arguments, not two. With event delegation, the callback for the event gets passed as the third parameter. The second parameter is a CSS selector which acts as a filter: the callback only executes if the event target matches the selector passed in.

This is quite useful for adding event listeners that you want to trigger on that don't yet exist on the page. Let's see this in action. Create a new empty HTML file, throw the following code into it, and open the page in Chrome:
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <button>Click me to make a new div!</button>
  <div id="container"></div>
  <script src="http://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>
  <script>
    $(function(){
      var count = 0;
      $("button").on("click", function(){
        var $newDiv = $("<div>", {
          text: "div number " + count
        });
        count++;
        $("#container").append($newDiv);
      });
      $("#container").on("click", "div", function(e){
         console.log("You just clicked on ", $(e.target).text());
      });
    });
  </script>
</body>
</html>
```

## preventDefault vs stopPropagation
With vanilla JavaScript, we saw that the event object contains a preventDefault method to stop the default behavior of an event. This is very common with form submissions because the default action of a form is to refresh a page. Using preventDefault is a very common way of performing validation as well, by making sure that we disable all default behavior until certain conditions have been met.

There's another method, called stopPropagation, which is sometimes confused with preventDefault. Let's briefly highlight an example to show the difference between the two. These methods both exist in vanilla JS and jQuery so you can use them in both environments.

Create a new HTML file, put the following code into it, then open the page in Chrome and open your dev tools (for simplicity, we've thrown the relevant JavaScript code inside of a script tag):
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Long list</title>
</head>
<body>
  <div>
    <a href="http://www.google.com" id="google">Google</a>
  </div>
  <div>
    <a href="http://www.yahoo.com" id="yahoo">Yahoo</a>
  </div>
  <div>
    <a href="http://www.bing.com" id="bing">Bing</a>
  </div>
  <script src="http://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>
  <script>
    $(function() {

      $("div").on('click', function(e) {
        console.log("you clicked on a div!");
      });

      $("#google").on('click', function(e) {
        e.preventDefault();
      });

      $("#yahoo").on('click', function(e) {
        e.preventDefault();
        e.stopPropagation();
      });

      $("#bing").on('click', function(e) {
        e.stopPropagation();
      });

    });
  </script>
</body>
</html>
```
As you can see, this page consists of three a tags, each of which is inside of a div. There are listeners on each a tag, and on each div, so that some code should execute whenever you click on a link or on a div.

However, the behavior you see should be slightly different depending on which link you click on:

- If you click on "Google," you should see that the link doesn't do anything, but you get a message logged to the console. e.preventDefault() is preventing the default behavior of the link (i.e., taking you to Google.com), but it doesn't affect the event listener on the parent div.
- If you click on "Yahoo," nothing should happen. The link is broken, as with "Google," but you also shouldn't see anything in the console! This is because e.stopPropagation() stops the click event from bubbling up from the a tag and on to the link.
- If you click on "Bing", you'll see that the link works. e.stopPropagation() doesn't prevent the default behavior of the link, it just stops the event from bubbling up to the parent div.

Just remember: ``stopPropagation`` will prevent an event from bubbling up, but it won't impact the event's behavior on the target. If you want to stop the default behavior of the event on its target, use preventDefault. This will begin to make more sense once you start building full-stack WebApplications, and begin using these methods (especially preventDefault) more regularly.


### Examples

Check these out:
- Disappear
```html
<!DOCTYPE html>
<html>
<head>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>
<script>
$(document).ready(function(){
    $("p").click(function(){
        $(this).hide();
    });
});
</script>
</head>
<body>

<p>If you click on me, I will disappear.</p>
<p>Click me away!</p>
<p>Click me too!</p>

</body>
</html>
```
- Disappear on double click
```html
<!DOCTYPE html>
<html>
<head>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>
<script>
$(document).ready(function(){
    $("p").dblclick(function(){
        $(this).hide();
    });
});
</script>
</head>
<body>

<p>If you double-click on me, I will disappear.</p>
<p>Click me away!</p>
<p>Click me too!</p>

</body>
</html>
```

- Mouse enter
```html
<!DOCTYPE html>
<html>
<head>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>
<script>
$(document).ready(function(){
    $("#p1").mouseenter(function(){
        alert("You entered p1!");
    });
});
</script>
</head>
<body>

<p id="p1">Enter this paragraph.</p>

</body>
</html>
```

## Animation in jQuery

jQuery comes with a few helpful built-in animations, as well as the ability to create your own using the animate function. These animations used to be more popular, but with CSS transitions/animations they have fallen a bit out of favor. However, they are still good to know, so let's take a look at some examples. Let's continue to use our HTML example from the previous chapter:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <article>
        This is an article.
        <div>
            <p>This is a paragraph inside of a div inside of an article.</p>
        </div>
        <input id="edit_user" type="text" value="My user name">
        <ul class="items">
            <li>Item 1</li>
            <li>Item 2</li>
        </ul>
    </article>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.js"></script>
</body>
</html>
```
### fade / slide / hide / show

Fading, sliding, hiding and showing are very common ways to manipulate the visibility of elements on the page with jQuery. To explore some common methods, put the following JavaScript code in a script tag below where you loaded jQuery:
```javascript
$(document).ready(function(){
    $("article").hide();
    $("article").fadeIn(2000); // fade in over 2000 milliseconds (there are also animations for sliding as well)
    var toggleShow = true;
    $("article").on("click", function(){
        if(toggleShow){
            $("#edit_user").show();
        } else {
            $("#edit_user").hide();  
        }
        $(".items").slideToggle(500); // if hidden, then slideIn. If showing, then slideOut.
        toggleShow = !toggleShow;  // switch the value of the boolean  
    });
});
```
Click on the article once it fades in to execute the callback written above!

You can also perform more general animations, similar to CSS animations, using jQuery's animate function. Here is an example of a custom animation. Replace the previous example with the following code inside of a script tag:

```javascript
$(document).ready(function(){
  $(".items").click(function() {
    $("li").animate({
      // what properties to manipulate
      opacity: 0.5,
      marginLeft: "+=100",
    }, 5000, function() {
      // this code will be executed when the animation is complete
      $("p").css("font-size","+=5");
    });
  });
});
```
(This example highlights another nice feature in jQuery: you can increment numerical property values by passing in a string of the form "+=NUMBER". In this case, clicking on the ul increments the left margin of each li by 100 pixels, and once the animation is complete the font size of each p tag is incremented by 5 pixels.)

Although much of this functionality can now be done using CSS animations, it is important to know how to do simple animations with jQuery and many of these methods like slide, fade, and delay are commonly used in jQuery applications. Remember that these methods have either two options slideDown or slideUp and fadeIn or fadeOut and a useful switch between each one using slideToggle and fadeToggle.

### Examples for animations

Check these out:

- Box

```html
<!DOCTYPE html>
<html>
<head>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>
<script> 
$(document).ready(function(){
    $("button").click(function(){
        $("div").animate({
            left: '250px',
            opacity: '0.5',
            height: '150px',
            width: '150px'
        });
    });
});
</script> 
</head>
<body>

<button>Start Animation</button>

<p>By default, all HTML elements have a static position, and cannot be moved. To manipulate the position, remember to first set the CSS position property of the element to relative, fixed, or absolute!</p>

<div style="background:#98bf21;height:100px;width:100px;position:absolute;"></div>

</body>
</html>
```

- Button
```html
<!DOCTYPE html>
<html>
<head>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>
<script>
$(document).ready(function(){
    $("button").click(function(){
        $("#div1").fadeIn();
        $("#div2").fadeIn("slow");
        $("#div3").fadeIn(3000);
    });
});
</script>
</head>
<body>

<p>Demonstrate fadeIn() with different parameters.</p>

<button>Click to fade in boxes</button><br><br>

<div id="div1" style="width:80px;height:80px;display:none;background-color:red;"></div><br>
<div id="div2" style="width:80px;height:80px;display:none;background-color:green;"></div><br>
<div id="div3" style="width:80px;height:80px;display:none;background-color:blue;"></div>

</body>
</html>
```


# Exploration

- Just one Github link do PHD on jQuery [here](https://github.com/petk/awesome-jquery)
- Understanding event delegation [here](https://learn.jquery.com/events/event-delegation/)
- Refer to Event handler APIs [here](http://api.jquery.com/on/)
-If you want to learn more about the difference between stopPropagation and preventDefault, you can read about it [here](http://stackoverflow.com/questions/5963669/whats-the-difference-between-event-stoppropagation-and-event-preventdefault).
- Event in jQuery [here](https://developer.mozilla.org/en-US/docs/Web/Events)
- More about the animate function [here](http://api.jquery.com/animate/)
