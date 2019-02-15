# React Life Cycle Methods

#### Mounting in Order

##### Constructor
Just like with using es6 classes the first thing that gets called in a React class is the ```constructor``` this does not apply to functional components. A constructor should look like this.
```javascript
class App extends Component {
    constructor(props) {
        super(props);
        
    }
}
```
The constructor gets called with the component props and you must call super and pass in the props. You can also initialize state in two different ways. Remember that the ```constructor``` is optional so if it is left out you would initialize state like this
```javascript
class App extends Component {
    state = {
        name: ''
    }
}
```
With the ```constructor``` you initialzie state inside the ```constructor``` like this with the ```this``` keyword
```javascript
class App extends Component {
    constructor(props) {
    super(props);
        this.state = {
            name: ''
        }
    }
}
```
You will also need a constructor if you are going to use a ```ref``` as well. 
#### DO: Set Up State
#### DONT: Cause Side Effects
____

##### getDerivedStateFromProps

When mounting ```getDerivedStateFromProps``` is the last method called before ```render``` . The ```getDerivedStateFromProps``` method is used to set the State of something before the component is mounted and updated. You can also use the constructor to set the state from props but this way is more intuitive. The most common use for this is return a state based object on the intial props.
```javascript 
class Square extends Component {
    constructor(props) {
        super(props);
        this.state = {
            tiles: 0
        }
    }
    static getDerivedStateFromProps(props, state) {
        return {titles: someMethod(props.numberOfTiles)}
    }
}
```
#### DO: Sync state to Props
#### DONT: Cause Side-effects
____


