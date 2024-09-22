Created: 2024-09-22 17:55
## Family Tree:
1. Computer
2. Frontend Development
3. [[React]]
-- -
So far, we’ve seen what a component is and how it can be reused to streamline our workflow. But what if we want the content of the component to be dynamic?
**Props** are the internal data of a component. They represent information that is sent at the moment a component is used. Props allow the internal information of a component to be variable so that we can have truly dynamic and reusable HTML structures.
## Key features
- **Immutable**: Props are generated in the parent component when attributes are passed to the children. Therefore, the child component cannot modify them.
- **Received**: Children receive and use them.
- **Facilitate reuse**.
- **Passed to the child component when it is created**.
## Prop `children`
When working with React, we can create components that act as generic boxes or containers for other components. In such cases, we might want to use these containers in different parts of our application. The challenge is that when creating the containers, we don’t know in advance what their children will be (since this will depend on each specific use case).
To solve this issue, React provides a special prop known as **children**. This prop allows us to pass child elements directly when invoking the container component. This way, we can arbitrarily nest our components using generic containers. Let’s look at an example:
```jsx
const Father = (props) => (
  <div>
    <h5>I'm a father</h5>
    {props.children}
  </div>
);
```
As you can see, inside the `<Father />` component, we have an `<h5 />` tag followed by `props.children`. This indicates that any component we nest inside `<Father />` will appear after the text "I'm a father."
Then, when we use the `<Father />` component in our application, we add the `<Son />` component inside it:
```jsx
const Son = () => <p>I'm a son</p>;
// Rendering in the app:
<Father>
  <Son />
</Father>
```
This will result in the following interface:
```
Soy un padre
Soy un hijo
```
## Fragment
Just as we may want to nest one component inside another, there may be cases where we want to return several components at the same level. For example, we might have a component called `Columns` like the following:
```jsx
const Columns = () => (
  <td>Hello</td>
  <td>World</td>
);
```
If we try to use this component, we’ll get an error because React only allows each component to return a single JSX element as its "parent." To resolve this, we could group our `<td />` tags inside a common container, like this:
```jsx
const Columns = () => (
  <div>
    <td>Hello</td>
    <td>World</td>
  </div>
);
```
The issue here is that we are unnecessarily creating empty HTML tags in each case. Here’s another example where we "group" the `<span />` and `<p />` tags inside a `<div />`:
```jsx
const Example = () => (
  <div>
    <span>Hello</span>
    <p>World</p>
  </div>
);
```
When inspecting the DOM, we would see the following tags:
```html
<div>
  <span>Hello</span>
  <p>World</p>
</div>
```
As you can see, a `<div>` tag was created solely to group each rendered element. While this isn’t a serious problem, it adds unnecessary content to our application and can make it harder to inspect when needed.
To solve this, React provides the `<Fragment>` tag, which allows us to group elements without creating extra nodes (like we saw earlier). Let’s revisit the previous example, but this time replace the `<div>` tag with `<Fragment>`:
```jsx
import { Fragment } from 'react';

const Example = () => (
  <Fragment>
    <span>Hello</span>
    <p>World</p>
  </Fragment>
);
```
If we inspect the application again, we get the following result:
```html
<span>Hello</span>
<p>World</p>
```
As you can see, we get fewer lines and a more readable code structure.
There are two ways to use **Fragment**:
1. The syntax we saw earlier, using the `<Fragment>` tag, which we can import from React.
2. The shorthand syntax, represented by `<>` and `</>`:
```jsx
const Example = () => (
  <>
    <span>Hello</span>
    <p>World</p>
  </>
);
```
## Prop key + `map()`
Let's now introduce two elements that go hand-in-hand and are widely used in the world of programming with React. As we may have guessed, we're talking about the `key` property and the `map()` method.
Imagine we have an array of characters, and for each one of them, we want to render a card element in our app. Since the information is stored in an array, we can use the `map()` method to go through the entire list of characters and return a card for each one of them.
However, with this solution, we must be cautious about one aspect. Although each of our characters has a different name, for React and the Virtual DOM, they are all exactly the same. Therefore, if a change occurs in one of them (for instance, if the user deletes or modifies one of the characters), React will change all of them instead of keeping the rest intact. To solve this problem and prevent performance issues in our app, we have the `key` property. Although it's called a property and is assigned the same way props are assigned to a component, they are entirely different concepts. The ultimate goal of this attribute is not to pass any information to the component being rendered, but it will only be used by React to identify each element as unique. We can think of it as an ID for our component.
### Example:
Character array:
```json
const characters = [
  {name: "Mr. Poindibags", isImpostor: true},
  {name: "Bombom", isImpostor: false},
  {name: "Tito", isImpostor: false},
  {name: "X-Ray", isImpostor: false},
  {name: "Fixfox", isImpostor: false},
];
```
`map()` method to iterate over the array and create components:
```jsx
let characterComponents = characters.map(
  character => <CharacterStatus {...character}/>
);
```
The expression `{...character}` expands the information within each character and passes it as props to the component.
If we leave the code like this, React will throw a warning about the missing keys. When adding keys, it's important to note that they must be unique among sibling elements, but not globally. For this, we can use the `index` parameter of the `map` method as the key:
```jsx
let characterComponents = characters.map(
  (character, index) => <CharacterStatus key={index} {...character}/>
);
```