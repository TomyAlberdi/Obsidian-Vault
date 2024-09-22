Created: 2024-09-17 17:47
## Family Tree:
1. Computer
2. [[Testing]]
-- -
A **test type** is a group of Testing activities aimed at testing specific characteristics of a Software system, or part of a system, based on specific test objectives.

|                | Functional Testing                                                                                                                                               | Non-Functional Testing                                                                                                                                                                                                                       | Structural Testing                                                                                                                                                                                         | Testing Associated with Change                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Definition     | Functional testing includes tests that evaluate the functions the system must perform. Functions describe what the system does.                                  | Non-functional testing evaluates how well the system behaves.                                                                                                                                                                                | Structural testing is based on the internal structure of the system or its implementation. This structure can include code, architecture, workflows, and/or data flows within the system.                  | There are two types of testing related to changes:<br><br>1. **Confirmation Testing**: After a defect has been fixed, the software is retested using the test cases that failed due to the defect. The goal is to confirm that the original defect has been satisfactorily resolved.<br>2. **Regression Testing**: Changes made to one part of the code (whether fixing a defect or another type of change) may inadvertently affect other parts of the code, either within the same component, in other components of the system, or even in other systems. Regression testing involves running tests to detect these unintended side effects. |
| Implementation | Functional testing observes the software’s behavior.                                                                                                             | Non-functional test design and execution may require special skills and knowledge, such as understanding inherent weaknesses in a design or technology. For example, security vulnerabilities associated with certain programming languages. | Designing and executing structural tests may require specialized skills, such as understanding how the code is constructed, how data is stored, and how to use coverage tools and interpret their results. | In iterative and incremental development cycles (e.g., Agile), new features, changes to existing features, and code refactoring lead to frequent changes in the code, which requires regular change-related testing.                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Test Levels    | Functional tests can be performed at all test levels.                                                                                                            | Non-functional tests can be performed at all test levels.                                                                                                                                                                                    | Structural testing is often performed at the component and integration levels.                                                                                                                             | Confirmation and regression testing are performed at all test levels.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| Scope          | Functional requirements can be detailed in business requirement specifications, epics, user stories, use cases, and/or functional specifications.                | Non-functional testing evaluates characteristics like usability, performance efficiency, or security.                                                                                                                                        | At the component integration level, structural testing may be based on system architecture, such as the interfaces between components.                                                                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Coverage       | Functional coverage is the extent to which a functional element has been exercised by tests and is expressed as a percentage of the type(s) of elements covered. | Non-functional coverage is the extent to which a non-functional element has been tested and is expressed as a percentage of the type(s) of elements covered.                                                                                 | At the component integration level, structural testing may be based on system architecture, such as the interfaces between components.                                                                     | Regression test suites are run many times and usually evolve slowly. As a result, regression testing is a strong candidate for automation. Coverage increases as more functionality is added to the system, requiring more regression tests.                                                                                                                                                                                                                                                                                                                                                                                                    |
## Examples:
### Functional Testing:
- **Component Testing**: Tests are designed based on how a component should calculate the interest payable on a loan.
- **Component Integration Testing**: Tests are designed to verify how the account information captured on the user interface is transferred to the business logic.
- **System Testing**: Tests are designed to assess how account holders can request a line of credit on their checking accounts.
- **System Integration Testing**: Tests are designed to verify how the system uses an external microservice to check the account holder’s credit rating.
- **Acceptance Testing**: Tests are designed to evaluate how a bank employee processes the approval or rejection of a credit application.
### Non-Functional Testing:
- **Component Testing**: Performance tests are designed to evaluate the number of CPU cycles required to perform a complex total interest calculation.
- **Component Integration Testing**: Security tests are designed to check for buffer overflow vulnerabilities as data passes from the user interface to the business logic.
- **System Testing**: Portability tests are designed to verify if the presentation layer functions correctly across all supported browsers and mobile devices.