Created: 2024-09-26 17:43
## Family Tree:
1. Computer
2. Frontend Development
3. React
4. [[Hooks]]
-- -
There are some cases where we need to process the information we receive before storing it in our state. Additionally, there may be situations where our state is somewhat complex, requiring us to use more than one `useState`.
In such cases, we can use an alternative Hook that React offers: **`useReducer`**. The structure of this Hook is as follows:
```jsx
const [state, dispatch] = useReducer(reducer, initialArg, init);
```
- **`state`**: Represents the current state, similar to the first argument in a `useState`.
- **`dispatch`**: This is the method that allows us to update the state. Unlike `useState` (where we directly pass the value we want to store in the state), `dispatch` receives an object with the following structure: 
  `dispatch({ type: "actionType", payload: "someValue" });`
	- The `type` property indicates the type of action we want to perform. This helps us identify the action and determine how to update the state for each specific type (as we’ll see later).
	- The `payload` property contains the value that we will send to the reducer function, which can be of any type, as explained below.
- **`reducer`**: The reducer (or reducing function) is a function that receives the current state and the action that was sent using `dispatch`, and it returns a new state with the necessary updates based on the type of action sent. A `switch` statement is often used to determine the logic to execute for each action type.
For example, if we think of a counter, we could have an action to increment the value and another to decrement it. In that case, our reducer function would look like this:
```jsx
function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    case 'decrement':
      return {count: state.count - 1};
    default:
      throw new Error();
  }
}
```
- **`initialArg`**: This allows us to initialize the state with an initial value before any action is executed. For example, if we want to start our counter at 0, we can do it as follows:
```jsx
const [state, dispatch] = useReducer(reducer, {count: initialCount});
```
- **`init`**: This is another way to initialize the state in a deferred manner, reserved for cases where we need to execute some logic to calculate the initial state value. We’ll see an example of how to use this argument later.
## Example
Continuing with the previous example, the complete implementation of `useReducer` within a component would look like this:
```jsx
const initialState = {count: 0};

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    case 'decrement':
      return {count: state.count - 1};
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);
  
  return (
    <>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({type: 'decrement'})}>-</button>
      <button onClick={() => dispatch({type: 'increment'})}>+</button>
    </>
  );
}
```
### Explanation:
- We define an initial state (`initialState`) with a `count` set to 0.
- The `reducer` function takes the current state and an action. Based on the action’s `type`, it either increments or decrements the count.
- Inside the `Counter` component, we use `useReducer` to manage the state. We render two buttons—one to decrement and one to increment the count—and update the state using the `dispatch` method.
## `useReducer` + `useContext`
Let's now explore how we can combine `useReducer` with `useContext`. To do this, we'll go back to our mini GitHub profile application and replace `useState` with `useReducer`.
### Creating the reducer:
We’ll start by creating our reducer function inside the `context.js` file:
```js
// Create a reducer to manipulate the information and store it in state
export const githubUserReducer = (state, action) => {
  switch (action.type) {
    case "CHANGE_USER":
      // Check if the user is the same as the one already stored
      const existingUser = state.username === action.payload.login;
      
      // If it's a different user, extract the properties we want to store and save them in state
      if (!existingUser) {
        const { name, avatar_url, html_url, login } = action.payload;
        
        // Our state is an object with these properties
        const newUser = { name, avatar_url, html_url, username: login };
        
        // Update the information in localStorage if the selected user changes
        setUserInStorage(newUser);
        
        return newUser;
      }
      return state;
    default:
      return state;
  }
};
```
### Replacing `useState` with `useReducer`:
Now that we’ve defined our action and how we want to update the state, we can replace `useState` with `useReducer` inside the context provider:
```jsx
const UserContextProvider = ({ children }) => {
  // Replace useState with useReducer
  const [user, dispatch] = useReducer(
    githubUserReducer,  // Pass the reducer
    {},                 // Pass an empty object as we initialize the state lazily
    getUserFromStorage  // Pass the function to initialize the state lazily
  );

  // Our function now dispatches a "CHANGE_USER" action
  const changeUser = (user) => dispatch({ type: "CHANGE_USER", payload: user });

  return (
    // Share the user and the update function to use them in the components within the context
    <UserContext.Provider value={{ user, changeUser }}>
      {children}
    </UserContext.Provider>
  );
};
```
### Updating the component behavior:
Finally, when using the `changeUser` function, we no longer need to worry about extracting the properties we want to store in the state. The reducer will handle that for us. So, we can modify the component behavior by passing all the information received from the API directly:
```jsx
const onClick = async () => {
  const data = await fetch(`https://api.github.com/users/${input}`);
  const json = await data.json();
  // No need to extract properties here, the reducer will handle it
  changeUser(json);
};
```
### Conclusion:
By combining `useReducer` with `useContext`, we've simplified the usage of the context within our components by moving the logic into our reducer. The app continues to work as expected, but with a cleaner and more maintainable code structure.