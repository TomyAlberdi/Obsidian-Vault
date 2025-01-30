Created: 2024-10-03 15:43
## Family Tree:
1. Computer
2. Backend Development
3. Microservices Architecture
4. [[Computer Science/Backend Development/Microservices Architecture/Design Patterns/Design Patterns|Design Patterns]]
-- -
In practice, when something fails, it's common to simply show the user an error message saying "something went wrong, please try again later." But what happens if the user was trying to make a purchase? Are we willing to let that opportunity slip?
With the advent of new distributed architectures like microservices, many advantages have emerged, but so have new challenges that are often difficult to address precisely. One such challenge is identifying when a service suddenly stops functioning so that we can stop sending requests to it and take appropriate action.
The **Circuit Breaker** pattern proposes a solution to this problem and can be likened to a household electrical fuse, which blows to prevent a power surge from affecting the circuit. In other words, this pattern allows us to intelligently stop communication with a particular service when it’s detected to be failing, thereby preventing the failure from spreading to the rest of the system.
Continuing with the example of a purchase, if a service fails, we could stop sending requests to it and implement a fallback plan while the service recovers. Some alternatives could include retrying the transaction after a specified delay, or sending the request to a queue to be processed asynchronously, after which we can confirm the purchase to the end consumer.
## States
The Circuit Breaker pattern can transition through three different states, each affecting how it operates. These states are **Closed**, **Open**, and **Half Open**.
- **Closed:** This is the initial state, indicating that the service is responding successfully. If a certain threshold of errors is reached, the Circuit Breaker will transition to the Open state.
- **Open:** In this state, it indicates that the target service is failing, and returns an error when invoked. After a specified timeout, it transitions to the Half Open state.
- **Half Open:** In this state, the Circuit Breaker allows a small number of requests to test if the service is functioning again. If the next few requests succeed, the Circuit Breaker transitions back to Closed; otherwise, it returns to the Open state.
## General Operation
The Circuit Breaker pattern is typically applied when one service depends on another. If the other service fails or takes too long to respond (timeout), it retries a certain number of times. If the threshold is exceeded, an error is returned. Otherwise, normal operation resumes.
This pattern also often reveals design issues. For example, if your service depends on a third-party service that frequently fails, one option is to call the service owner and ask them to fix it, but sometimes this isn't possible. The solution, in such cases, would be to use a **message queue** and make the operation asynchronous.
The **Circuit Breaker** pattern is widely used in critical processes, helping prevent the application from becoming overwhelmed with requests that are bound to fail. It allows the system to take appropriate action and, whenever possible, provide a response, even if it's a different one.