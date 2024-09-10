Static testing is based on manual evaluation of work products (i.e., reviews) or tool-based evaluation of code or other work products (i.e., static analysis). This type of [[Testing]] does not require the software to be executed.
**Static testing** is used to examine any work product, including:
- Specifications, business requirements, functional and security requirements.
- Epics, user stories, and acceptance criteria.
- Architecture and design specifications.
- Code.
- Test work products: plans, cases, procedures, and scripts.
- User manuals.
- Contracts, project plans, schedules, and budgets.
#### Advantages of Early Static Testing:
When applied early in the software development lifecycle, static testing allows for early defect detection, leading to cost and time savings in development and testing. On the other hand, if a defect is found after dynamic testing, fixing it would require code changes, confirmation testing, inclusion in regression testing, and updating associated documentation.
#### Defects Found with Static Testing:
Some defects that are easier and more cost-effective to detect and correct through static testing include:
- **Requirements defects** (inconsistencies, ambiguities, etc.).
- **Design defects** (inefficient database structures, high coupling, etc.).
- **Coding defects** (undefined variables, unreachable or duplicated code, etc.).
- **Deviation from standards** (failure to use coding standards).
- **Incorrect interface specifications** (e.g., different units of measurement).
- **Security vulnerabilities** (e.g., susceptibility to buffer overflow).
- **Traceability or coverage inaccuracies** (e.g., missing tests for an acceptance criterion).
- **Maintainability defects** (e.g., poor component reuse, inadequate modularization).
## Review Process
Within static testing, one way to detect errors is through a **review process**. Reviews involve carefully examining a work product with the primary goal of identifying and removing errors. They can be performed by one or more people.
### Types of Reviews:
- **Formal Reviews**: These have defined roles, follow an established process, and must be documented.
- **Informal Reviews**: These do not follow a defined process and are not formally documented.
The level of formality in the review process is influenced by factors such as the software development lifecycle model, the maturity of the development process, the complexity of the work product being reviewed, legal requirements, and the need for an audit trail.
#### Formal Review Process:
The following table outlines the components of formal reviews: the roles involved, types of formal reviews, implementation techniques, and the activities that should be included.
##### Roles:
- **Author**: Creator of the work product under review, responsible for correcting defects if needed.
- **Management**: Plans and controls the reviews.
- **Facilitator**: Ensures the effective functioning of review meetings and moderates them.
- **Review Leader**: Takes overall responsibility for the review, decides who will be involved, and organizes when and where it will take place.
- **Reviewers**: Identify potential defects in the work product under review, representing different perspectives such as tester, programmer, user, operator, business analyst, or usability expert.
- **Scribe**: Collects potential defects, open issues, and decisions during the review.
##### Types of Formal Reviews:
- **Walkthrough**: Led by the author of the work product; a scribe is required. The use of checklists and individual preparation is optional. It can range from informal to formal, and defect documentation may or may not occur.
- **Technical Review**: Conducted among the author’s technical peers. If a meeting is held, individual preparation is required. A facilitator and a scribe are mandatory, and the scribe ideally should not be the author. Defect logs and review reports are created.
- **Inspections**: Results are formally documented. Individual preparation is required, and defined roles are involved: author, management, facilitator, scribe, reviewers, and review leader. A dedicated reader may also be included. The author cannot act as facilitator, review leader, reader, or scribe. Checklists are used, and defect logs and review reports are produced.
##### Techniques:
- **Ad Hoc**: Reviewers read the work product sequentially and document defects as they find them, with little or no guidance in the process.
- **Scenario-Based and Dry Run**: Based on the expected use of the work product as described in a document, such as a use case.
- **Checklist-Based**: Reviewers identify defects from a set of questions based on potential defects, created from the author’s experience.
- **Role-Based**: Reviewers evaluate the work product from the perspective of different types of users, such as experienced, inexperienced, adults, children, or specific organizational roles like a system administrator or performance tester.
- **Perspective-Based**: Similar to role-based reviews, but reviewers adopt different points of view, such as that of the end user, marketing staff, designer, tester, or operations staff.
##### Activities:
- **Planning**: Define the scope, establish objectives, roles, timing, and deadlines. Define and check entry and exit criteria for more formal reviews.
- **Initiate Review**: Distribute the material and instruct participants.
- **Individual Review/Preparation**: Review the material and take notes of the defects found.
- **Communicate and Analyze**: Communicate defects to those responsible.
- **Correct and Report**: Communicate potential defects found in a review meeting. Create reports of findings, document quality characteristics, and check exit criteria.
## Requirements
One of the key reviews conducted during **static testing** is the examination of **software requirements**. But do we know what requirements are and what types exist?
A **requirement** defines the functions, capabilities, or intrinsic attributes of a software system. In other words, it describes how a system should behave. To say that a system has quality, it must meet both **functional** and **non-functional requirements**.
### Functional Requirements:
These define what a system allows the user to do. These requirements must be explicitly specified. For example:  
_"The amount field only accepts numerical values with two decimal places."_ (Functional and system testing).
### Non-Functional Requirements:
These define the conditions under which the system operates in its environment. Examples include:
- **Usability Requirement**: Usability is defined as the effort a user needs to learn, use, enter data, and interpret results from application software (Usability testing).
- **Efficiency Requirement**: Related to performance in terms of response time, number of operations per second, and other metrics, as well as resource consumption such as memory, processor, and disk or network space (Performance testing, load, stress, scalability testing, memory management testing, compatibility, and interoperability testing).
- **Availability Requirement**: The system's ability to provide service correctly (Availability testing).
- **Reliability Requirement**: The continuity of the service provided by the system (Security testing).
- **Integrity Requirement**: The absence of inappropriate alterations to the system (Security testing, integrity testing).
- **Maintainability Requirement**: The ability to make modifications or repairs to a process without affecting service continuity (Maintenance and regression testing).