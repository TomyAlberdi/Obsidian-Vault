Created: 2024-09-22 15:26
## Family Tree:
1. Computer
2. [[Frontend Development]]
-- -
React is a declarative and flexible JavaScript library used to create user interfaces. It is open-source and free, maintained by Facebook and a community of companies and individual developers.
React can be used to develop mobile applications (with React Native) or single-page applications known as SPAs (Single Page Application).
With React, user interfaces are built from smaller, isolated pieces of code that we call components. From these pieces, we can compose large and complex user interfaces that function as a single system.
Among its many advantages, its implementation allows the application to load faster and more efficiently.
## State update
- Fewer backend loads.
- No page reloads.
State is a representation of the system at a given moment. It refers to the data stored in the application in the form of strings, arrays, objects, etc. Each time a user changes something, an event is triggered, or whenever the backend injects data into the browser, the application's state changes with new values.
Managing state with vanilla JS, HTML, and CSS would be a very error-prone and costly task to maintain, as you would constantly have to track everything that changes and propagate those changes throughout the interface.
To improve performance in cases where updating the DOM is necessary, React maintains a "virtual copy" of it in order to compare the changes and re-render only the parts that have changed.
## JSX
An essential feature of React is that the interface of components is expressed using JSX, which is a declarative XML-like syntax that is used internally in JavaScript but resembles HTML tags. This is why React functions as a JavaScript library.
## Project creation
Nowadays, we have tools that allow us to create an entire template for our project by running just two commands. In seconds, we will have a React-integrated template ready to start development.
There are two major options for creating these templates:
- On one hand, we have **Create React App** (CRA), created by Facebook (also the creator of React), which has been around for years.
- On the other hand, there's **Vite**, a relatively "new" alternative that came to innovate and address some of the shortcomings left by CRA.
Both **Create React App** and **Vite** are excellent alternatives for starting our React projects quickly and efficiently. Choosing one or the other is up to the developer.
Vite is fast, but it doesn’t come pre-configured with things like Jest. So, if we wanted to write our tests, we would need to manually set up the environment ourselves. On the other hand, with CRA, we could start writing tests immediately.
However, it's a fact that **esbuild** (the bundler used by Vite) is currently far superior to **webpack** (used by Create React App) and many other options on the market. Therefore, when working with large projects, its superiority in terms of performance and speed is remarkable, leaving the competition behind. If speed is our priority, **Vite** is the go-to choice.
### Vite
Although the ultimate goal of Vite is the same as that of CRA, there are certain differences to consider when choosing between the two. Behind the scenes, Vite uses very different tools compared to CRA. While the end goal is the same, the approach is different. By default, Vite comes with the following pre-configured features:
- **Esbuild**: A transpiler and bundler similar to Babel and Webpack combined, but much more efficient and faster.
- **TypeScript support by default**: No need to configure any extra settings.
- **Native support for CSS preprocessors by default**.
- **HMR (Hot Module Replacement)**: Vite tracks which part of our project has been modified and updates only that section in isolation, without needing to reload the entire page.
Unlike CRA, Vite doesn’t come with pre-configured options like ESlint or Jest. However, what it lacks in extra features, Vite makes up for with speed. This is one of the key differences with CRA: Vite is fast, _very_ fast (its name even means "fast" in French).
#### Usage and installation
To create a Vite project, we only need Node.js (with npm) installed on our computer and run the following command in the terminal: `npm create vite`.
Automatically, the terminal will show us the different options for configuring our project with Vite. First, we choose the project name, then the library (because Vite is not only for React), and finally, whether we want to add TypeScript or just use JavaScript.
Next, we install dependencies with: `npm install`.
At this point, our project will be ready to start coding. The folder structure will look like this:
![[Frontend Development/React/attachments/image.png]]
As we can see, Vite’s structure comes with much less unnecessary clutter and is much cleaner. This is a plus when developing, as we won’t waste time deleting unnecessary files. Unlike CRA, Vite initializes all pages in the `main.jsx` file. Its functionality is exactly the same as what CRA does in `index.js` and `<App />`, so to see changes in our web app, we need to add or modify `App.jsx`.
To see our project in action, we just run the following command and follow the link displayed in the terminal: `npm run dev`.
## Cheat Sheet

| Command               | Usage        |
| --------------------- | ------------ |
| `npm install -D sass` | Install SASS |
[Deploy React Vite SPA to GitHub Pages with GitHub Actions tutorial](https://www.youtube.com/watch?v=MKw-IriprJY).
```html
<script type="text/javascript">
    (function(l) {
        if (l.search[1] === '/' ) {
          var decoded = l.search.slice(1).split('&').map(function(s) {
            return s.replace(/~and~/g, '&')
          }).join('?');
          window.history.replaceState(null, null,
              l.pathname.slice(0, -1) + decoded + l.hash
          );
        }
      }(window.location))
  </script>
```