Created: 2024-09-17 17:47
## Family Tree:
1. Computer
2. [[Testing/Testing]]
-- -
## Unit or Component Testing
### Specific Objectives:
- Reduce risk.
- Verify that the functional and non-functional behaviors of the component are as designed and specified.
- Build confidence in the component's quality.
- Detect defects in the component.
- Prevent defects from spreading to higher test levels.
### Test Basis:
Some examples of work products that can be used as a test basis include:
- Detailed design.
- Code.
- Data model.
- Component specifications.
### Test Objects:
Common test objects for component testing include:
- Components, units, or modules.
- Code and data structures.
- Classes.
- Database modules.
### Characteristic Defects and Failures:
- Incorrect functionality (e.g., not working as described in the design specifications).
- Data flow issues.
- Incorrect code and logic.
### Approach and Responsibilities:
In general, the developer who wrote the code performs component testing. Developers often alternate between writing code and finding and fixing defects. They typically write and execute tests after completing the component code. In agile development, automated component test cases may be written before the application code.
## Integration Testing
### Specific Objectives:
- Focus on interactions between components or systems.
- Reduce risk.
- Verify that the functional and non-functional behaviors of interfaces are as designed and specified.
- Build confidence in the quality of interfaces.
- Detect defects in interfaces, components, or systems.
- Prevent defects from spreading to higher test levels.
### Test Basis:
- Software and system design.
- Sequence diagrams.
- Interface specifications and communication protocols.
- Use cases.
- Component or system-level architecture.
- Workflows.
- External interface definitions.
### Test Objects:
- Subsystems.
- Databases.
- Infrastructure.
- Interfaces.
- Application programming interfaces (APIs).
- Microservices.
### Characteristic Defects and Failures:
- Incorrect or missing data.
- Incorrect sequencing or synchronization of interface calls.
- Interface incompatibility.
- Failures in communication between components.
- Untreated or incorrectly treated communication failures.
- Incorrect assumptions about the meaning, units, or boundaries of data transmitted between components.
### Approach and Responsibilities:
Integration testing focuses on proper integration. It can use functional, non-functional, and structural testing techniques. This is generally the responsibility of testers.
## System Testing
### Specific Objectives:
- Reduce risk.
- Verify that the system's functional and non-functional behaviors are as designed and specified.
- Validate that the system is complete and will function as expected.
- Build confidence in the overall system quality.
- Detect defects.
- Prevent defects from spreading to higher test levels or production.
### Test Basis:
- System and software requirements (both functional and non-functional).
- Risk analysis reports.
- Use cases.
- Epics and user stories.
- System behavior models.
- State diagrams.
- System and user manuals.
### Test Objects:
- Applications.
- Hardware/software systems.
- Operating systems.
- System under test (SUT).
- System configuration and configuration data.
### Characteristic Defects and Failures:
- Incorrect calculations.
- Incorrect or unexpected system functional or non-functional behavior.
- Incorrect control and/or data flows within the system.
- Inability to properly and completely perform end-to-end functional tasks.
- Failure of the system to operate correctly in production environments.
- Failure to function as described in system and user manuals.
### Approach and Responsibilities:
System testing focuses on the overall, end-to-end behavior of the system, both functional and non-functional. Independent testers typically conduct system testing.
## Acceptance Testing
### Specific Objectives:
- Similar to system testing, it focuses on the behavior and capabilities of the entire system or product.
- Build confidence in the overall system quality.
- Validate that the system is complete and will function as expected.
- Verify that the system's functional and non-functional behaviors meet the specified requirements.
### Test Basis:
- Business processes.
- User or business requirements.
- Regulations, legal contracts, and standards.
- Use cases.
- System requirements.
- System or user documentation.
- Installation procedures.
- Risk analysis reports.
### Test Objects:
- System under test.
- System configuration and configuration data.
- Business processes for a fully integrated system.
- Disaster recovery systems (for business continuity and disaster recovery testing).
- Operational and maintenance processes.
- Forms.
- Reports.
- Existing and transformed production data.
### Characteristic Defects and Failures:
- System workflows that do not meet business or user requirements.
- Incorrect implementation of business rules.
- Failure to meet contractual or regulatory requirements.
- Non-functional failures, such as security vulnerabilities, poor performance under high loads, or improper operation on supported platforms.
### Approach and Responsibilities:
Acceptance testing is often the responsibility of customers, business users, product owners, or system operators. Other stakeholders may also be involved. Acceptance testing is typically considered the final level of testing in a sequential development lifecycle.