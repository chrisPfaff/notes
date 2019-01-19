# Getting Elements From The DOM

### querySelectorAll()

Use document.querySelectorAll() to find matching elements on a page. You can use and valid CSS selector. Will return a nodeList.

```javscript 
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
```javscript 
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

```javscript
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






























































