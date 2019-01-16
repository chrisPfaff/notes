
# React Hooks

React Hooks is a new feature which is coming with React 16.7 and is adding missing pieces of functionality to React’s functional components:

By using State Hooks it’s possible to add state to functional components
By using Effect Hooks you can add code to functional components which is executed in response to component’s lifecycle events

##### Motivation behind Hooks

The component based design lets us reuse views accross our app, one of the biggest probems dev's face is how can we reuse state logic between components. When we have components that share similar state logic, there hasn't been a great solution for resuse and this can sometimes lead to dulicate logic in lifecycle methods. The most typical way of dealing with this was higher order components and render props.

###### Hooks am to solve all of these by enabling you to write functional components that have access to features like state, context, lifecycle methods, ref, without writing a class component

##### How hooks map to classes

Recall that when writing a component class we often need to maintain state and Use lifecycle methods like componentDidMount() and componentDidUpdate() and access context by setting contextType. 
With react hooks we can replicate a similar behavior in functional components. Component state uses the 
##### useState() 
Hook

lifecycle methods like componentDidMount() use the 
##### useEffect()
Hook

Static contextType uses the 
##### useContext()
Hook

Before hooks, state was usually only used in a class component but as mentioned above, Hooks allows us to add state to a functional component.
```javascript
import React, { useState } from "react";
import ReactDOM from "react-dom";

import "./styles.css";

function LightBulb() {
  let [light, setLight] = useState(0);

  const setOff = () => setLight(0);
  const setOn = () => setLight(1);

  let fillColor = light === 1 ? "#ffbb73" : "#000000";

  return (
    <div className="App">
      <div>
        <LightbulbSvg fillColor={fillColor} />
      </div>

      <button onClick={setOff}>Off</button>
      <button onClick={setOn}>On</button>
    </div>
  );
}

function LightbulbSvg(props) {
  return (
        /*
      Below is the markup for an SVG that is the shape
      of a lightbulb.
      The important part is the `fill`, where we set the
      color dynamically based on props
    */
    <svg width="56px" height="90px" viewBox="0 0 56 90" version="1.1">
      <defs />
      <g
        id="Page-1"
        stroke="none"
        stroke-width="1"
        fill="none"
        fill-rule="evenodd"
      >
      </svg>
  );
}

const rootElement = document.getElementById("root");
ReactDOM.render(<LightBulb />, rootElement);”



 
```