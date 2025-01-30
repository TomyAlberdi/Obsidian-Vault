Created: 2024-09-17 17:38
## Family Tree:
1. Computer
2. [[Computer Science/Testing/Testing]]
-- -
## Quality
What do we mean when we talk about quality in testing? It refers to the degree of customer satisfaction. It involves meeting their expectations and fulfilling them without exceeding time and budget.
So, if we meet their requirements beyond their expectations, are we talking about quality? In this scenario, it wouldn't be considered quality, as we would be allocating more resources than necessary, thereby reducing quality.
### Validation and Verification:
- **Validation**: This refers to matters that a business/functional analyst must confirm with the client, ensuring a clear understanding of the needs before moving on to execution itself.  
    _Are we building the right product?_
- **Verification**: This refers to quality control over a product, service, or deliverable. In this case, we can say it involves comparing the output with business requirements to check if what was planned and analyzed matches what was actually achieved.  
    _Are we building the product correctly?_
## 7 Principles of Testing
1. **Testing shows the presence of defects, not their absence**:  
    It cannot prove there are no defects. It reduces the likelihood of undiscovered defects in the software, but even if none are found, the testing process is not proof of correctness.

2. **Exhaustive testing is impossible**:  
    It is not possible to test everything—all input combinations and preconditions—except in trivial cases. Instead of trying for exhaustive testing, risk analysis, testing techniques, and priorities should be used to focus testing efforts.

3. **Early testing saves time and money**:  
    To detect defects early, both static and dynamic testing activities should begin as early as possible in the software development lifecycle to help reduce or eliminate costly changes.

4. **Defects are clustered**:  
    Generally, a small number of modules contain the majority of defects found during pre-release testing or are responsible for most operational failures.

5. **Beware of the pesticide paradox**:  
    If the same tests are repeated over and over, eventually, these tests will no longer find new defects. To detect defects, it may be necessary to change existing tests and test data.

6. **Testing is context-dependent**:  
    For example, critical safety control software for industrial systems is tested differently from a mobile e-commerce application.

7. **Absence of errors is a fallacy**:  
    The success of a system is not solely dependent on finding and fixing errors until none remain. There may be no errors, but other problems can still exist. There are other variables to consider when measuring success.
## Psychological Aspect of Testing
Testing is the process of executing a program with the intention of finding errors. Human beings tend to be highly goal-oriented, and setting the right goal has a significant psychological impact. If our goal is to demonstrate that a program has no errors, we will subconsciously be driven toward that goal. In other words, we tend to select test data with a low probability of causing the program to fail.
On the other hand, if our goal is to demonstrate that a program has errors, our test data will be more likely to find them.
Beyond the developer or tester, testing tasks can be performed by people in a specific testing role or another role, such as clients.
### Independent Testing:
The way testing independence is implemented varies depending on the software development lifecycle model. For example, in agile development, testers can be part of a development team. In some organizations that use agile methods, these testers can also be considered part of a larger, independent testing team. Additionally, in such organizations, product owners may perform acceptance testing to validate user stories at the end of each iteration.
##### Potential Benefits of Independent Testing:
- Independent testers are likely to identify different types of failures compared to developers, due to their different contexts, perspectives, techniques, and biases.
- An independent tester can verify, question, or challenge assumptions made by those involved in specifying and implementing the system.
##### Disadvantages of Independent Testing:
- Developers may lose a sense of responsibility for quality.
- Independent testers may be seen as a bottleneck or blamed for delays in release.
- Independent testers may lack important information, such as details about the test object.
### Three-Legged Stool
While each actor has a defined role, teamwork is essential among all three. They must work as a team, which is why we use the analogy of a three-legged stool—if any leg is missing, the stool cannot stand.
In some small software companies or startups, one person may hold more than one role. Additionally, an important aspect of agile development methodologies is the "three amigos" meeting. This is a session where these three roles come together to share their perspectives on the software under development. Here, more than ever, the functionality of the stool is demonstrated.
- **Business Analyst**: Responsible for identifying key business factors and serving as the intermediary between the systems department and the end customer.
- **Software Developer**: Designs, produces, programs, or maintains software components or subsets according to functional and technical specifications for integration into applications.
- **QA (Quality Assurance)**: The primary function is to test the software systems to ensure they work correctly according to customer requirements, document any errors found, and develop test procedures to track product issues more effectively and efficiently.