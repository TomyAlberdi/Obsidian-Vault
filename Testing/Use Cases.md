Created: 2024-09-17 17:48
## Family Tree:
1. Computer
2. [[Testing]]
-- -
Before designing Test Cases, it's important to analyze the documents that will serve as the basis for generating those test cases. These documents will ensure the client's requirements are met. Typically, these requirements are written as **use cases**. A tester (Testing) must understand what a use case is and how to design test cases from them.
### Differences:
- A **use case** tells the story of how a user interacts with a software system to achieve or abandon a goal. Each use case can contain multiple paths that the user follows, known as **use case scenarios**.
- A **test case** covers the software in more depth and detail than a use case. It includes all the functions that the program can perform and considers all types of input/output data, expected behaviors, and design elements.
## Combining Use Cases with Test Cases:
You can start by writing test cases for the "main scenario" and then for "alternative scenarios." That means writing one or more test cases for each use case scenario. You can break down the parts according to the following table:

| Parts of the Use Case                                                   | Parts of the Test Case         |
| ----------------------------------------------------------------------- | ------------------------------ |
| Name of the Use Case                                                    | Name of the Test Case          |
| Preconditions of the Use Case                                           | Preconditions of the Test case |
| Normal and alternative sequence                                         | Steps of the Test Case         |
| Results in the normal or alternative sequence (Use Case postconditions) | Expected result                |
The ability to create test cases from use cases and trace them to one another is a vital skill in ensuring a quality product.
## Use Case Testing:
Use case testing is a **black-box technique** where the focus is on verifying whether the user's path works as expected. One or more test cases can be created for each behavior detailed in the use cases—covering normal or basic behavior, exceptions, alternatives, and error handling.
Coverage is measured as it follows:
`Tested use case behaviors or paths / Total use case behaviors or paths`
**Key considerations when using this test generation technique:**
- Use case testing alone cannot determine software quality.
- Even though it’s an end-to-end test type, it doesn’t guarantee full coverage of the user application.
- Defects may still be discovered later during integration testing.