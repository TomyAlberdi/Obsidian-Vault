Created: 2024-09-26 14:51
## Family Tree:
1. Computer
2. Frontend Development
3. [[React]]
-- -
As we already know, product quality is one of the essential aspects of web application development. Therefore, it's not enough to just learn the tools and technologies that allow us to create an application.
We must also integrate concepts, methodologies, and tools that enable us to produce reliable tests for the product we are developing, ensuring high-quality standards.
Specifically in the field of React, during this class, we will focus on writing tests to verify the proper functioning of our components. To do this, we will use two main tools: **Jest** and **React Testing Library**.
## Jest
Jest is an open-source JavaScript unit testing framework created by Facebook, based on the Jasmine framework. It is the most popular and recommended testing tool within the JavaScript community.
Since Jest is specifically designed for testing, it comes with an assertion library, a test runner, and support for various development frameworks or libraries (such as React).
### Installation:
If we have created our application using **Create React App**, our project is already set up to use Jest, so no additional steps are necessary. For any other case, the installation process is quite simple.
Run the following command in our terminal (inside the project folder):
```sh
npm install --save-dev jest
```
Once installed, add the following script inside the `package.json` file:
```json
{
 "scripts": {
   "test": "jest"
 }
}
```
### Methods:
When using Jest, we have access to various methods and objects in the global environment of our test files. This means we can use them directly without importing them. Let’s review the most important ones.
```js
import { expect, test, describe } from "@jest/globals";
```
#### `expect`:
This method allows us to check a specific value. Generally, it is used together with a **matcher**, which is a method that performs an evaluation on the value inside the `expect`.
To check that the result of a function is what we expect, we use the following syntax:
```js
test('should sum two numbers', () => {
  const number1 = 2;
  const number2 = 3;
  // Invoke the function and store the result
  const result = sum(number1, number2);
  // Use expect to evaluate the result, along with the matcher “toBe”, to check that the result equals 5
  expect(result).toBe(5);
});
```
#### `test`:
This method allows us to wrap each of our tests inside a block. The `test` method takes two arguments: the first is a brief description of the case we want to check, and the second is a function containing our test.
```js
// We use the test method with a brief description of the test case and the block of code that should run to perform the check
test('should sum two numbers', () => {
  const number1 = 2;
  const number2 = 3;
  const result = sum(number1, number2);
  expect(result).toBe(5);
});
```
#### `describe`:
The `describe` method creates a block that groups related tests together. For example, in the previous case, we might want to check that the sum works correctly for negative numbers. In this case, our test could look like this:
```js
describe('sum function tests', () => {

  test('should sum two positive numbers', () => {
    const number1 = 2;
    const number2 = 3;
    const result = sum(number1, number2);
    expect(result).toBe(5);
  });

  test('should sum two negative numbers', () => {
    const number1 = -2;
    const number2 = -3;
    const result = sum(number1, number2);
    expect(result).toBe(-5);
  });
});
```
### Mock:
Let's imagine we're testing an implementation of a `forEach` function, which invokes a callback for each element of a provided array.
```js
function forEach(items, callback) {
  for (let index = 0; index < items.length; index++) {
    callback(items[index]);
  } 
}
```
If we want to write a unit test for the `forEach` function, we need a callback that can be invoked during each iteration. To keep this test isolated, we can use a mock function as the callback and evaluate its behavior to ensure that the callback is invoked as expected.
```js
// We create a mock using the fn() method provided by Jest.
const mockCallback = jest.fn((x) => 42 + x);

// We invoke the function we want to test, passing the mock as the callback
forEach([0, 1], mockCallback);

// With this, we can check that the callback is invoked
// 2 times, once for each iteration.
expect(mockCallback.mock.calls.length).toBe(2);

// We can also check the argument the callback was called with
// during the first iteration.
expect(mockCallback).toBeCalledWith(0);
```
In other words, by using the mock, we eliminate complex dependencies that our function might need to execute.
## React Testing Library
So far, we've reviewed how we can use **Jest** to write our unit tests. As we've seen, testing JavaScript functions is relatively simple and doesn't require interacting with the DOM since we don't have on-screen elements, buttons to press, or complex interactions. But what happens if we want to test these scenarios?
For that, we need a way to “interact” with our **React** components, just like a user would when navigating our application. This is where the second library comes into play: **React Testing Library (RTL)**.
RTL is a set of testing utilities, very popular today, used by companies like Facebook, PayPal, and Autodesk. Its main focus is on allowing us to write tests as closely as possible to how end users interact with the software, ensuring that these tests reflect real usage conditions.
When creating a new React application using **Create React App (CRA)**, everything is already configured by default to use Jest and RTL without any additional setup. It’s worth mentioning that this library was created by **Kent C. Dodds**, one of the leading figures in the JavaScript testing community.
#### Testing React Components
Unlike the previous cases where we worked with functions that returned values, we now have a React component whose job is to render certain information on the screen. What we want to test is the content that appears on the screen — in other words, what the user sees when using the application. The rest of the component’s properties and values are irrelevant to us. This is where RTL shines.
##### Key Features:
1. **Testing the final product**:
   Jest and RTL allow us to test the "final product," meaning the compiled code as seen by the browser and the user. This way, we can simulate how our component will work under different scenarios.
2. **User-Centric view**:
   Since users only see this "version" of the code and have no knowledge of the components or views (as we know them in React), it makes sense that we test the code the same way. That is, as the end user would see it, because they are the ones for whom we are creating use cases, flows, and alternatives to evaluate.
3. **Advantages**:
   In addition to allowing us to test what is displayed on the screen, another benefit of RTL’s approach is that these tests are framework-agnostic. This is a major advantage since the technologies used to build an application might change, but the flow and interaction users have with the application — and what they see on the screen — should remain the same, regardless of the technology used.
##### Basic Syntax:
###### `render()`:
This method renders the component we want to test. We pass a React component to it, and it returns the rendered component within a container that is inserted into `document.body`.
```js
import { render } from "@testing-library/react";

render(<button>Submit</button>);
```
###### `screen`:
This object provides access to various query methods to access the different DOM elements with which we want to interact.
###### Query Types:
Queries consist of a prefix (which determines the return value and when an error should be thrown) and a suffix (which determines the attribute by which the search is executed).
By combining some of the prefixes and suffixes, we can access an element within the container generated by the `render` method:
```js
import { render, screen } from "@testing-library/react";

render(<button>Submit</button>);

const button = screen.getByRole('button', { name: "Submit" });
```
##### Methods:
###### `fireEvent()`:
This method allows us to trigger a DOM event on a particular element, such as a button. Here’s a link to a list of all the events that can be triggered using this method: [DOM Event Map](https://github.com/testing-library/dom-testing-library/blob/11fc7731e5081fd0994bf2da84d688fdb592eda7/src/event-map.js).
```js
import { render, screen, fireEvent } from "@testing-library/react";

render(<button>Submit</button>);
const button = screen.getByRole("button", { name: "Submit" });

fireEvent.click(button);
```
###### `userEvent()`:
This method is provided by the `user-event` library and is used to simulate user interactions with our application, triggering events in a way that closely mimics how users would interact through the browser. While this method allows us to trigger events in a similar way to `fireEvent()`, the main difference is that the events are fired as if a user had interacted with the application via the browser. This helps detect cases where the event might not be triggered by the user, for example, due to a bug.
To use this library, we can call the `setup()` method within each test. We can then trigger the desired event depending on the test case.
```js
import { render, screen } from "@testing-library/react";
import userEvent from '@testing-library/user-event';

test('button click', async () => {
  const user = userEvent.setup();
  render(<button>Submit</button>);
  await user.click(screen.getByRole('button', { name: "Submit" }));
  
  // Add your assertions here...
});
```
##### Matchers:
RTL uses **jest-dom**, a library that provides additional methods for testing certain behaviors in the DOM.
Some of the most commonly used matchers include:
- **`toBeInTheDocument()`**: Checks if a specific element is present in the document.
- **`toBeDisabled()`**: Checks if certain elements (like a button) are disabled from the user's perspective.
- **`toHaveTextContent()`**: Checks if an element contains a specific text.
You can find a list of all the matchers provided by **jest-dom** at the following link: [jest-dom Matchers](https://github.com/testing-library/jest-dom).
##### Example:
Let’s start by defining a simple example of a component to test:
```jsx
import React from "react";

const RaceCar = ({ status }) => {
  const getStatusMessage = () => {
    if (status === "start") {
      return "The car is speeding off";
    } else if (status === "wait") {
      return "The car is ready to start";
    } else {
      return "Please check the race status";
    }
  };

  return <p>{getStatusMessage()}</p>;
};

export default RaceCar;
```
This component receives the parameter `status`, and based on its value, it displays a message about the current state of the race car. The conditions we can test with this are:
- If it receives `"start"` as the value for `status`, it should display the message that the car is speeding off.
- If it receives `"wait"` as the value for `status`, it should display the message that the car is ready to start.
- If it receives any other value, it should display an error message.
###### Writing the test:
To start writing our test, we create a test file where we will import our component. Unlike previous cases where we tested simple functions, now we need to import the `screen` and `render` functions from `@testing-library/react`. Then, we create a `describe` block and an empty test, which will serve as the starting point for testing our component:
```js
import RaceCar from "./RaceCar";
import { render, screen } from "@testing-library/react";

describe("The RaceCar component", () => {
  test("renders correctly", () => {});
});
```
As the first test, we will validate that our component appears on the screen and that the code runs correctly. This would be a basic test for most components. To do this, we first need to render the component using the `render` function, which receives a React component as a parameter. This function loads our component into the virtual environment that Jest creates to evaluate whether our conditions are met. All of this happens behind the scenes, without us actually seeing it on the screen.
```jsx
import RaceCar from "./RaceCar";
import { render, screen } from "@testing-library/react";

describe("The RaceCar component", () => {
  test("renders correctly", () => {
    render(<RaceCar />);
  });
});
```
Once our component is rendered, we need to evaluate that something appears on the screen. Don't forget that every test should have at least one assertion!
To do this, we use the second function we imported: `screen`. This allows us to access or find elements on our "screen" (even though we won't actually see the rendered component, the virtual environment simulates what would appear in the final compiled HTML, CSS, and JavaScript output).
```js
import RaceCar from "./RaceCar";
import { render, screen } from "@testing-library/react";

describe("The RaceCar component", () => {
  test("renders correctly", () => {
    render(<RaceCar />);

    const component = screen.getByText("Please check the race status");

    expect(component).toBeInTheDocument();
  });
});
```
In these two lines, we tell our test to look for an element on the screen that contains the text "Please check the race status". This is the default message our component renders when it does not receive a `status` prop.
The `getByText` function allows us to use regular expressions or strings to search for text. In this case, we use a string.
In the final line of our test, we perform the assertion, indicating that we expect the selected element to be present in the document.
###### Finalizing the tests:
We now have a functional test for a React component. To complete our tests, we need to use different props for our component to simulate other possible use cases. To do this, we simply pass the props we want when rendering the component, since we are writing JavaScript and specifically using React syntax. The logic for writing components and props remains the same.
```js
import RaceCar from "./RaceCar";
import { render, screen } from "@testing-library/react";

describe("The RaceCar component", () => {
  test("renders correctly and shows an error message if no race status is provided", () => {
    render(<RaceCar />);
    const component = screen.getByText("Please check the race status");

    expect(component).toBeInTheDocument();
  });

  test("displays the start message", () => {
    render(<RaceCar status={"start"} />);

    const component = screen.getByText("The car is speeding off");

    expect(component).toBeInTheDocument();
  });

  test("displays the wait message", () => {
    render(<RaceCar status={"wait"} />);

    const component = screen.getByText("The car is ready to start");

    expect(component).toBeInTheDocument();
  });
});
```
### Testing Hooks:
On more than one occasion, we will encounter complex components that not only receive "props" but also implement some logic using hooks. In some cases, these hooks perform simple tasks whose impact on the component occurs relatively immediately. In such cases, we can likely test the behavior of the hooks by evaluating the component's behavior, as we saw in the previous section.
However, there are other situations where hooks become more complex (for example, when making requests to an API or when needing to "re-render" the component with different props). In these cases, testing the behavior of hooks in the traditional way can be a bit complicated.
In such cases, we can use the `renderHook` method provided by **(RTL)**. This method allows us to "emulate" the behavior of any hook so we can test the use cases and expected outcomes. Let's look at an example.
Suppose we have the following hook to handle a counter:
```js
import { useState, useCallback } from "react";

export default function useCounter() {
  const [counter, setCounter] = useState(0);
  const increment = useCallback(() => setCounter((x) => x + 1), []);

  return { counter, increment };
}
```
To test its functionality, we use the `renderHook` method provided by RTL. First, we test the initial state of the counter:
```js
import { renderHook } from "@testing-library/react";
import useCounter from "./useCounter";

test("returns the initial state and the increment method", () => {
  const { result } = renderHook(() => useCounter());

  expect(result.current.counter).toBe(0);
  expect(typeof result.current.increment).toBe("function");
});
```
As we can see, the `renderHook` method returns an object that contains the `current` property. This property, in turn, is an object that holds the latest return value of the hook (in our case, the `counter` variable and the `increment` function). This way, we can test the initial values using assertions.
Similarly, we can evaluate what happens when we update the counter value using the `increment` method:
```js
import { renderHook, act } from "@testing-library/react";
import useCounter from "./useCounter";

test("increments the counter when calling the increment method", () => {
  const { result } = renderHook(() => useCounter());

  act(() => {
    result.current.increment();
  });
  expect(result.current.counter).toBe(1);
});
```
Although this is a simple example, this tool allows us to test much more complex hooks in a reliable and accurate way.