Created: 2024-09-17 16:22
## Family Tree:
1. Computer
2. [[Infrastructure Administration]]
-- -
Test execution is carried out in different workspaces depending on the stage of the development cycle the system is in, whether it's under construction or maintenance. These workspaces are known as **environments**. In other words, environments refer to servers with specific assigned resources, installed software and libraries, their own database, and a specific configuration.
This setup allows for the secure development of applications with separate environments for programming, testing, sharing results with clients, and enabling them to conduct tests and trials. Ultimately, this ensures a robust and stable application is deployed.
Each environment serves a specific purpose and offers certain advantages at different stages of the work process.
## Levels of Environments
- **Development Environment (DEV)**:  
    This is where the programmer develops the application code, runs initial tests, and checks if the application runs correctly with the new code. This environment can be local or cloud-based, depending on the project’s needs.

- **Testing Environment (QA)**:  
    The QA environment is typically hosted on a cloud server or a local server farm (laboratory). It helps minimize issues later on since testers perform the initial functionality tests in this environment.

- **User Acceptance Testing Environment (UAT)**:  
    The UAT environment allows client users to verify that the implemented changes are what they requested, while also assessing accessibility and usability.

- **Preproduction Environment (STAGE)**:  
    This environment should have the same technical configuration as the production environment. Its primary purpose is to simulate the production environment to test updates and ensure they won’t corrupt the application when deployed on the production servers. This minimizes system downtime and service interruptions.

- **Production Environment (PROD)**:  
    This is the environment where the application is finally run, where end users access it, and where real business data is processed. It has the same characteristics and configuration as the preproduction environment. However, it may involve multiple servers for load balancing in applications that need infrastructure capable of handling heavy user traffic and thousands of concurrent connections.
## Environment Variables
An **environment variable** is a dynamic value that the operating system and other programs can use to determine specific information about your computer.
In other words, an environment variable represents something else, such as a location on the computer, a version number, a list of objects, a user, or a password. It is also a dynamic variable that can affect the behavior of running processes on a computer.
Typically, these values refer to common system files, directories, and functions whose specific path may vary, but which other programs need to be aware of.
A very popular way to configure environment variables is through **`.env` files**, also colloquially called "dotenv files" or just "dotfiles." In fact, many technologies today support this type of file: IDEs, Docker, and some web frameworks are just a few examples.