Created: 2024-09-22 16:59
## Family Tree:
1. Computer
2. Frontend Development
3. [[React]]
-- -
A component is a class or function that returns an HTML component, usually expressed through JSX syntax. Its main purpose is to allow us to break down the user interface into independent, reusable pieces and think about each piece in isolation.
Once defined, it is registered within the application's component tree. Although React focuses heavily on components as a library, the surrounding ecosystem makes it a flexible framework.
## Characteristics
- **Nesting**: One component can be displayed inside another.
- **Reusability**: A well-constructed component can be reused in any application.
- **Customization**: We can customize its content depending on where we use it.
- **Lifecycle**: From its registration, mounting, to when it is "unmounted."
## Class Components vs Functional Components
### Class Components:
The first way to declare a component is by creating it as a JavaScript class. We can see an example in the following code:
```jsx
import React, { Component } from 'react';

class MyComponent extends Component {
  render() {
    return <div>Hello, I'm a class component!</div>;
  }
}

export default MyComponent;
```
To create a class component, we must extend it from `React.Component`, which is the "parent" class that React provides. It acts as a "template" so that our components can be registered and used within our application.  
Our component will have a `render` method, where we need to return the JSX that we want to render whenever we use this component. While there are other specifics associated with class components, the above syntax is the basic one we use to create a class component.
### Functional Components:
As the name suggests, a functional component is nothing more than a function that returns the JSX we want to render for each component, as shown in the following code:
```jsx
function MyComponent() {
  return <div>Hello, I'm a functional component!</div>;
}

export default MyComponent;
```
In this case, we don’t need to use any super class or method to create our component. Simply declaring our function and returning what we want to render is enough.
## Reutilization
As we’ve been seeing, one of React’s main purposes is to create user interfaces through components. This means "breaking down" our application into different parts, with each part represented by a component.  
Similarly, since another goal is to maximize component reuse, we can partition each part of our interface repeatedly, reaching a level that allows us to fully leverage this functionality.
Take a look at the following diagram:
![[Pasted image 20240922170534.png]]
We can begin our partition by dividing the application into two main components: **Header** and **Main**. But, as we see, we could further subdivide the content of **Main** into a reusable **Content** component. In turn, **Content** could be subdivided again into two components: **Text** and **Button**, which can later be reused.
The limit of this subdivision is determined by the needs of our application and our ability to analyze and abstract components that can be reused in various parts of the system.
The creation and use of reusable components require us to consider **Component Architecture**.
### Pure Components:
When talking about component reuse, one of the key concepts we need to keep in mind is **pure components**.
Let’s revisit the concept of a "pure function". A generally accepted definition tells us that a function is "pure" when, given the same arguments, it always returns the same result. Its main characteristic is that it cannot cause any side effects, such as modifying a global variable or altering the state of the application.
If we apply this concept to React, we can say that a component is "pure" when its purpose is purely presentational. In other words, a pure component receives certain props and simply returns a JSX element based on the received information, without generating any side effects. Given the same props, the JSX content returned by the component will always be identical.
When it comes to component reuse, creating components as purely as possible gives us the ability to use them across the entire application without worrying about potential side effects these components might introduce into our code.
## Immutability
The concept of immutability is quite simple to understand: something is immutable when it cannot be modified, and, consequently, something is mutable when it can be modified. Whether we realize it or not, we've already been working with this concept, but because it's transparent to the developer, we might not have noticed that, in JavaScript, we apply both mutability and immutability.
The truth is that in JS, primitive data types such as `string`, `boolean`, `number`, `undefined`, and `null` are immutable. Let's look at an example:
```js
let name = "example 1";
let copyName = name;
copyName = "example 2";
// name = "example 1" and copyName = "example 2"
```
This behavior seems normal, but it occurs because the `string` data type is immutable. Each variable occupies a different memory location, so modifying one doesn't affect the other. On the other hand, examples of mutability in JS include objects and arrays. We can see this in the following example:
```js
let user = {
  name: "name",
  surname: "surname 1"
}
let copyUser = user;
copyUser.surname = "surname 2";
// user.surname = "surname 2" and copyUser.surname = "surname 2"
```
In this case, both objects (mutable data in JS), despite being different variables, share the same memory location. So if one is modified, the other is also affected.
Now, the concept of immutability is frequently applied and used in the world of React. The valuable **props** of React components are read-only objects, meaning they are immutable. Although JS allows us to mutate objects, doing so in the context of the React library would be an error.
Later on, we'll explore what aspects of a component we can mutate and how to do it, but for now, let's stick with the idea that **props are immutable**.
Some advantages of this implementation are:
- **Side-effect free**: With this implementation, we ensure that our objects and components aren't modified in unexpected places, which could affect the execution of our program.
- **Cleaner and more predictable code**.
- **Centralized changes**: Since immutable objects are only assigned once, tracking their value is easier.
- **Easier to test and debug**.
## Component Styles
There are two modern approaches to working with CSS: **CSS Modules** and **Styled Components**.
CSS Modules allow writing styles in files that are consumed as JS objects. They are very popular because they ensure that class and animation names are unique, so you don’t have to worry about selector name collisions.
Styled Components exploit tagged templates introduced by ECMAScript, allowing you to write actual CSS code within your components. This removes the need to map between components and styles.
Although both approaches are valid, we will work with **CSS Modules**, as they use native CSS, meaning that loading these modules happens in parallel and allows us to use pre-processors like SASS or take advantage of caching.
**Example:** We will create different style files for each of the components.
```jsx
import styles from './header.module.scss';

const Header = () => {
  return (
    <header>
      <h1 className={styles.title}>Header</h1>
    </header>
  );
}
```