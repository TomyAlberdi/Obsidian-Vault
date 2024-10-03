Created: 2024-09-28 00:52
## Family Tree:
1. Computer
2. Programming Theory
3. Object-Oriented Programming
4. [[Programming Theory/Object-Oriented Programming/Design Patterns/Design Patterns]]
-- -
## Pattern Model, View, Controller
### Advantages:
- Separates the logic of the application (**Model**) from its representation (**View**).
- Facilitates **code reuse**.
- Simplifies development by organizing each layer independently.
- Increases **development speed** in team environments.
- Makes **unit testing** easier.
### Components
#### Model:
- Contains the **application logic**.
- Responsibilities: connecting to the database, performing queries, and managing what is known as **business logic**.
- The model does **not communicate directly** with the views.
#### View:
- Represents the graphical user interface (GUI) of the application, containing all elements visible to the user.
- Users interact with the view by sending and requesting information from the server.
- Responsibilities: defining the appearance of data and displaying it on the screen.
- The view does **not communicate directly** with the model.
#### Controller:
- Acts as the **intermediary layer** between the views and models.
- Responsibilities: processing data received from the models and selecting the appropriate view based on that data.
- It directly interacts with both the views and the models, making it a **critical component** in the MVC flow.
### How MVC works:
- **View** connects to the **Controller** to request data.
- **Controller** receives the request, validates the data, and then asks the **Model** for the requested information.
- **Model** retrieves the requested information and sends it back to the **Controller**, which in turn passes it to the **View** for display.
The MVC pattern efficiently organizes the structure of an application by keeping data handling, user interface, and control logic separated, which improves maintainability and scalability.