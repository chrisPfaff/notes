# DOM injection and Traversal

* How to detect the viewport is ready
* How to manipulate HTML
* How to add and remove elements from the DOM
* How to traverse up and down the DOM
* How to detect when elements are in the viewport
* How to calculate distances in the viewport

#### HTML and Content 

##### innerHTML
Use innerHTML to get and set HTML content in an element. 
```javascript
const elem = document.querySelector(".some-elem");

//get HTML
let html = elem.innerHTML;

//set HTML
elem.innerHTML = "we can dynamically change the html and even include elements like <a></a> tags"

//add HTML to excisting html elements
elem.innerHTML += "Add this after";

//add HTML to beginning of element
elem.innerHTML = "this will be on the beginning " + elem.innerHTML;
```

##### textContent
The textContent property works just like innerHTML, but only gets the text of an element and omits the markup

```javascript
let elem = document.querySelector('.some-elem');

//get text 
let text = elem.textContent;

//set text
elem.textContent = 'this will change the text'

//add text
elem.textContent += 'this will add after'

//add to beginning
elem.textContent = 'this will be at the beggining' += text.textContent;
```

#### DOM Injection

How to add and remove elements in the DOM

##### createElement()
Use the document.createElement() method to create an element.

```javascript
let div = document.createElement('div');
let link = document.createElement('a ');
let article = document.createElement('article');
```
You can use a valid HTML tag, and even create invalid ones, to for example

```javascript
let chicken = document.createElement('chicken'); /// <chicken></chicken>
let placeholder = document.createElement('_'); // <_></_>
```
You can manipulate an element created with createElement() like you would any other element in the DOM. Add classes, attributes, styles and more.

```javascript
var div = document.createElement('div');
div.className = 'new-div';
div.id = 'new-div';
div.setAttribute('data-div', 'new');
div.style.color = '#fff';
div.style.backgroundColor = 'rebeccapurple';
```

#### insertBefore()

The insertBefore() method is the original way to add elements to the DOM. Call it on the parent of the element you're inserting your new element before (the reference node), and pass in both the new element and the reference node as arguments.
```javascript
//create new element
let newNode = document.createElement('div');

//get the referenceNode
let referenceNode = document.getElementById('some-element')

//insert the new node before the referenceNode
referenceNode.parentNode.insertBefore(newNode, referenceNode);
```
Oddly you can also use it to inject and element after another one by using the .nextSibling property on your reference node

```javascript
//create new element
let newNode = document.createElement('div');

//get reference node
let referenceNode = document.getElementById('some-elem');

//Insert the new node after the referenceNode
referenceNode.parentNode.insertBefore(newNode, referenceNode.nextSibling);
```

#### before()

The before() method is a new es6 function that let's you insert an element before another one. Call the before() method on the reference node, and pass in the new node as an argument.

```javascript
//create new elem
const newNode = document.createElement('div');

//grab the referenceNode
let referenceNode = document.querySelector('some-elem');

//insert new node before the reference node
reference.before(newNode)
```







































