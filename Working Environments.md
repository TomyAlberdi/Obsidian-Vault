#Theory 
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