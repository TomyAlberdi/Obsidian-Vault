Created: 2024-09-22 20:27
## Family Tree:
1. Computer
2. Frontend Development
3. React
4. [[Hooks]]
-- -
When it comes to interaction, perhaps the most emblematic case (and the one we will likely encounter most often in our professional journey) is the **form**.
In a form, we can find a variety of events that are triggered as the user interacts with it. In React, HTML form elements work a little differently from other DOM elements because form elements naturally maintain some internal state.
But before diving into how a form works in React, it's important to introduce a concept that will be very helpful for this task: the difference between **controlled** and **uncontrolled** components.
## Controlled vs Uncontrolled Components
- A **controlled component** is one that gets its current value through props and notifies changes via callbacks like `onChange`. A parent component "controls" it by handling the callback, managing its own state, and passing new values as props to the controlled component.
- An **uncontrolled component** is one that stores its own internal state, where the programmer queries the DOM using a `ref` to get its current value when needed.
## `onChange` and `onSubmit`
We will use the example of a **login form**.
For this form, we will use two controlled inputs, using `useState` to store and update the state of each as the user interacts with the inputs. Starting with a basic React project, within the `<App>` component, we will declare two `useState` hooks that we will use later:
```jsx
export default function App() {
  const [userName, setUserName] = useState("");
  const [password, setPassword] = useState("");
}
```
Next, we will need an event handler for each input, which will update the state as the user enters data:
```jsx
const onChangeUserName = (e) => setUserName(e.target.value);
const onChangePassword = (e) => setPassword(e.target.value);
```
With these handlers, we can use the `onChange` event in the `<input>` tag. Now, we also need to create a handler for the `onSubmit` event, which will trigger when the user submits the form:
```jsx
const onSubmitForm = (e) => {
  e.preventDefault();

  // For now, we just display the username
  alert(`Welcome: ${userName}`);
};
```
Now that we have the state and event handlers, we can create our form using JSX:
```jsx
export default function App() {
  return (
    <div className="App">
      <h3>Login</h3>
      {/* Pass the handler to the onSubmit event */}
      <form onSubmit={onSubmitForm}>
        {/* Create two controlled inputs by passing the state as value and the handler to the onChange event */}
        <input
          type="text"
          placeholder="Username"
          value={userName}
          onChange={onChangeUserName}
        />
        <input
          type="password"
          placeholder="Password"
          value={password}
          onChange={onChangePassword}
        />
        {/* Use type to ensure the onSubmit event is triggered when clicking the button */}
        <button type="submit">Submit</button>
      </form>
    </div>
  );
}
```
## Validations
We’ve successfully built a controlled form using React, adding the necessary events to store the input data and handle the form submission via the `onSubmit` event. To complete our learning, we need to revisit a topic we've worked on in this front-end track: **validations**.
In real-world applications, whenever a user submits a form, an exchange of information occurs between the front end and the back end. The front end retrieves the form data and sends it to the back end via a request, with the intent of storing that information or modifying some previously existing data.
This scenario presents the challenge of ensuring that the information we send meets a set of minimum requirements, which vary depending on the specific case. By applying validations to a form, we ensure that the data being sent can be received by the back end without any issues.
Additionally, performing validation before submitting the information helps prevent unnecessary requests when we already know the data won’t be valid. Whether for optimizing resources or ensuring data integrity, we must always ensure proper validations are in place before sending any data to the server.
### When to perform validations:
In practice, there are different moments when input validations can occur in a form:
- **As the user enters data**.
- **When they leave a specific field** (blur event).
- **At the time of form submission**.
Each option has its pros and cons, and the choice depends on the specific case and the strategy to be employed.
### Form validation example:
Let’s return to our login form. In this case, we will implement two types of validation:
1. Ensure the **username** field has at least 3 characters and does not contain leading spaces.
2. The **password** must be at least 6 characters long, with at least one of those characters being a number.
First, we’ll create two functions to handle the validations:
```jsx
const validateUserName = (userName) => {
  // Remove leading and trailing spaces
  const withoutSpaces = userName.trim();
  // Validate length
  if (withoutSpaces.length > 2) {
    return true;
  } else {
    return false;
  }
};

const validatePassword = (password) => {
  // Remove leading and trailing spaces
  const withoutSpaces = password.trim();
  // Split the string into an array to check if there is at least one number
  const passwordAsArray = withoutSpaces.split("");
  // 'Some' returns true if at least one iteration is true
  const hasNumber = passwordAsArray.some((character) => {
    // If the value is NaN, it's not a number
    return !isNaN(character);
  });
  // Validate length and ensure there's at least one number
  if (withoutSpaces.length > 5 && hasNumber) {
    return true;
  } else {
    return false;
  }
};
```
Next, we’ll use these functions to perform validations within the event handler that executes when the form is submitted:
```jsx
const onSubmitForm = (e) => {
  e.preventDefault();

  // Perform validations using the values stored in state
  const isUsernameValid = validateUserName(userName);
  const isPasswordValid = validatePassword(password);

  // If either validation fails, display an error message
  if (!isPasswordValid || !isUsernameValid) {
    alert("Some of the entered data is incorrect");
  } else {
    // For now, just display the username
    alert(`Welcome: ${userName}`);
  }
};
```
In this way, if any of the entered values do not meet the specified validation criteria, an error message will be displayed, and the data will not be sent to the server.