# Getting Elements From The DOM

### querySelectorAll()

Use document.querySelectorAll() to find matching elements on a page. You can use and valid CSS selector. Will return a nodeList.

```javascript 
const elemsRed = document.querySelectorAll('.redElems');
//returns a nodeList of all elemetns with th redElems class

const elemsSnacks = document.querySelectorAll('[data-snack]')
//Gets all elemtns with the [data-snack] attribute
```

### querySelector()
Use document.querySelector() to find the 
###### first matching element on a page. 
If the element isnt found it will return null which may throw an error if you try and do something to it.
```javascript
const elem = document.querySelector('div');
//will grab first div
const elemRed = document.querySelector('.redElem');
//the first element with the class .redElem

// Verify element exists before doing anything with it
if (elemRed) {
// Do something...
}

//helper function 
var getElem = function (selector) {
return document.querySelector(selector) || document.c
reateElement('_');
};
```
#### getElementByid()
Use to get an element by its id

#### getElementsByClassName()

Use getElementsByClassName() to find all the elements on the page that have a specific class or classes.
Note: This returns a live HTMLCollection of elements. If an element is added or removed from the DOM after you set your variable, the list is automatically updated to reflect the current DOM.
```javascript
const elemsByClass = document.getElementsByClassName('some-class');
//Get elements with a class

const elemsWithMultipleClasses = document.getElementsByClassName('some-class another-class')
```

#### getElementsByTagName()

Use get elementsByTagName() to get all the elements that have a specific tag name.
Note: This returns a live HTMLCollection of elements. If an element is added or removed from the DOM after you set your variable, the list is automatically updated to reflect the current DOM.
```javascript
const divs - document.getElementsByTagName('div')
//will get all divs
const paras = document.getElementsByTagName('p')
//will get all paragraphs
```

#### matches()

Use matches() to check if an element would be selected by a particular selector or set of selectors. Returns true if the element is a match and false when its not.
###### only works for dom elements
```javascript 
const elem = document.querySelector(".some-elem")
if(elem.matches('.some-class')) {
    console.log('its a match');
} else {
    console.log('Not a match')
}
```

# A word about selector performace
Selectors that target a specific elemtn type, like get elementById() and getElementsByClassName(), are more than twice as fast as querySelector() and querySelectorAll(). But its not as bad as it sounds. Yes getElementById and ByClassName are faster but the flexibilty and consistency of querySelector() and querySelectorAll() make them the obvious muscle memory choice for projects.
They are not slow just not as fas



# Iterating through a NodeList

#### NodeList.forEach()

es6 intoduced a new forEach() method for looping over NodeLsts. It works exactly the same as Array.forEach()

```javascript
const sammys = document.querySelectorAll('.sandwhich');

sammys.forEach((sandwhich, index) => {
    console.log(sandwhich) // nodeList value
})
```

# Classes 
## How to add, remove, toggle and check for classes on an element.

### classList

The classList API works very similar to jquerys class manipulation functions.

```javascript
const elem = document.querySelector('#some-elem');

elem.classList.add('.new-class');

elem.classList.remove('.diff-class');

elem.classList.toggle('.action-class'); //add class if its not a class remove if //it is

if(elem.classList.contains('.this-class')) {
    //do something
}
```

#### className
You can use clasName to get all of the classes on an element as a STRING, add a class or classes, or completely replace of remove all classes.

```javascript
const elem = document.querySelector('div');

const elemClasses = elem.className;

elem.className += ' new-class'; //add space in front

elem.className = "new-class"; //will replace all classes and only have new one
```

# Attributes
### getAttribute(), setAttribute(), removeAttribute() and hasAttribute()

The getAttribute(), setAttribute(), removeAttribute() and hasAttribute() methods let you get, set, remove and check for the existance of attributes on an element



```javascript
const elem = document.querySelector('#some-elem');

let sammy = elem.getAttribute('data-sandwhich');

elem.setAttribute('data-sandwhich', 'turkey');
elem.setAttribute('class', 'turkey') 

elem.removeAttribute('data-sandwhich');

if(elem.hasAttribute('data-sandwhich')) {
    //do something
}
```
These methods can also be used to manipulate other types of attributes (things like id, tabindex, name, and so on), but these are better done by calling the attribute on the element directly (see below). Older versions of IE don’t always expose attribute properties. While using getAttribute(), setAttribute(), and so on is more verbose, it also ensures the broadest browser compatibility. I prefer to use them whenever possible.

#### Attribute Properties
```javascript
const elem = document.querySelector( '#some-elem' );
// Get attributes
const id = elem.id;
const name = elem.name;
const tabindex = elem.tabindex;
// Set attributes
elem.id = 'new-id';
elem.title = 'The title for this thing is awesome!';
elem.tabIndex = '-1';
// Remove attributes
elem.id = '';
elem.title = '';
elem.name = '';
```

# Event Listeners
How to listen for browser evens and run a callback function when they happen.

#### addEventListener()

use addEventListner to listen for evens on an element. 
```javascript
const btn = document.querySelector('#main-btn');
btn.addEvenListner('click', function(event) {
    console.log(event);
    console.log(event.target) //the clicked element
}, false)
```

##### Multiple Targets

The vanilla JavaScript addEventListener() function requires you to pass in a specific, individual element to listen to. You cannot pass in an
array or node list of matching elements like you might in jQuery or other frameworks.
To add the same event listener to multiple elements, you also cannot just use a for loop because of how the i variable is scoped (as in, it’s not and changes with each loop).
Fortunately, there’s a really easy way to get a jQuery-like experience: event bubbling.
Instead of listening to specific elements, we’ll instead listen for all clicks on a page, and then check to see if the clicked item has a matching selector.

```javascript
window.addEventListener('click', function(event){
    if(event.target.classList.contaiens('click-me')){
        //do something
    }
}, false);
```
##### multiple events

In vanilla JS, each eent type requires its own even listener. Unfortunately, you can't pass multple events to a single listener like you might in other frameworks. But... by using a named function and passing that into your event listener, you can avoid having to write the same code over and over again.

```javascript
const someFunction = function(event) {
    //do something
}

//add event listners 
window.addEventListener('click', someFunction, false)
window.addEventListener('scroll', someFunction, false)
```

# Event Debouncing

Events like scroll and resize can cause huge performance issues on
certain browsers. Paul Irish explains:12
If you’ve ever attached an event handler to the window’s resize event, you have probably noticed that while Firefox fires the event slow and sensibly, IE and Webkit go totally spastic.
Debouncing is a way of forcing an event listener to wait a certain period of time before firing again. To use this approach, we’ll setup a timeout element. This is used as a counter to tell us how long it’s been since the event was last run.
When our event fires, if timeout has no value, we’ll assign a setTimeout function that expires after 66ms and contains our the methods we want to run on the event. If it’s been less than 66ms from when the last event ran, nothing else will happen.

```javascript
//set up timer
let timeout;

//listen for resize events
window.addEventListener('resize', function(even){
    console.log('no debounce')
    // If timer is null, reset it to 66ms and run your functions.
    // Otherwise, wait until timer is cleared
if (!timeout) {
timeout = setTimeout(function() {
            // Reset timeout
timeout = null;
// Run our resize functions
            console.log('debounced');
        }, 66);

}, false)
```































































