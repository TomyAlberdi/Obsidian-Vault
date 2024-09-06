#Theory 
Component testing or unit testing is the [[testing]] of individual software components. They are small tests created specifically to cover all code requirements and verify their results. [[Testing Techniques#White-box Techniques|White box]] techniques are used to generate these tests.
Unit tests are generally automated tests written and executed by software developers to ensure that a section of an application - known as the “unit” - complies with its design and behaves as intended.
The general process for the creation of these unit tests consists of three parts:
1. **Agreement or acceptance criteria** where the requirements to be met by the main code are defined.
2. **Writing the test**, the process of creation, where the results to be analyzed are accumulated.
3. **Confirmation** is considered the moment in which we check if the grouped results are correct or incorrect. Depending on the result, it is validated and continued, or repaired, so that the error disappears (debug).
## Unit:
A unit can be almost any part of the code you want: a line of code, a method or a class. In general, the smaller the better. Smaller tests provide a much more granular view of how the code is performing. There is also the practical aspect that when you test very small units, you can run them quickly.
## Frameworks for Unit Testing
It is a tool that provides an environment for unit or component testing in which a component can be tested in isolation or with appropriate stubs and drivers. It also provides other support for the developer, such as debugging capability.
For example, to perform component testing of code done in JavaScript you can create a framework based on the following tools:
- Mocha
- Chai
## NPM
npm is the default package management system for Node.js. When we refer to “packages” what we are referring to is code packages that will live in a folder called “node_modules” and will have a configuration that will call them inside a file called “package.json”.
This is generated when starting a project with the command “npm init” having previously downloaded node.js.
This configuration will contain valuable information for the project, for example:
- The author
- The title of the project
- The license
- The repository
- The dependencies
- Scripts
- Test
Among others.
## Conclusion:
Node.js is used to run server-side JavaScript, which has a package manager called npm that has a giant community that constantly uploads its code packages to share with others and through a few commands, they can use those code packages in their projects.