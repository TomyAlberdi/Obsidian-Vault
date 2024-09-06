#Theory 
When developing software, we’ll realize that finishing the project doesn’t mean the work is done. Eventually, the project will be released, and the client will start using it. Everything should work well, but what happens if an unexpected change needs to be made, or if an error is discovered that requires fixing? We can’t make changes directly in the environment where the client is using the software, as we risk breaking it and rendering it inoperative.
This is why different **working environments** must exist, where changes can be developed and [[Testing|tested]] before reaching the client’s environment.
A **[[Working Environments|working environment]]** refers to the setup with all the necessary resources to run a system. In this part of the subject, we will learn how different tests are organized across environments, understanding which tests to use and where they should be executed.
## Types of Testing by Workspace
In the following section, we will not cover the **PROD** environment because:
- Testers generally do not have access to this environment.
- If they do have access and perform tests:
	-  Actions that generate data should not be performed.
    - There is a risk of entering junk data.
    - It may interfere with tracking cases.
### DEV Environment:
- Unit or component testing.
- Integration testing.
### QA Environment:
- Functional testing.
- Use case testing.
- Accuracy testing.
- Suitability testing.
- System testing.
- Regression testing.
- Confirmation testing.
- Sanity testing.
- Smoke testing.
### UAT Environment:
- Acceptance testing.
- Exploratory testing.
- Usability testing.
- Accessibility testing.
### STG Environment (Preproduction):
- Maintenance testing.
- Security testing.
- Performance testing.
- Load, stress, and scalability testing.
- Infrastructure testing.
- Memory management testing.
- Compatibility testing.
- Interoperability testing.
- Data migration testing.