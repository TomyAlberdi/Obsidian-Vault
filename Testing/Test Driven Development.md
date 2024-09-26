Created: 2024-09-17 17:48
## Family Tree:
1. Computer
2. [[Testing/Testing]]
-- -
**TDD (Test-Driven Development)** means using tests to guide the way we write code. The typical workflow of TDD is often described as **Red, Green, Refactor**.
## Red
In this phase, you write business logic test cases, which are expected to fail initially because the required functionality doesn't exist yet.
**Premise**: A new test case will always fail at first.
### Iteration 1:
- You start by writing a test case.
- Since the method being tested doesn’t exist, the test fails due to a **compilation error**.
### Iteration 2:
- You write a minimal method to make the code **compile**.
- The focus here is only to pass the compilation stage, not necessarily solve the business need.
## Green
In this phase, you modify the code just enough to make the test pass.
### Iteration 3:
- Write the minimal amount of code required to make the test **pass successfully**.
- The goal is to make the test case functional, even if the implementation is not perfect.
## Refactor
In this phase, you refactor both the code and the test to make them more efficient, clean, and maintainable.
### Iteration 4:
- You refactor the code to improve its structure without changing its behavior.
### Iteration 5:
- Further refactor or optimize both the production code and tests to ensure they are clean, efficient, and follow best practices.
By following this **Red-Green-Refactor** cycle, TDD ensures that the code is tested thoroughly and built incrementally, which improves quality and reduces bugs.