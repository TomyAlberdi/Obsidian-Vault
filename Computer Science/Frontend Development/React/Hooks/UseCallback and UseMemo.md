Created: 2024-09-24 19:44
## Family Tree:
1. Computer
2. Frontend Development
3. React
4. [[Hooks]]
-- -
Both `useCallback` and `useMemo` expect the same parameters: a function and a dependency array. The difference between them lies in their behaviour during renders:
- **`useCallback`** returns a memoized version of the callback function that only changes if one of the dependencies has changed. It focuses on **preserving the reference** of the function across renders.
- **`useMemo`** executes the provided function and returns a **memoized value** that is recalculated only when one of the dependencies changes.
## Key difference
- **`useCallback`** returns the **function itself**.
- **`useMemo`** executes the function and returns the **result of the function**.
## Why use this hooks?
These hooks can be used when working with values that are rendered many times. By keeping a reference to these values in memory, we can optimize the next render. This behavior is derived from a concept called **memoization**, which works similarly to caching, storing execution data in memory.
## Example of `useCallback`
Let's start our example with this code:
```jsx
import { useCallback, useState } from 'react';

const Button = ({ handleClick, name }) => {
  console.log(`${name} rendered`);
  return <button onClick={handleClick}>{name}</button>;
};

const Counter = () => {
  console.log('counter rendered');
  const [countOne, setCountOne] = useState(0);
  const [countTwo, setCountTwo] = useState(0);
  return (
    <>
      {countOne} {countTwo}
      <Button handleClick={() => setCountOne(countOne + 1)} name="button1" />
      <Button handleClick={() => setCountTwo(countTwo + 1)} name="button2" />
    </>
  );
};
```
The execution of the above code gives the following result:
```
// counter rendered
// button1 rendered
// button2 rendered
```
If we apply `useCallback` to our `handleClick` functions and wrap our `Button` in `React.memo`, we can see what `useCallback` provides. `React.memo` is similar to `useMemo` and allows us to memoize a component.
```jsx
import { useCallback, useState } from 'react';

const Button = React.memo(({ handleClick, name }) => {
  console.log(`${name} rendered`);
  return <button onClick={handleClick}>{name}</button>;
});

const Counter = () => {
  console.log('counter rendered');
  const [countOne, setCountOne] = useState(0);
  const [countTwo, setCountTwo] = useState(0);
  const memoizedSetCountOne = useCallback(() => setCountOne(countOne + 1), [countOne]);
  const memoizedSetCountTwo = useCallback(() => setCountTwo(countTwo + 1), [countTwo]);
  return (
    <>
      {countOne} {countTwo}
      <Button handleClick={memoizedSetCountOne} name="button1" />
      <Button handleClick={memoizedSetCountTwo} name="button2" />
    </>
  );
};
```
Now, we get the following result when clicking any button:
```
// counter rendered
// button1 rendered
// counter rendered
// button2 rendered
```
By applying memoization to our `Button` component, the prop values passed to it are seen as the same. The two `handleClick` functions are cached and will be seen as the same function by React until the value of an element in the dependency array (e.g., `countOne`, `countTwo`) changes.
## Example of `useMemo`
Let’s look at the following code:
```jsx
import { useState, memo } from 'react';

function ShowValue({ params }) {
  console.log(`ShowValue render, ${params.value}`);

  return <div className="value">{params.value}</div>;
}

const MemoShowValue = memo(ShowValue);

function App() {
  const [counter, setCounter] = useState(0);
  const [value, setValue] = useState('ON');

  console.log(`App re-render, ${counter}`);

  const changeCounter = () => {
    setCounter(counter + 1);
  };

  const changeValue = () => {
    setValue(value === 'ON' ? 'OFF' : 'ON');
  };

  return (
    <div className="container">
      <h1>useMemo Example</h1>
      <div className="items">
        <MemoShowValue params={{ value }} />
      </div>
      <div className="actions">
        <button onClick={changeCounter} className="btn btn-teal">Re-render</button>
        <button onClick={changeValue} className="btn btn-sky">Change Value</button>
      </div>
    </div>
  );
}

export default App;
```
As the code stands, if we click on "Re-render," we’ll see that we have broken our memoization. Although `params` is an object with the same values on each render, every cycle creates a new object. In this case, we need to use `useMemo` to solve this, because it is no longer a primitive type.
Let’s see how this can be solved with `useMemo`:
```js
import { useState, useMemo, memo } from 'react';

// ... code
function App() {
  const [counter, setCounter] = useState(0);
  const [value, setValue] = useState('ON');
  const params = useMemo(() => ({ value }), [value]);

  console.log(`App re-render, ${counter}`);

  const changeCounter = () => {
    setCounter(counter + 1);
  };

  const changeValue = () => {
    setValue(value === 'ON' ? 'OFF' : 'ON');
  };

  return (
    <div className="container">
      <h1>useMemo Example</h1>
      <div className="items">
        <MemoShowValue params={params} />
      </div>
      <div className="actions">
        <button onClick={changeCounter} className="btn btn-teal">Re-render</button>
        <button onClick={changeValue} className="btn btn-sky">Change Value</button>
      </div>
    </div>
  );
}

export default App;
```
Now our `MemoShowValue` works as expected again. We should use `useMemo` for objects and arrays.