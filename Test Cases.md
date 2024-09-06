#Theory 
A test case is a written document that provides information about what and how to [[Testing|test]].
## Characteristics:
- **Do not assume**:  
    Do not assume the functionality and features of the application while preparing the test case. Be faithful to the specification documents, and in case of doubt, consult the relevant sources.
- **Ensure maximum coverage**:  
    Write test cases for all specified requirements.
- **Autonomy**:  
    The test case should yield the same results regardless of who runs it.
- **Avoid repetition of test cases**:  
    If a test case needs another to be executed first, reference that test case by its ID.
- **Keep it simple**:  
    Test cases should be as simple as possible, as someone other than the author might execute them. Use assertive language to facilitate understanding and ensure faster execution.
- **The title should be strong**:  
    Just by reading the title, any tester should understand the objective of the test case.
- **Consider the end user**:  
    The ultimate goal is to create test cases that meet the client's requirements and are user-friendly.
### What should a Test Case include?
- **Identifier**:  
    It can be numeric or alphanumeric. Most tools generate it automatically.
- **Test case name**:  
    Use a defined naming convention. If none exists, it’s advisable to include the name of the module to which the test case belongs.
- **Description**:  
    It should state what will be tested, the test environment, and the data needed to execute it.
- **Precondition**:  
    An assumption that must be fulfilled before running the test case.
- **Steps**:  
    The actions that must be taken to achieve the expected results.
- **Expected results**:  
    This tells the tester what the expected outcome should be after executing the steps and helps determine whether the test passed or failed.
## Positive and Negative Testing:
- **Positive Testing (+)**:  
    These are test cases that validate the normal flow of a system under test. In other words, flows related to the functional requirements of the system.
- **Negative Testing (-)**:  
    These are test cases that validate flows not covered by the requirements of the system under test.
## Happy Path Testing:
It is the only approach that tests an application through carefully designed test scenarios, which should follow the same flow as the end user when using the application regularly. It is usually the first form of testing performed on an application and is categorized as positive testing. Its purpose is not to find [[Defects|defects]] but to ensure that a product or procedure works as designed.
#### Advantages:
- It is used to understand the basic standards of the application. It is the first test performed.
- It helps determine the stability of the application before proceeding with other levels of testing.
- It helps identify any issues at an early stage, saving effort later on.
#### Disadvantages:
- It does not guarantee the quality of the product because the process only uses positive test scenarios.
- Finding this single path requires extensive knowledge of the application’s usage and the client’s needs.