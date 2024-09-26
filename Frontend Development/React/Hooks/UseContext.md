Created: 2024-09-26 16:18
## Family Tree:
1. Computer
2. Frontend Development
3. React
4. [[Hooks]]
-- -
In the applications we've been working on so far, data was shared between components from top to bottom (from parent components to child components). However, as our application grows, this practice becomes less ideal. It's likely we will start encountering **prop drilling**, bugs, or even performance issues. Additionally, some states need to be available across the entire app (such as geolocation, language, or theme color).
Fortunately, the **Context API** comes to the rescue, allowing us to share information between parts of the app without requiring a specific hierarchy within the component tree.
Thanks to its design, Context allows us to encapsulate data and inject it into components included within that context. To understand this better, we can think of **Context** as a container for components:
- **Values**: Any value defined and updated within the context can be used by the components included in that context.
- **Globality**: While Context provides some global data management, it offers **partial globality**.
- **Scope**: This is a valuable feature because it lets us define the specific scope of global data.
In summary, Context spares us from the hassle of passing data through entire component trees using props. It gives us **years of life** back by simplifying state management.
## Use Cases
- **Theming**: Implementing dark mode or alternative themes.
- **User Authentication**: For registration and login processes.
- **Internationalization**: Managing multiple languages within the app.
## Implementation
1. **Create a context** using the `createContext` method.
2. **Set any value** in the Provider using the `value` property.
3. **Use a context Provider** to encapsulate a component tree.
4. **Access the value** in any encapsulated component using the `useContext()` hook.
### `createContext()`:
A Context object is created by passing a default value to React's `createContext` method. While `createContext` accepts an initial value, it's not mandatory. When creating the context, we obtain two properties: **Provider** and **Consumer**.
```jsx
import { createContext } from "react";
const defaultTitle = "Optional Value";
export const TitleContext = createContext(defaultTitle);
```
### Provider:
The context should be global for the components that consume it, which is why Context provides a **Provider**. This is a component that takes a property called `value`, which is the value provided to the context, and injects it into the components wrapped by it. This value can be anything, including an object with multiple values.
Not all components within the context need to subscribe to it unless they explicitly declare the subscription. This is because not every component may need access to the context data.
When a subscribed component renders, it reads the current context value provided by the **Provider**, so the Provider's responsibility is to give access to the data stored in the context.
```jsx
export const TitleContext = createContext(defaultTitle);

function App() {
  return (
    <TitleContext.Provider value="I am a title">
      <Left />
      <Main />
    </TitleContext.Provider>
  );
}
```
In this way, both component subtrees (`Left` and `Main`) will be able to consume the `TitleContext`.
### Consumer:
For a component to receive the value from a context, it needs to subscribe to it. There are two ways to subscribe: by using the **Consumer Component** or the **`useContext()` hook**.
The Consumer component must include a function as its child or **children**. This function receives the current context value (`value`) as an argument, returns a React node (JSX), and listens for changes.
Think of **Context** as a channel for sharing data. In the component tree, the Consumer sits below the Provider. This function will be called at render time. For each Provider, there will be a corresponding Consumer that interacts with it.
```jsx
import { TitleContext } from './App';

const Main = () => {
  return (
    <TitleContext.Consumer>
      {(props) => {
        return <h1>{props}</h1>;
      }}
    </TitleContext.Consumer>
  );
};
```
### `useContext()`:
To consume context data, we call this hook inside the component that needs it. It takes the context object as its first and only argument and returns the current context value.
Keep in mind that a component using `useContext` will re-render whenever the context value changes. Compared to the Consumer Component, `useContext` provides **better code readability**.
```jsx
import { useContext } from 'react';
import { TitleContext } from './App';

const Main = () => {
  const title = useContext(TitleContext);

  return (
    <div>
      <h1>{title}</h1>
    </div>
  );
};
```
## Example
Step by step guide to implement a dark and light mode switch:
### Create Theme Context:
Next, we create a file named `context.js`, where we define our theme context for light and dark modes. Using `createContext`, we can utilize both the Provider component and the `useContext` hook to consume the context data.
```js
import React, { createContext } from 'react';

export const themes = {
  light: {
    font: 'black',
    background: 'white'
  },
  dark: {
    font: 'white',
    background: 'black'
  }
};

const ThemeContext = createContext(themes.light);
export default ThemeContext;
```
- **Export Themes Object**: Contains light and dark mode colors.
- **Export Context**: Default value set to `light`.
### Configuration in `App.jsx`:
Now, we will configure the context and the theme switching logic in `App.jsx`.
First, the imports:
```jsx
import React, { useState, useMemo } from 'react';
import "./styles.css";
import ThemeContext, { themes } from './context';
```
Then, inside the `App` component, we add state and a function to toggle the theme. We use `useMemo` to optimize the performance by memoizing the theme and the `handleChangeTheme` function.
```jsx
const App = () => {
  const [theme, setTheme] = useState(themes.light);

  const handleChangeTheme = () => {
    if (theme === themes.dark) setTheme(themes.light);
    if (theme === themes.light) setTheme(themes.dark);
  };

  const providerValue = useMemo(() => ({ theme, handleChangeTheme }), [theme, handleChangeTheme]);

  return (
    <ThemeContext.Provider value={providerValue}>
      <Layout>
        <Navbar />
        <Body />
      </Layout>
    </ThemeContext.Provider>
  );
}

export default App;
```
- `useState`: Manages the theme state (defaults to `light`).
- `handleChangeTheme`: Toggles between light and dark themes.
- `useMemo`: Memoizes the theme and change function to prevent unnecessary re-renders.
### Adding components:
Now, let's add some structure to our project by creating three new components: `Navbar.jsx`, `Body.jsx`, and `Layout.jsx`. Create a `components` folder and add these files inside.
Imports:
```jsx
import Navbar from './components/Navbar';
import Body from './components/Body';
import Layout from './components/Layout';
```
Return inside `App` component:
```jsx
return (
  <ThemeContext.Provider value={providerValue}>
    <Layout>
      <Navbar />
      <Body />
    </Layout>
  </ThemeContext.Provider>
);
```
### Components code:
#### `Navbar.jsx`:
```jsx
import React, { useContext } from 'react';
import "../styles.css";
import ThemeContext from '../context';

const Navbar = () => {
  const { theme, handleChangeTheme } = useContext(ThemeContext);
  
  return (
    <div className="navbar">
      <p>Inicio</p>
      <button onClick={handleChangeTheme} style={{ background: theme.background, color: theme.font }}>
        Change Theme
      </button>
    </div>
  );
}

export default Navbar;
```
- `useContext`: Consumes the theme and the `handleChangeTheme` function.
- `onClick`: Switches the theme when the button is clicked.
#### `Body.jsx`:
```jsx
import React from 'react';

const Body = () => {
  return (
    <div>
      <h1>CONTEXT TUTORIAL</h1>
      <p>Lorem ipsum dolor</p>
    </div>
  );
}

export default Body;
```
#### `Layout.jsx`:
```jsx
import React, { useContext } from 'react';
import ThemeContext from '../context';

const Layout = ({ children }) => {
  const { theme } = useContext(ThemeContext);

  return (
    <div style={{ background: theme.background, color: theme.font }}>
      {children}
    </div>
  );
}

export default Layout;
```
### Adding the button:
Lastly, update the button in `Navbar.jsx` to trigger the theme change:
```jsx
import React, { useContext } from 'react';
import "../styles.css";
import ThemeContext from '../context';

const Navbar = () => {
  const { theme, handleChangeTheme } = useContext(ThemeContext);

  return (
    <div className="navbar">
      <p>Inicio</p>
      <button onClick={handleChangeTheme} style={{ background: theme.background, color: theme.font }}>
        Change Theme
      </button>
    </div>
  );
}

export default Navbar;
```