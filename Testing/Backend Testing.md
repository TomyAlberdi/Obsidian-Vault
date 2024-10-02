Created: 2024-10-02 18:11
## Family Tree:
1. Computer
2. [[Testing/Testing|Testing]]
-- -
A typical web application consists of three layers: the user interface (UI), business logic, and a database. Testing the user interface, or front end, involves validating the parts of the application that are visible to end users, such as forms, menus, navigation, etc. On the other hand, back-end testing deals with all the elements that users cannot see (business logic and database).
Back-end testing ensures that the data contained in an application’s database and its structure meet the project's requirements.
## API Testing
At a high level, our job is to understand how the API works, create a good combination of input parameters, run tests against the API, verify the result, and report any deviations from the expected functionality. These tests involve making HTTP requests (GET, POST, PUT, and DELETE) and then verifying the response.
## HTTP
The **Hypertext Transfer Protocol** (HTTP) is a simple client-server protocol that organizes the exchange of information between a server and an application that consumes these services. This communication is made possible by HTTP methods, which allow us to send and receive information. In the following video, we will explore these concepts more deeply along with some examples.
### HTTP Status Codes:
- **200:** This is the code returned when a webpage or resource behaves exactly as expected.
- **201:** The server has successfully fulfilled the browser's request, and as a result, a new resource has been created.
- **204:** This code means the server successfully processed the request but will not return any content.
- **300:** (Used for redirection purposes, typically a range of redirection codes.)
- **301:** This code is returned when a webpage or resource has been permanently replaced by a different resource.
- **302:** This code is used to indicate that the requested resource was found, but not in the location where it was expected.
- **400:** The server cannot return a response due to a client-side error.
- **401:** This is returned by the server when the targeted resource lacks valid authentication credentials.
- **403:** This code is returned when a user attempts to access something they do not have permission to view.
- **404:** This code means the requested resource does not exist, and the server doesn't know if it ever existed.
- **500:** This is a generic code that simply means "internal server error." Something went wrong on the server, and the requested resource was not delivered.
- **503:** This code may be returned by an overloaded server that cannot handle additional requests.