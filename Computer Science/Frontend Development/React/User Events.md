Created: 2024-09-22 20:10
## Family Tree:
1. Computer
2. Frontend Development
3. [[React]]
-- -
User events are a fundamental pillar in any front-end application. Through them, users can interact with the visual and data layers of the application. This makes our app dynamic and able to respond almost instantly to various user actions.
React allows us to handle events with some specific considerations:
- Event names should use **camelCase**.
- Event handlers should be passed inside curly braces `{}`, instead of a string.
- You must explicitly use the **`preventDefault()`** method if you want to prevent the default behavior. In vanilla JavaScript, you could simply return `false` in the callback.
Since React allows us to pass event handlers directly within JSX, we don’t need to use **`addEventListener`** and **`removeEventListener`** as we do in vanilla JavaScript. React takes care of adding and removing the event according to whether the component is rendered on the screen or not.
## Arguments
In some cases, it may be necessary to pass extra arguments to the function handling the event. See the following example:
```jsx
import React from 'react';

const Posts = () => {
  const postsInfo = [
    {
      id: 1,
      text: 'hello',
    },
    {
      id: 2,
      text: 'world',
    },
  ];

  const deletePost = (id, e) => {
    e.preventDefault();
    console.log(id);
    // .... logic to remove the post
  };

  return (
    <>
      {postsInfo.map(post => (
        <div key={post.id}>
          <p>{post.text}</p>
          <button onClick={e => deletePost(post.id, e)}>Delete Post</button>
        </div>
      ))}  
    </>
  );
};

export default Posts;
```
In this example, we have a list of posts, and each one shows a button that allows deleting it from the list.
Logically, we want to use the **post ID** to filter the list and remove the desired post. For this, we need to pass the ID as an argument to the event handler.
However, since our event handler is simply a function, it's enough to add the argument when declaring it and then pass it when we use it in JSX. This way, we can pass any extra arguments to the handler, in addition to the event, based on our needs.