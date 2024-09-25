Created: 2024-09-24 19:16
## Family Tree:
1. Computer
2. Frontend Development
3. React
4. [[Hooks]]
-- -
Starting with React version 16.8, we can use state and other features without needing to define a class component. We already know how a functional component can handle its internal state thanks to the introduction of the `useState` hook, but how do we handle the lifecycle and side effects in a functional component? The answer is: by using **`useEffect()`**.
A functional React component uses props and/or state to calculate its output. If the functional component performs calculations that are not related to its output, these calculations are called **side effects**.
The `useEffect` Hook allows us to perform side effects in functional components. It is the equivalent, condensed into a single function, of what can be done with the `componentDidMount()`, `componentDidUpdate()`, and `componentWillUnmount()` methods in a class component.
## Characteristics
- It has access to variables inside the component, as they share the same scope.
- It runs after the first render and after each subsequent update unless configured otherwise.
- It allows us to think differently about the lifecycle, focusing more on logical component synchronization.
## Implementation
Imagine we want to create a functional component that represents a greeting for a given user. We want to return a message containing the name received through props and a side effect that changes the title of our page to display the user's name at the top of the page. We want to do this every time this prop changes.
**Example with incorrect use of side effects:**
```jsx
function Greeting({ name }) {
  const message = `Hello, ${name}!`; // Construct the message
  // Error!!👇 - We shouldn't generate effects here
  document.title = `Greeting: ${name}`; // Side effect
  return <div>{message}</div>; // Return value
}
```
The component's rendering logic and side effect logic should be independent. It’s a mistake to perform side effects directly within the body of the component, which is primarily used to calculate the component’s output.
**Example with correct use of side effects:**
```js
//👇 Import the hook for use
import { useEffect } from 'react';
function Greeting({ name }) {
  // Construct the message
  const message = `Hello, ${name}!`;
  //👇 Use the useEffect hook
  useEffect(() => {
    // Recommended way to handle a side effect
    document.title = `Greeting: ${name}`; // Side effect
  }, [name]); 
  // This way, it will re-render only if there is a change in the “name” prop
  return <div>{message}</div>; // Component structure
}
```
In the above example, updating the document title is the side effect because it’s not directly calculated and doesn’t depend on the component's output. Therefore, we don’t want the page title to update every time the `Greeting` component re-renders. However, we do want to change the title only when the name prop changes, which is why we provide `name` as a dependency in the array. Example: `useEffect(callback, [name])`.
## Understanding `useEffect`
The `useEffect` hook accepts two arguments:
```
useEffect(callback, [array of dependencies]);
```
Thus, we need to put the side effect logic inside the callback function (the first parameter) and use the dependency array (the second parameter) to control when that particular side effect should execute.
The following image shows the execution flow of a component using the `useEffect` hook.
![[Frontend Development/React/Hooks/attachments/image.png]]
### Controlling the side effect through the dependency array:
- **Array not supplied**: The side effect occurs after every render of the component.
```jsx
function MyHookUseEffect() {
  useEffect(() => {
    //👇 Always runs after each render
    // -- some side effect --
  }); // No dependency array is provided
}
```
- **Empty array**: The side effect only runs once after the component's initial render.
```jsx
function MyHookUseEffect() {
  useEffect(() => {
    //👇 Runs only after the first render
    // -- some side effect --
  }, []); // The array is declared, even if empty
}
```
- **Array controlled by props and/or state**: The side effect runs once after the initial render and re-runs every time one of the dependency array values changes.
```jsx
function MyHookUseEffect({ prop }) {
  const [state, setState] = useState("");
  useEffect(() => {
    //👇 Runs after each render
    // -- some side effect --
  }, [prop, state]); // Re-runs whenever a value in the array changes
}
```
### Cleaning up side effects with `useEffect`:
Components that use side effects may need some cleanup or shutdown. Common examples are closing open connections or terminating active timers.
```jsx
function MyHookUseEffectCleanUp() {
  useEffect(() => {
    //👇 Runs after each render
    // -- some side effect --
    // A cleanup function is returned to handle cleanup when the component unmounts
    return function cleanup() {
      // Perform some cleanup action for the effect
    };
  }, [dependencies]);
}
```
In `useEffect`, if the primary callback (first parameter) returns a function, it is considered responsible for cleaning up the side effect.
The following image shows the execution flow of a component using the `useEffect` Hook, including the cleanup process for side effects.
![[Frontend Development/React/Hooks/attachments/image 1.png]]
## Use cases
### Setting the page title imperatively:
The page title is outside React's root node (`#root`). However, it is accessible through the `document` interface.
```jsx
import { useEffect, useState } from "react";

const ChangeTitleExample = () => {
  const [title, setTitle] = useState(
    "Certified Tech Developer | Digital House"
  );

  useEffect(() => {
    document.title = title;
  }, [title]);
  
  return <div />;
};

export default ChangeTitleExample;
```
### Working with timers: `setInterval` or `setTimeout`:
```jsx
import { useEffect, useState } from "react";

const Interval = () => {
  const [count, setCount] = useState(2);

  useEffect(() => {
    const interval = setInterval(() => {
      setCount((prevState) => ++prevState);
    }, 1000);

    // Clean up the interval when the component unmounts
    return () => clearInterval(interval);
  }, []);
  
  return <div>I want {count} chocolates</div>;
};

export default Interval;
```
### Reading the width, height or position of DOM elements:
Here's an example where we detect the window's width and height when resized and log a message to the console.
```jsx
import { useEffect } from "react";

const GetResizeFromWindow = () => {
  useEffect(() => {
    function handleResize() {
      console.log("Resized: ", window.innerWidth, "x", window.innerHeight);
    }

    window.addEventListener("resize", handleResize);

    // Clean up the event listener when the component unmounts
    return () => window.removeEventListener("resize", handleResize);
  }, []);
  
  return <div />;
};

export default GetResizeFromWindow;
```
### Setting or getting local storage values:
We can use the browser's local storage for a variety of scenarios, like checking if a user is logged in.
```jsx
import React, { useState, useEffect } from "react";
import Login from "./Login";
import Home from "./Home";

const UserLogged = () => {
  const [user, setUser] = useState();

  useEffect(() => {
    function checkUser() {
      const item = localStorage.getItem("User");
      if (item) setUser(item);
    }

    window.addEventListener("storage", checkUser);

    // Clean up the event listener when the component unmounts
    return () => {
      window.removeEventListener("storage", checkUser);
    };
  }, []);
  
  return <>{user ? <Home /> : <Login />}</>;
};

export default UserLogged;
```
### Making requests to services:
When making an API request using `Fetch` or `Axios`, you should declare `async` and `await` since the `useEffect` callback is synchronous.
```jsx
useEffect(() => {
  async function getCandy() {
    const resp = await fetch("https://alotofcandy.iumi");
    const data = await resp.json();
    setCandy(data);
  }
  
  getCandy();
}, []);
```