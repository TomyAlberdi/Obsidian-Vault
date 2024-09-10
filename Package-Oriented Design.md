#Development 
**Package-Oriented Design** is a popular way to structure projects in [[Go]], where the philosophy is to use packages for composing an application. This allows the developer to know where each package belongs in a Go project.
## Structure
We will divide our application into three parts: **controller**, **service**, and **repository**.
![[image 4.png]]
With this methodology, we will place all controllers in the `handler` layer. The service and repository will be inside the folder of their respective entity.
### Controller:
The controller (or handler) is responsible for receiving the client's request, validating required values, executing various services, and returning a response.

All requests that our web application receives must pass through the controller. It verifies the request and, if it finds an issue, returns a response informing the client. If the request information is correct, the controller forwards the task to the service. Once the service finishes, it returns the response to the client.
### Service:
The service is responsible for performing the main functions of the application: data processing, implementing business logic, and managing external resources.
- **Data processing**: The service receives the data sent through the controller and is responsible for performing the main functions of the application with business logic. We should not send the full request to the service, but only the necessary data for processing and sending a response back to the controller. The controller expects to receive either the data it needs or an error if an issue occurs in the service.
- **External resource management**: The service handles external resources, such as sending requests to an API and receiving a response (either data or an error). If information from the database is needed, the service sends its request to the repository, which handles returning either the necessary data or an error to the service.
### Repository:
The repository is responsible for abstracting data access and interacting with the database.
Whenever the service requires information from the database, it must request it through the repository. The repository performs database operations and returns the information to the service. The service only sends the request, while the repository handles fetching the data from the correct location.
If we need to change the database, we only need to make changes in the repository. This change should not affect the service.
## Example:
![[image 5.png]]
Each employee, for example, would have their own **controller**, **service**, and **repository**. Each package, therefore, would represent an entity.