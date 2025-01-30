Created: 2024-09-26 17:21
## Family Tree:
1. Computer
2. [[Frontend Development]]
-- -
Previously, we saw how to use global states to share information between different components, thereby avoiding the issues that arise from using the method known as **prop drilling**. In this class, we’ll dive deeper into the use of **context** within React, combining it with other tools to maximize its potential.
First, we’ll look at how we can use **localStorage** and **sessionStorage** to store and retrieve information, which we can then use in our context.  
We’ll also introduce the use of **useReducer**, a state management hook that will allow us to manipulate information before storing it in state.
## `localStorage` and `sessionStorage`
As we already know, our browser provides a storage API that allows us to store data locally in the browser, without needing to connect to or access a database.  
For this, we can use **localStorage** or **sessionStorage**, depending on whether we want to persist the data over time (even when the user closes the browser) or just keep it while the session is active.
So, how do localStorage and sessionStorage relate to React? React is just JavaScript, and our application is a web app that runs in a browser. This gives us the ability to use these methods in our app to store information.
### Example application:
For this example, let’s think of a small application that fetches a GitHub profile for a given user. The first time we access this app, we’ll need to make a request to the GitHub API to get the user information. However, once we have this information, we can store it in the browser (using **localStorage**) so that on subsequent visits, the data is shown immediately without needing to repeat the request.
Let’s see how to implement this functionality.
First, we’ll create our context based on what we covered in the previous class, in a `context.js` file:
```jsx
import { createContext, useEffect, useState } from "react";

export const UserContext = createContext();

const UserContextProvider = ({ children }) => {
  return (
    <UserContext.Provider value={{ user, changeUser }}>
      {children}
    </UserContext.Provider>
  );
};

export default UserContextProvider;
```
To use this context within our app’s components, we will wrap the app inside the provider. We’ll do this in the `index.js` file:
```jsx
root.render(
  <StrictMode>
    {/* Wrap our app with the provider to use the context in our components */}
    <UserContextProvider>
      <App />
    </UserContextProvider>
  </StrictMode>
);
```
We’ve now created our context. Next, we’ll work on its content.
In this case, we want to be able to store and share GitHub user information. Additionally, we want to store this information using **localStorage** and retrieve it when the page is reloaded or when the user revisits the app.
To achieve this, we’ll first create two functions to store and retrieve data from localStorage:
```jsx
const getUserFromStorage = () => {
  const localData = localStorage.getItem("user");
  return localData ? JSON.parse(localData) : [];
};

const setUserInStorage = (user) =>
  localStorage.setItem("user", JSON.stringify(user));
```
Inside the provider of our context, we’ll create a state to share this information and update it if we want to change the user. Our provider will look like this:
```jsx
const UserContextProvider = ({ children }) => {
  // Store user information to share with components. The initial value comes from localStorage.
  const [user, setUser] = useState(getUserFromStorage());

  // Update localStorage when the selected user changes.
  useEffect(() => {
    setUserInStorage(user);
  }, [user]);

  // Create a function to update the user.
  const changeUser = (user) => setUser(user);

  return (
    // Share the user and the update function so they can be used by components within the context.
    <UserContext.Provider value={{ user, changeUser }}>
      {children}
    </UserContext.Provider>
  );
};

export default UserContextProvider;
```
Our context is now ready to store user information in localStorage and retrieve it as initial data when the app loads.
The final step is to use the context values inside a component in the app:
We’ll create a simple view that allows us to search for a GitHub user and display their basic information:
```jsx
import { useContext, useState } from "react";
import { UserContext } from "./context";

export default function App() {
  // Access the created context.
  const userContext = useContext(UserContext);
  // Get the user info and the update function.
  const { user, changeUser } = userContext;
  // Create a state to control the input where we’ll search for a GitHub user.
  const [input, setInput] = useState(user.username);

  // Button to search for the user. The click handler will fetch the GitHub API data and invoke the context update function.
  const onClick = async () => {
    const data = await fetch(`https://api.github.com/users/${input}`);
    const json = await data.json();
    const { name, avatar_url, html_url, login } = json;
    changeUser({ name, avatar_url, html_url, username: login });
  };

  return (
    <div className="App">
      <h1>GitHub Profile</h1>
      <div>
        {/* Input and button to search for a GitHub user */}
        <input
          placeholder="Enter username"
          defaultValue={user.username}
          onChange={(e) => setInput(e.target.value)}
        />
        <button onClick={onClick}>View Profile</button>
        {/* Display basic user information and a link to the GitHub profile */}
        <section>
          <h3>{user.name}</h3>
          <h4>{user.username}</h4>
          <img src={user.avatar_url} alt={user.name} />
          <a href={user.html_url} target="_blank" rel="noreferrer">
            View Full Profile
          </a>
        </section>
      </div>
    </div>
  );
}
```
Now we can enter a GitHub username and see the information appear on the screen. Additionally, if we reload the page, we’ll see that the data is retrieved directly from localStorage without needing to make another request to the API.