Created: 2024-09-17 17:44
## Family Tree:
1. Computer
2. [[Testing]]
-- -
### Error, Defect and Failure:
- **Error**: Occurs due to a mistake made by a person.
- **Defect**: The error results in a defect in the software.
- **Failure**: The defect causes a failure when the test (Testing) is executed.
## Defect Lifecycle
The process that manages a defect from its discovery to its resolution is called the defect lifecycle. In each state, there is only one person responsible for the defect, except in terminal states (e.g., closed, duplicate) because no further actions will be taken.
1. **New/Initial**: Information is collected, and the defect is recorded.
2. **Assigned**: If it’s a valid defect that needs fixing, it is assigned to the development team; otherwise, it can be rejected or deferred (bug triage).
3. **Duplicate**: If the defect repeats or there is another with the same root cause.
4. **Returned or Rejected**: More information is requested, or the defect is rejected.
5. **Deferred**: The defect is not a priority and will be fixed in a future version.
6. **In Progress**: The defect is analyzed, and work on a solution begins.
7. **Fixed**: Code changes are made to fix the defect.
8. **Awaiting Verification**: Waiting for a tester to be assigned. The developer is awaiting the verification result.
9. **In Verification**: The tester performs a confirmation test.
10. **Reopened**: The confirmation test shows that the defect hasn’t been fixed.
11. **Verified**: The expected result is achieved in the confirmation test.
12. **Closed**: The defect is fixed and available to the end user.
## Defect Management Process
1. **Detect**.
2. **Log**: Varies based on the context of the component or system, the test level, and the chosen development model.
3. **Investigation and Tracking**.
4. **Classification/Resolution**.
#### Objectives:
- Provide information on any adverse event to identify specific effects, isolate the problem with minimal reproduction, and fix potential defects.
- Provide test managers with a way to track the quality of the work product and the impact on testing.
- Provide ideas for improving the development and testing processes.
### Writing a Defect Report:
**Conditions to consider**:
- **Bugs must have unique identifiers**: Although many bug-tracking tools automatically assign a unique ID, many bugs are reported via emails, bypassing the tool's registration.
- **A failure must be reproducible to report it**: If the defect is not reproducible, it’s not a defect. For isolated occurrences, we can make a personal note to investigate later and determine the necessary conditions for it to happen.
- **Be specific**: Avoid writing assumptions or ideas about what is happening. Only include relevant information to reproduce the defect.
- **Report each step taken to reproduce the defect**: Provide the developer with all necessary information to replicate the failure. No relevant step should be omitted.
#### Common problems with Defect Reports:
- Writing a defect report in an overly casual and vague manner.
- Providing only a screenshot without indicating what was being done when the defect occurred.
- Not including the expected result for the steps taken.
- Failing to identify a pattern before reporting the defect—this is essential for clearly stating the problem.
- Not following the steps oneself to ensure that the description is clear.
- Omitting information that is relevant given the nature of the defect.
#### Parts of a Defect Report:
- **ID**: A unique, non-repetitive code that can be numeric or alphanumeric (001 - "Test01").
- **Title**: Short and specific, conveying what we want to report. The developer or team should be able to quickly understand what, where, and how important the defect is ("Login - Allows submission with blank fields").
- **Description**: Provide further details about the error, elaborating on what is not mentioned in the title ("On the login screen, if the name and password fields are left blank, the system redirects to the main page").
- **Report Date**: The date the defect was detected, to track the time it took to resolve (04/23/21).
- **Author**: The name of the tester who found the defect, so the developer knows who to contact if there are questions ("Juan Pérez").
- **Test Item ID**: Name of the application or component being tested ("Shopping Cart").
- **Steps to Reproduce**: The steps required to reach the detected defect.
- **Expected Result**: What the application should do or display according to its requirements ("It should not allow access without valid username and password").
- **Actual Result**: What actually happens or is shown by the application. If it doesn’t match the expected result, a bug has been found ("Accesses the application without username and password").
- **Severity**: How serious the defect is: Blocker, Critical, High, Medium, Low, or Trivial ("Critical").
- **Priority**: How quickly the defect should be fixed: High, Medium, or Low ("High").
- **Defect Status**: Possible statuses: New, Deferred, Duplicate, Rejected, Assigned, In Progress, Fixed, Awaiting Verification, In Verification, Verified, Reopened, or Closed ("New").
- **References**: Link to the test case where the error was found.
- **Image**: A screenshot of the error can be attached to demonstrate the issue, helping the developer locate it.