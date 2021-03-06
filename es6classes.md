# es6 classes

A class is just an object in JS. You can describe what values they will have those will be called instance properties. An instance method will be what the class does and typically the method will use the instance properites to achieve their results. By convention you want to use a capital letter when creating a class. 

##### constructor

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

##### instance properties
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

The more conventional way to create class instance properties is to pass in a value when instatiating the new object. This allows you to make custom classes for whatever values you put in, like making multiple people from one class Person. This is done by putting the the parameters in the constructor function.
```javascript 
class Person {
    constructor(name, age, mood) {
        this.name = name;
        this.age = age;
        this.mood = mood;
    }
}

const Joe = new Person('Joe', 30, "happy");
```
This would create the same object as if you were instantiating the object with the values hardcoded into the constructor. This allows for multiple objects using the same class. If i were to make a new Person like 

```javascript 
const Mike = new Person("Mike", 29, "sad");
```
These two objects would have different this values considering when you use the new keyword it creates a whole new object with a this value attacted to it.

##### instance methods

Like a constructor a instance method is just a function that on inside the class object. They operate just like functions and can be used like function invocations on the class object. In this example 

```javascript
class Person {
    constructor(name, age, mood) {
        this.name = name;
        this.age = age;
        this.mood = mood;
    }
    
    sayName() {
        return `Hello my name is ${this.name}`
    }
}

const Joe = new Person("Joe", 30, "happy");
```
If you were to call Joe.sayName() it would produce a log of "Hello my name is Joe", which would be completely different depending upon when the Class is first instantiated. If you were to do 

```javascript
const Chris = new Person("Chris", 30, "happy")
```

The same method would log "Hello my name is Chris".

##### getters and setters 

Getters and setters can be used to define methods on the class which then are used as if they are properties. To define a getter you use the get then the method name just like how you would with a regular method inside a class.

```javscript

class Person {
    constructor(name, age, currentYear) {
        this.name = name;
        this.age = age;
        this.currentYear
    }
    get ageOfPerson() {
        return this.age;
    }
}

const Joe = new Person('Joe', 30, "happy");
console.log(Joe.ageOfPerson)
```
Since the getter acts like a property there is no need to invoke the ageOfPerson method when using it. Joe.ageOfPerson would return 30. 

Setters work pretty much the same way you can assign new values to your instance properties with a property like syntax. 

```javscript

class Person {
    constructor(name, age, currentYear) {
        this.name = name;
        this.age = age;
        this.currentYear
    }
    get ageOfPerson() {
        return this.age;
    }
    set newAge(age) {
        this.age = age;
    }
}

const Joe = new Person('Joe', 30, "happy");
console.log(Joe.ageOfPerson) // 30
Joe.newAge = 40;
console.log(Joe.ageOfPerson) // 40
```
The Joe.newAge setter can be used just like how object property reassingment syntax works with dot notation. 

##### Static Methods

A static method is a method defined on a class but it is not part of the instantiated object once its been created. It does not require an instance of an object to be used. Most static methods are helper methods or utilities that are relevant to the class but dont have an object bound to them. Like with getters
and setters you need to use a keyword before defining the method. In this case that keyword would be static like below. Keep in mind when calling a static method you do not need to instantiate the object before invoking the method also you can call the static method directly from the class. 

```javascript
class Person {
    constructor(name, age, currentYear) {
        this.name = name;
        this.age = age;
        this.currentYear = currentYear
    }
    
    static reverseName(obj) {
        return obj.name.split('').reverse().join('');
    }
    static isCurrentYear(obj) {
        obj.currentYear === 2018 ? console.log('Yes') : console.log('No')
    }
}
const chris = new Person('Chris', 30, 2018)

//calling directly from Class but still using an instatiated object
console.log(Person.reverseName(chris));
```

##### inhertiance and extends

The extends keyword allows you to achieve inheritance in js classes. This is when you have  parent class and want to create a child class off of that. You use the extends keyword when declaring a new class. In the example below when instantiating the Sweet class it will still have access to the describe method on the Fruit class but the fruit class will not have access to the taste property ot the how to I taste method on the Sweet class.

```javascript 
//Parent Class
class Fruit {
    constructor(name, color) {
        this.name = name;
        this.color = color;
        }
    describe() {
        console.log(`I am a ${this.name} and I am ${this.color}`)
    }    
}
    
class Sweet extends Fruit {
    constructor(name, color, taste) {
        //super calls the parent contructor
        super(name, color);
        this.taste = taste;
    }
    howDoITaste() {
        return `I taste ${this.taste}`;
    }
}
const Apple = new Fruit('Apple', 'red');
const Banana = new Sweet('Banana',  'yellow', 'sweet');

console.log(Banana);
```
###### This is the log for Banana
When you log Banana to the console you can see that the __proto__ which points to the original class that Banana has extended from. This is great because you can have one main class and which will share its functionality with any other class that extends off of it but more specific methods or properties can be kept on the other classes.

Sweet {name: "Banana", color: "yellow", taste: "sweet"}
color: "yellow"
name: "Banana"
taste: "sweet"
__proto__: Fruit
constructor: class Sweet
howDoITaste: ƒ howDoITaste()
__proto__: Object

##### polymorphism 

Polymorphism is the act of redefining a method inside a derived child class of a parent. In the example below since Class dog extends animal and they both share a makeSound method when I instantiate Rosie and invoke Rosie.makeSound() it will log "woof woof" instead of "I make this sound". If there was no makeSound method on the Dog class it would go up the prototype chain and find the makeSound method in the Parent class.  

```javascript 
class Animal {
    constructor(name) {
        this.name = name;
    }
    makeSound () {
        console.log(`I make this sound`);
    }
}
class Dog extends Animal {
    constructor(name) {
        super(name); //calls parents constructor
    }
    makeSound () {
        console.log('woof woof')
    }
}

const Tiger = new Animal('tiger');
tiger.makeSound(); // I make this sound
const Rosie = new Dog('rosie');
Rosie.makeSound();
```
##### super

You can also use the super method to achieve polymorphism. In the example below you can use the super method to call a parent method from a derived child class. I put the super method inside the constructor because it will invoke the method anytime I instatiate a new Dog class. You could also put the super.makeSound() inside another method as well. The super keyword allows you to call methods form the parent class.

```javascript 
class Animal {
    constructor(name) {
        this.name = name;
    }
    makeSound () {
        console.log(`I make this sound`);
    }
}
class Dog extends Animal {
    constructor(name) {
        super(name); //calls parents constructor
        super.makeSound()
    }
    makeSound () {
    console.log('woof woof')
        }
}

const Tiger = new Animal('tiger');
tiger.makeSound(); // I make this sound
const Rosie = new Dog('rosie');


class X {
  constructor() {
    this.arr = [];
  }
  addToArr(...item) {
    this.arr.push(...item);
  }
  returnArr() {
    console.log(this.arr);
  }
}

class Y extends X {
  constructor(){
    super();
  }
  newAdd(...item) {
    super.addToArr(...item)
  }
}

const Z = new Y();
Z.newAdd('Chris');
Z.newAdd(1, 3, 4)
Z.returnArr();
```


