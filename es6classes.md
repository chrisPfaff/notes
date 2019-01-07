# es6 classes

A class is just an object in JS. You can describe what values they will have those will be called instance properties. An instance method will be what the class does and typically the method will use the instance properites to achieve their results. By convention you want to use a capital letter when creating a class. 

###### constructor

Every class has whats called a contructor method and it is only run once during the creation of the object.
```javascript 
class Person {
    constructor() {
        console.log('hello')
    }
}
```
If I were to create a new Object using the new keyword
```javascript
const person = new Person();
```
This would log hello to the terminal/console but only when using the new keyword to instantiate the object. 

###### instance properties
You can create instance properties in two ways in JS. One is when they are defined directly in the constructor.

```javascript 
class Person {
    constructor() {
        this.name = "Joe";
        this.age = 30;
        this.mood = "happy";
    }
}
```

The 
```javscript
this
```
keyword refers to the current object. When typing this it refers to the object being created by that class. The this keyword can be confusing at first but there are certain rules to follow to make it less confusing about which object this is refering to.
* If the new keyword is used when calling the function, this inside the function is a brand new object.
* If apply, call, or bind are used to call a function, this inside the function is the object that is passed in as the argument.
* If a function is called as a method -- that is, if dot notation is used to invoke the function -- this is the object that the function is a property of. In other words, when a dot is to the left of a function invocation, this is the object to the left of the dot. (ƒ symbolizes function in the code blocks)
* If multiple of the above rules apply, the rule that is higher wins and will set the this value.
* If the function is an ES2015 arrow function, it ignores all the rules above and receives the this value of its surrounding scope at the time it’s created. To determine this, go one line above the arrow function’s creation and see what the value of this is there. It will be the same in the arrow function.





