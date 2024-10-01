Created: 2024-10-01 16:02
## Family Tree:
1. Computer
2. [[Infrastructure Administration]]
-- -
**DevOps** is the combination of philosophies, practices and tools that increases the speed at which an organization delivers applications and services. This approach enables companies to improve their products at a faster pace than those using traditional development and infrastructure management processes. This speed allows organizations to deliver more value to their customers and become more competitive in the market.
In the DevOps culture, development teams (**Dev**) and operation teams (**Ops**) do not work separately; instead, they communicate constantly. Sometimes, these teams merge into a single unit that works across the entire application lifecycle, from development and testing to deployment and operations. In some cases, **quality** and **security** are also integrated with development and operations.
These teams focus on automating processes that were historically manual and slow. To achieve this, they use a stack of technologies and tools that helps them operate and evolve applications quickly and reliably. Moreover, DevOps practices allow individuals to perform tasks that would typically require a combination of serveral people, such as deploying code or provisioning infrastructure.
## Steps for software development
### Codification Process:
This phase involves converting what was defined and designed into **source code**, using a specified programming language. Here’s a breakdown of the process:
1. **Cloning and Local Development**:
    - The programmer **clones a remote repository** to their local environment and begins working on the code.
    - Local tests or tests within containers are typically run during this phase. The developer integrates the new code with existing functional code.
2. **Branching Strategy**:
    - Based on the chosen **branching strategy**, the code is pushed back to the remote repository for **peer review** by another colleague.
### Automated Processing (Initial Testing and Compilation):
Once the new code is approved, it moves to another repository, triggering a series of **automated processes**, which may be sequential or parallel. These processes often include:
- **Syntax testing**: Ensuring there are no syntax errors in the code.
- **Indentation formatting**: Formatting the code for readability.
- **Vulnerability scanning**: Scanning the code for potential security risks.
Following these checks, the code moves to a **build station**, where it is **compiled** (translated from the programming language into machine code), generating a series of **artifacts**. These artifacts may include:
- Executable files
- Libraries
- Configuration files
### Testing:
Once artifacts are produced, they move into the **testing environment**, where various types of tests are conducted:
1. **Functional Tests**:
    - **Unit tests**: Test individual units of code.
    - **Integration tests**: Check how different pieces of code work together.
    - **Regression tests**: Ensure that new changes don’t break existing functionality.
    - **UAT (User Acceptance Testing)**: Validates the software from the user's perspective.
2. **Non-Functional Tests**:
    - **Performance testing**: Ensures the system meets performance standards.
    - **Load testing**: Checks how the system behaves under expected load.
    - **Reliability testing**: Ensures the system is reliable over time.
    - **Stress testing**: Determines how the system performs under extreme conditions.
Testing continues until all tests are passed successfully. **Automatic notifications** are often sent to relevant stakeholders, informing them of the results.
### Artifact Storage:
After successful testing, the artifacts are stored in an **artifact repository**. These repositories are organized so that artifacts can be easily retrieved via **API calls** whenever necessary.
This storage ensures that the artifacts are:
- Accessible for future deployment or usage.
- Organized for quick retrieval based on version, project, or other metadata.
This entire process streamlines the workflow in a **DevOps** environment, ensuring that the code moves efficiently from development to deployment, with each step automated and verified through rigorous testing and artifact management.