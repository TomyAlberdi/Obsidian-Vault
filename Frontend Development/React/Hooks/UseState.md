Created: 2024-09-22 19:37
## Family Tree:
1. Computer
2. Frontend Development
3. React
4. [[Hooks]]
-- -
In React, the user interface represents the state at the time of the initial render. If any piece of that state changes, React will re-render the components involved with that piece of state after comparing the virtual DOM with the DOM stored in memory. The goal of this process is to make updates efficient and based on the difference between the two DOMs.
Since the release of hooks, functional components can declare and update their internal state using the `useState` hook. This is a function that creates a variable to store a piece of internal state, and it also provides a way to update that value within a functional component.
```jsx
const [state, setState] = useState("Learning");
```
Each component has an associated internal list of "memory cells." These memory cells are translated into JavaScript objects where we store our data. When `useState` is invoked, the function reads the cells one by one. This way, multiple calls to `useState` result in multiple independent local states.
In theory, this allows us to declare an infinite number of `useState` constants:
```jsx
const [count, setCount] = useState(0);
const [phone, setPhone] = useState("");
const [username, setUsername] = useState("");
const [email, setEmail] = useState("");
const [password, setPassword] = useState("");
```
We can include `useState` as many times as we need, with the only condition being that they are called from a top-level scope, not inside a block.
## Types
### State with a single value:
```jsx
const [likes, setLikes] = useState(0);

<button onClick={() => setLikes(likes + 1)}>
```
### State with multiple values:
```jsx
const [state, setState] = useState({
  likes: 0,
  visits: 0
});

<button onClick={() => setState(prev => ({ ...prev, likes: prev.likes + 1 }))}>
```
Here, `prev` is a parameter provided by the `setState` function that gives us access to the previous state value. To update the `state`, we make a copy of everything we had before using the spread operator, and we change only the attribute we want to modify, in this case, `likes`.
It's important to note that `prev` is not a reserved word in the language; it is simply a parameter, and we can name it however we like.
## `UseState` cycle
1. React traverses the component tree, mounting them to render the UI.
2. In each case, React will pass the corresponding props.
3. Each component invokes `useState` for the first time, requesting the initial value from `useState`, which in turn requests it from React.
4. React then returns both the current value and the update function.
5. The component sets up the user event handlers.
6. The component uses the obtained state value to declare the UI.
7. React updates the DOM with the required changes.
8. When the event handler invokes the update function, an event is triggered, and the handler executes. Through the handler, the update function is invoked to modify the state value.
9. React updates the state with the value passed by the update function.
10. React then calls the component again.
11. The component calls `useState` again but disregards the initially passed argument.
12. React returns the current state value and the update function once more.
13. The component creates a new version of the event handler and uses the new state value.
14. The component then returns its UI with the updated state value.
15. Finally, React updates the DOM with the necessary changes.
## `State` vs `setState()`
As we’ve seen, the **state** of a component allows it to store information internally. The state of a component is called **state**, and it’s a literal object (key/value pairs) that stores the information we want. On the other hand, **`setState()`** is a method that lets us update the state whenever we deem necessary.
Why do we say "update" and not "modify"? Because the state is **immutable**.
### Immutability in state:
We define something as **immutable** when its value cannot be changed, and **mutable** is the opposite definition.
Up until now, we had seen this concept applied only to **props**. We defined props as immutable, but we also said that there is a part inside the component where we can update its value as we wish: this is the state. But if the state is immutable, how do we "mutate" it? The truth is, we don’t.
Every time we want to "modify" the internal state of a component, what we’re actually doing is creating or returning a completely new state. So, we’re not truly modifying its value. In practice, we don’t need to worry about this extra logic. We only need to use the **`setState()`** function, which takes care of creating the new state with the applied changes.