# React Life Cycle Methods

#### Mounting

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