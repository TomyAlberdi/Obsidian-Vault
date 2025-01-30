Created: 2024-09-17 17:48
## Family Tree:
1. Computer
2. [[Computer Science/Testing/Testing]]
-- -
Since writing, designing, and implementing test cases play a central role in a quality assurance process, we are discovering everything related to these concepts together. Understanding and applying the most widely used Testing techniques in the market gives us a significant advantage as testers when analyzing and covering the functionality of a system under test.
Knowing these testing techniques will also be an advantage in our role as testers, as it will help us certify quality in a software project. Another benefit is the organization it brings when writing test cases from scratch, based on a use case, or from a user story.
The goal of a testing technique is to help identify test conditions, test cases, and test data. The choice of testing technique depends on factors such as:
- Type and complexity of the component or system.
- Regulatory standards.
- Client or contractual requirements.
- Risk classes and levels.
- Testing objectives.
- Available documentation.
- Knowledge and skills of the tester.
- Software lifecycle model.
- Time and budget.
## Classification of Testing Techniques
### Black-box Techniques:
These techniques are based on the behavior derived from analyzing test basis documents (formal requirement documents, use cases, user stories, etc.). They apply to both functional and non-functional tests and focus on inputs and outputs without considering the internal structure.
- **Test conditions**, **test cases**, and **test data** are derived from test bases such as software requirements, specifications, use cases, and user stories.
- Test cases can be used to detect discrepancies between requirements and implementation, as well as deviations from the requirements.
- **Coverage** is measured based on the elements tested from the test basis and the technique applied.
### White-box Techniques:
These are based on the structure derived from documents such as architecture, detailed design, internal structure, or system code. They focus on the internal processing of the test object.
- **Test conditions**, **test cases**, and **test data** are derived from test bases such as code, software architecture, detailed design, or other sources related to software structure.
- **Coverage** is measured by the elements tested within the selected structure (e.g., code or interfaces).
- Specifications are often used as an additional source of information to determine the expected test results.
### Experience-based Techniques:
These leverage the knowledge of developers, testers, and users to design, implement, and execute tests.
## Examples of Testing Techniques
### Black-box Techniques:
**Equivalence Partitioning**: This technique divides data into partitions called equivalence classes, where each member of the class is processed in the same way.
- **Valid equivalence partition** contains values accepted by the component or system.
- **Invalid equivalence partition** contains values rejected by the component or system.
- Partitions can be divided into sub-partitions.
- **Coverage** is measured as:  `Coverage = Tested partitions / Identified partitions`
**Boundary Value Analysis**: An extension of equivalence partitioning, this technique focuses on testing boundaries.
- Identify minimum and maximum boundary values.
- Can use 2 or 3 boundary values.
- **Coverage** is measured as:  `Coverage = Tested boundary values / Identified boundary values`
**Decision Tables**: This technique is used for combinatorial testing, formed by complex business rules that a system must implement.
- Identify **conditions** (inputs) and **actions** (outputs).
- Columns correspond to decision rules, each representing a unique combination of conditions and associated actions.
- **Coverage** is measured as:  `Coverage = Tested decision rules / Total decision rules`.
**State Transition Testing**: A state transition diagram shows the possible states of the software and how it transitions between these states.
- A state transition table shows valid and invalid transitions between states, as well as events and actions associated with transitions.
- **Coverage** is measured as:  `Coverage = Tested states or transitions / Total identified states or transitions`.
### Experience-based Techniques:
- **Error Guessing**: This technique is used to anticipate errors, defects, and failures based on the tester’s knowledge, using past experiences, common developer mistakes, and known failures in related applications.
- **Exploratory Testing**: Testers dynamically design, execute, and evaluate informal tests during test execution, often used when specifications are scarce or time is limited.
- **Checklist-based Testing**: Tests are designed, implemented, and executed based on predefined checklists, which are created using the tester’s experience and knowledge of what is important to the user.