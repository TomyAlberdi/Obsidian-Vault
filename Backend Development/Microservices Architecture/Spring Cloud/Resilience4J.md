Created: 2024-10-04 18:51
## Family Tree:
1. Computer
2. Backend Development
3. Microservices Architecture
4. [[Spring Cloud]]
-- -
## Fault Tolerance
When transitioning from building monolithic systems to microservices, one of the first things we notice is that each of the components in our microservices ecosystem is part of a network. Communicating across a network can introduce problems that we previously ignored because we moved from having a single application running to several independent components that need to work together to ensure the system functions correctly. **Fault tolerance** in distributed systems refers to the system's ability to continue operating if one of its components fails.
Initially, Spring Cloud provided **Netflix Hystrix** as the default Circuit Breaker. However, today, Spring Cloud uses **Resilience4J**, an open-source fault-tolerance library inspired by Netflix Hystrix but designed for Java 8 and functional programming.
## Implementation
Adding the dependency in the POM file for the microservice implementing the Circuit Breaker:
```xml
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-starter-circuitbreaker-resilience4j</artifactId>
</dependency>
```
### Configuration:
Resilience4J can be configured through the `.yml` file. Here's an example configuration:
- **`slidingWindowType`**: This parameter specifies if the Circuit Breaker should be triggered by an event counter (e.g., three consecutive errors) or by a time-based counter. In this case, we'll use **COUNT_BASED** to trigger based on event count.
- **`slidingWindowSize`**: The number of failed calls required to trigger the Circuit Breaker, moving it to the Open state. We'll set this to **5**.
- **`failureRateThreshold`**: The percentage of failed calls that will trigger the Circuit Breaker, moving it to the Open state. We'll set this to **50%**. Combined with the previous setting, this means that if 3 or more of the last 5 calls fail, the Circuit Breaker will activate and move to Open.
- **`automaticTransitionFromOpenToHalfOpenEnabled`**: Determines if the Circuit Breaker will automatically transition to Half-Open after the wait duration. Set to **true**.
- **`waitDurationInOpenState`**: Specifies how long the Circuit Breaker should remain in the Open state before transitioning to Half-Open. Set to **10000ms** (10 seconds).
- **`permittedNumberOfCallsInHalfOpenState`**: The number of calls allowed in Half-Open state to determine if the Circuit Breaker should transition to Closed or Open. Set to **3**. If 2 out of 3 calls fail, the Circuit Breaker returns to Open, otherwise, it transitions to Closed.
- **`ignoreExceptions`**: Defines exceptions that the Circuit Breaker should ignore (not count as failures). For example, business rule exceptions like `NotFoundException` or missing required field exceptions.
- **`registerHealthIndicator`**: Enables Resilience4J to provide health status information via the `/health` endpoint of Actuator. Set to **true**.
- **`allowHealthIndicatorToFail`**: If enabled, Resilience4J can switch the `/health` endpoint status from UP to DOWN when a service is in Open or Half-Open state. Set to **false** in this case, and we'll program a custom function to handle those states.
- **`management.health.circuitbreakers.enabled`**: This is an Actuator parameter to enable the `/circuitbreakerevents` endpoint for tracking Circuit Breaker events. Set to **true**.
### Retries:
Retry mechanism allows retrying a failed request, useful for temporary network issues. It can be configured in the `.yml` file:
- **`maxAttempts`**: The number of attempts, including the first call. Set to **3** (allowing two retries after the first call).
- **`waitDuration`**: The wait time between retry attempts. Set to **5000ms** (5 seconds).
- **`retryExceptions`**: A list of exceptions that trigger a retry. In this case, retries are triggered only on `InternalServerError` (HTTP 500).
## Example: Microservice Communication
Assume we have two microservices: `course-service` and `subscription-service`. The `course-service` consumes the API of `subscription-service`, searching for a subscription by user ID.
In `subscription-service`, we have a method that takes a parameter called `throwError` (boolean). If `throwError` is `true`, the method returns an error, simulating a failure to test the Circuit Breaker.
### Subscription Controller:
```java
@GetMapping("/find")
public Subscription findSubscriptionByUser(
    @RequestParam Integer userId,
    @RequestParam(defaultValue = "false") Boolean throwError,
    HttpServletResponse response
) {
    return subscriptionService.findSubscriptionByUserId(userId, throwError);
}
```
### Subscription Service:
```java
@Override
public Subscription findSubscriptionByUserId(Integer userId, Boolean throwError) throws RuntimeException {
    if (throwError) {
        throw new RuntimeException();
    }
    return subscriptionRepository.findByUserId(userId);
}
```
In `course-service`, we configure **Resilience4J** as it makes the call to `subscription-service`. For testing, we always send `true` for `throwError`. The code looks like this:
```java
@Override
@CircuitBreaker(name = "subscription", fallbackMethod = "getSubscriptionFallbackValue")
@Retry(name = "subscription")
public Course findById(Integer courseId, Integer userId) throws BusinessError {
    Course course = null;
    ResponseEntity<SubscriptionDTO> response = feignSubscriptionRepository.findByUserId(userId, true);
    checkSubscription(response);
    course = courseRepository.findById(courseId).orElse(null);
    return course;
}
```
- `@CircuitBreaker`: Activated when an exception is thrown. The `name` parameter links to the `.yml` configuration, and `fallbackMethod` specifies an alternative method if the Circuit Breaker goes Open.
- **`@Retry`**: Enables retry logic. The `name` parameter is linked to the `.yml` file for configuration.
### Fallback Method:
```java
private void getSubscriptionFallbackValue(CallNotPermittedException ex) throws CircuitBreakerException {
    throw new CircuitBreakerException("Circuit Breaker was activated");
}
```
**`CallNotPermittedException`**: Handles exceptions thrown when the Circuit Breaker is Open.
### YAML Configuration:
```yml
# Actuator configuration
management.endpoints.web.exposure.include=circuitbreakers,circuitbreakerevents,health,info
management.health.circuitbreakers.enabled=true
management.endpoint.health.show-details=always

# Circuit breaker configuration
resilience4j.circuitbreaker.instances.subscription.allowHealthIndicatorToFail=false
resilience4j.circuitbreaker.instances.subscription.registerHealthIndicator=true
resilience4j.circuitbreaker.instances.subscription.slidingWindowType=COUNT_BASED
resilience4j.circuitbreaker.instances.subscription.slidingWindowSize=5
resilience4j.circuitbreaker.instances.subscription.failureRateThreshold=50
resilience4j.circuitbreaker.instances.subscription.waitDurationInOpenState=15000
resilience4j.circuitbreaker.instances.subscription.permittedNumberOfCallsInHalfOpenState=3
resilience4j.circuitbreaker.instances.subscription.automaticTransitionFromOpenToHalfOpenEnabled=true

# Retry configuration
resilience4j.retry.instances.subscription.maxAttempts=3
resilience4j.retry.instances.subscription.waitDuration=1000
resilience4j.retry.instances.subscription.retryExceptions[0]=feign.FeignException$InternalServerError
```
All properties for Resilience4J begin with `resilience4j`. In this example, `subscription` is the instance name configured in the `findById` method.
When an error occurs while fetching a subscription, the Circuit Breaker activates, and the fallback method returns an error message. In other scenarios, we could fetch the subscription from cache, but the Circuit Breaker implementation with a fallback method remains the same.