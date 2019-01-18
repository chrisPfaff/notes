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
```


