Created: 2024-09-17 17:45
## Family Tree:
1. Computer
2. [[Computer Science/Testing/Testing]]
-- -
There is no single, universal Testing process, but there are common testing activities that help us organize ourselves to achieve established goals.
## Testing Process in context
Some context factors that influence the testing process are:
- Software development lifecycle model and project methodologies in use.
- Levels and types of testing considered.
- Product and project risks.
- Business domain.
- Operational constraints, including but not limited to:
    - Deadlines.
    - Complexity.
## Main Tasks
The software testing lifecycle consists of the following main activities—though they may not always be grouped this way in all software projects:
- **Planning**
- **Tracking and Control**
- **Analysis**
- **Design**
- **Implementation**
- **Execution**
- **Conclusion**
### Planning:
In this activity, objectives and the testing approach are defined within the constraints imposed by the context.
#### Sub-activities:
- Determining scope, objectives, and risks.
- Defining the general approach and strategy.
- Integrating and coordinating activities throughout the software lifecycle.
- Defining the specifications for techniques, testing tasks, people, and resources needed.
- Establishing a test schedule to meet a deadline.
- Producing a test plan.
#### Output Documents:
- General or level-specific test plan.
### Tracking and Control:
This activity aims to gather information and provide feedback and visibility regarding testing activities. As part of control, corrective actions may be taken, such as changing test priorities, schedules, or reevaluating entry and exit criteria.
#### Sub-activities:
- Checking results and test records against specified coverage criteria.
- Deciding whether further testing is needed depending on the required coverage level.
#### Output Documents:
- Test progress report.
### Analysis:
During this activity, the focus is on determining **"what to test."**
#### Sub-activities:
- Analyzing the test basis relevant to the test level considered (design, implementation information, system/component implementation, risk analysis reports, etc.).
- Identifying defects in the test bases (ambiguities, omissions, inconsistencies, inaccuracies, etc.).
- Identifying requirements to test and defining test conditions for each.
- Capturing traceability between the test basis and test conditions.
#### Output Documents:
- Test contracts containing test conditions.
### Design:
During this activity, the focus is on determining **"how to test."**
#### Sub-activities:
- Designing and prioritizing high-level test cases and test suites.
- Identifying necessary test data.
- Designing the test environment and identifying required infrastructure and tools.
- Capturing traceability between the test basis, test conditions, test cases, and test procedures.
#### Output Documents:
- Designed and prioritized high-level test cases.
### Implementation:
In this phase, the necessary testing products are completed for the execution phase, including the sequencing of test cases into test procedures.
#### Sub-activities:
- Developing and prioritizing test procedures.
- Creating test suites from the test procedures.
- Organizing the test suites within an execution schedule.
- Building the test environment and verifying proper configuration.
- Preparing test data and ensuring it is correctly loaded.
- Verifying and updating traceability among the test basis, test conditions, test cases, test procedures, and test suites.
#### Output Documents:
- Test procedures and data.
- Execution schedule.
- Test suite.
### Execution:
During this activity, the test cases are executed.
#### Sub-activities:
- Logging the identifiers and versions of the test elements or objects.
- Executing and recording the test results manually or using tools.
- Comparing actual results with expected results.
- Reporting defects based on expected failures.
- Repeating test activities due to a fix (retest or confirmation testing).
- Verifying and updating traceability among the test basis, test conditions, test cases, test procedures, and test results.
#### Output Documents:
- Defect report.
- Test execution report.