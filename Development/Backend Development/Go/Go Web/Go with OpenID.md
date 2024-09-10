In this scenario, we're using **Keycloak** as our Identity and Access Management (IAM) system to secure a [[Go]] microservice. The microservice will act as a **resource server**, validating the tokens it receives before granting access to its endpoints. The setup includes an **API Gateway** and **Eureka Server** for service discovery. Below, we walk through how to configure Keycloak, Go, and Spring Cloud components for a seamless integration.
## Setting up Keycloak
Before connecting the Go microservice, we need to configure **Keycloak**.
- **Realm**: Create a new realm (e.g., "digital-house").
- **Client**: Create a new client (e.g., "gateway") with the **confidential** access type. Enable the **standard flow** (for exchanging an authorization code for an access token).
- **Role**: Create a role named `"USER"` and map it to the client.
- **User**: Create a new user and assign the `"USER"` role to them.
This configuration allows users authenticated via Keycloak to access protected endpoints in your Go microservice.
## Go Microservice Middleware for JWT Validation
```SH
go get github.com/coreos/go-oidc
```
The following middleware will validate the JWT, ensuring the user has the required role to access specific endpoints:
### Middleware code:
```go
var RealmConfigURL string = "http://localhost:8082/realms/digital-house"
var clientID string = "gateway" // The clientId created in Keycloak

// Structs to map the JWT claims
type Claims struct {
  ResourceAccess client `json:"resource_access,omitempty"`
  JTI string `json:"jti,omitempty"`
}

type client struct {
  Gateway clientRoles `json:"Gateway,omitempty"`
}

type clientRoles struct {
  Roles []string `json:"roles,omitempty"`
}

// Middleware to validate the JWT and check the role
func IsAuthorizedJWT(role string) gin.HandlerFunc {
  return func(c *gin.Context) {
    // Extract the token from the Authorization header
    rawAccessToken := strings.Replace(c.GetHeader("Authorization"), "Bearer ", "", 1)
    
    tr := &http.Transport{
      TLSClientConfig: &tls.Config{InsecureSkipVerify: true},
    }
    client := &http.Client{
      Timeout: time.Duration(6000) * time.Second,
      Transport: tr,
    }
    
    ctx := oidc.ClientContext(context.Background(), client)
    
    // Connect to Keycloak (OpenID Provider)
    provider, err := oidc.NewProvider(ctx, RealmConfigURL)
    if err != nil {
      authorizationFailed("Failed to get provider: " + err.Error(), c)
      return
    }

    oidcConfig := &oidc.Config{ClientID: clientID}
    
    // Validate the JWT using Keycloak's public keys
    verifier := provider.Verifier(oidcConfig)
    idToken, err := verifier.Verify(ctx, rawAccessToken)
    if err != nil {
      authorizationFailed("Failed to verify token: " + err.Error(), c)
      return
    }
    
    // Map the token claims to our Claims struct
    var IDTokenClaims Claims
    err = idToken.Claims(&IDTokenClaims)
    if err != nil {
      authorizationFailed("Failed to parse claims: " + err.Error(), c)
      return
    }
    
    // Get roles associated with the client ("gateway")
    userAccessRoles := IDTokenClaims.ResourceAccess.Gateway.Roles
    for _, r := range userAccessRoles {
      if r == role {
        c.Next() // Allow access if the required role is present
        return
      }
    }
    
    authorizationFailed("User not allowed to access this API", c)
  }
}

// Error handling function
func authorizationFailed(message string, c *gin.Context) {
  data := Res401Struct{
    Status:   "FAILED",
    HTTPCode: http.StatusUnauthorized,
    Message:  message,
  }
  c.AbortWithStatusJSON(401, gin.H{"response": data})
}
```
### Using the Middleware in the Go Application:
```go
server := gin.Default()
server.Use(IsAuthorizedJWT("USER"))

usersRoute := server.Group("/users")
usersRoute.GET(":id", handler.FindById())
```
Here, the middleware `IsAuthorizedJWT("USER")` checks if the JWT contains the `"USER"` role before granting access to the `/users/:id` endpoint.
## Configuring API Gateway in Spring Cloud
In your **API Gateway**, we configure it to authenticate users using Keycloak and forward valid tokens to microservices (like the Go service) via **TokenRelay**.
### Example `application.yml`
```yml
# Server configurations
server:
  port: 8090

# Eureka configurations
eureka:
  instance:
    hostname: localhost
    prefer-ip-address: true
  client:
    register-with-eureka: true
    fetch-registry: true
    serviceUrl:
      defaultZone: http://localhost:8761/eureka

# Spring Cloud configurations
spring:
  application:
    name: ms-gateway
  security:
    oauth2:
      client:
        provider:
          api-gateway-service:
            issuer-uri: http://localhost:8082/realms/digital-house
        registration:
          api-gateway-service:
            provider: api-gateway-service
            client-id: gateway
            client-secret: a5946L5jX0YKydqNxay68LKKU2BxOnof
            authorization-grant-type: authorization_code
            redirect-uri: 'http://localhost:8090/login/oauth2/code/keycloak'

# Gateway routes and filters
cloud:
  gateway:
    default-filters:
      - TokenRelay
    routes:
      - id: users-service
        uri: lb://users-service
        predicates:
          - Path=/api/v1/users/**
        filters:
          - StripPrefix=2
```
Here’s what each section does:
- **TokenRelay** ensures the JWT is passed to the downstream services.
- **`uri: lb://users-service`** refers to the Go microservice registered in Eureka as `users-service`.
## Securing the API Gateway
The following Spring configuration restricts all requests and enables login via Keycloak.
### `SecurityConfiguration.java` :

```java
@Configuration
public class SecurityConfiguration {

  @Bean
  public SecurityWebFilterChain springSecurityFilterChain(ServerHttpSecurity http) {
    return http
      .authorizeExchange()
        .anyExchange().authenticated()
      .and()
        .oauth2Login()
      .and()
        .csrf().disable()
        .build();
  }

  @Bean
  public JwtDecoder jwtDecoder() {
    return NimbusJwtDecoder.withJwkSetUri("http://localhost:8082/realms/digital-house/protocol/openid-connect/certs")
      .build();
  }
}
```
This configuration ensures that the API Gateway only allows authenticated users to access the microservices.
## Conclusion
By following this architecture, you ensure that:
1. **Keycloak** acts as the central IAM system, handling authentication and authorization.
2. **Go microservices** securely validate JWTs using the **go-oidc** library.
3. **API Gateway** forwards authenticated requests and tokens to microservices, maintaining security across the system.
This setup abstracts security concerns from the microservices themselves, allowing them to focus on core functionality while relying on centralized authentication via Keycloak and OAuth 2.0/OpenID Connect.