A parameter is a variable (in this case, in the URL) used to receive values. These values can be used within our [[Backend Development|application]].
## Path Parameters
A company has a list of employees, and we want to retrieve the information of these employees according to their ID. If we direct the request to the path `/employees/:id`, it would look like the following example: `http://www.company.com/employees/11`.
We are receiving a value from the client as an unnamed parameter and assigning it the name "id" when receiving it in our route. In the above example, by receiving the value `11`, our router converts it into the `id` parameter, whose value will be `11`.
## Query Parameters
Now, path parameters (path params) are useful up to a point. How can we specify that we want information that meets certain criteria?
Let's suppose we have a virtual store server, and we want to retrieve an item from our collection with the code `"12742"`. The query URL would be: `http://www.mystore.com/items?code=12742
The question mark (`?`) denotes the query component of the URL, which is passed to the server or gateway resource. This query component is combined with the path of the URL, identifying the resource.
Every query always consists of a key and a value. If we want to send more than one, we must separate the pairs with an ampersand (`&`):
`http://www.mystore.com/items?type=book&author=StephenKing`
