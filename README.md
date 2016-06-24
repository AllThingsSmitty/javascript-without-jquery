# JavaScript Without jQuery
Tips and practical examples, from the [CatsWhoCode post](http://www.catswhocode.com/blog/javascript-without-jquery-tips-and-practical-examples).


## Table of Contents

1. [Listening for Document Ready](#listening-for-document-ready)
1. [Adding Event Listeners](#adding-event-listeners)
1. [Selecting Elements](#selecting-elements)
1. [Using Ajax](#using-ajax)
1. [Adding and Removing Classes](adding-and-removing-classes)
1. [Fade In](#fade-in)
1. [Hiding and Showing Elements](#hiding-and-showing-elements)
1. [DOM Manipulation](#dom-manipulation)


### Listening for Document Ready

A page can't be manipulated safely until the document is "ready". For that reason, we developers have taken the habit to wrap all of our JS code inside the jQuery `$(document).ready()` function:

```javascript
$(document).ready(function () {
  console.log('ready!');
});
```

The same result can be achieved easily using pure JavaScript:

```javascript
document.addEventListener('DOMContentLoaded', function () {
  console.log('ready!');
});
```


### Adding Event Listeners

Event Listeners are a very important part of JavaScript development. jQuery has a very easy way to handle them:

```javascript
$(someElement).on('click', function () {
  // TODO event handler logic
});
```

You don't need jQuery to create event listeners in JavaScript. Here's how to do so:

```javascript
someElement.addEventListener('click', function () {
  // TODO event handler logic
});
```


### Selecting Elements

jQuery makes it super easy to select elements using an ID, a class name, tag name, etc:

```javascript
// By ID
$('#myElement');

// By Class name
$('.myElement');

// By tag name
$('div');

// Children
$('#myParent').children();

// Complex selecting
$('article#first p.summary');
```

Pure JavaScript features various way to select elements. All of the methods below work on all modern browsers as well as IE8+.

```javascript
// By ID
document.querySelector('#myElement');

// By Class name
document.querySelectorAll('.myElement');

// By tag name
document.querySelectorAll('div');

// Children
document.querySelectorAll('myParent').childNodes;

// Complex selecting
document.querySelectorAll('article#first p.summary');
```


### Using Ajax

As most of you know, Ajax is a set of technologies allowing you to create asynchronymous web applications. jQuery has a set of useful methods for Ajax, including `get()` as shown below:

```javascript
$.get('ajax/test.html', function (data) {
  $('.result').html(data);
  alert('Load was performed.');
});
```

Although jQuery makes Ajax development easier and faster, it's a sure thing that you don't need the framework to use Ajax:

```javascript
var request = new XMLHttpRequest();
request.open('GET', 'ajax/test.html', true);

request.onload = function (e) {
  if (request.readyState === 4) {

    // Check if the get was successful.

    if (request.status === 200) {
      console.log(request.responseText);
    } else {
      console.error(request.statusText);
    }
  }
};
```


### Adding and Removing Classes

If you need to add or remove an element's class, jQuery has two dedicated methods to do so:

```javascript
// Adding a class
$('#foo').addClass('bold');

// Removing a class
$('#foo').removeClass('bold');
```

Without jQuery, adding a class to an element is pretty easy. To remove a class, you'll need to use the `replace()` method:

```javascript
// Adding a class
document.getElementById('foo').className += 'bold';

// Removing a class
document.getElementById('foo').className = document.getElementById('foo').className.replace(/^bold$/, '');
```


### Fade In
Here's a practical example of why jQuery is so popular. Fading an element only takes a single line of code:

```javascript
$(el).fadeIn();
```

The exact same effect can be achieved in pure JavaScript, but the code is way longer and more complicated.

```javascript
function fadeIn(el) {
  el.style.opacity = 0;

  var last = +new Date();
  var tick = function() {
    el.style.opacity = +el.style.opacity + (new Date() - last) / 400;
    last = +new Date();

    if (+el.style.opacity < 1) {
      (window.requestAnimationFrame && requestAnimationFrame(tick)) || setTimeout(tick, 16);
    }
  };

  tick();
}

fadeIn(el);
```


### Hiding and Showing Elements

Hiding and showing elements is a very common task. jQuery offers the `hide()` and `show()` methods for modifying the display of an element.

```javascript
// Hiding element
$(el).hide();

// Showing element
$(el).show();
```

In pure JavaScript, showing or hiding elements isn't more complicated:

```javascript
// Hiding element
el.style.display = 'none';

// Showing element
el.style.display = 'block';
```


### DOM Manipulation

Manipulating the DOM with jQuery is very easy. Let's say you would like to append a `<p>` element to `#container`:

```javascript
$('#container').append('<p>more content</p>');
```

Doing so in pure JavaScript isn't much of a big deal either:

```javascript
document.getElementById('container').innerHTML += '<p>more content</p>';
```
