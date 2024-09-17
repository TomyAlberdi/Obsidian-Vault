Created: 2024-09-17 15:19
## Family Tree:
1. Computer
2. Backend Development
3. Go
4. [[Go Web]]
-- -
## Adding a Go Microservice to a Spring Cloud Environment with Eureka
When talking about microservices architecture, we think of multiple small services that work together, each independent and deployable separately. While Go might not be the first choice in a Spring Cloud ecosystem where most services are Java-based, you can still integrate a Go microservice into this environment and register it with **Eureka Server**.
![[Backend Development/Go/Go Web/attachments/grafico-esp-be-3.png]]
Eureka Server provides a REST API that allows us to register services and query other services. For Java-based microservices using Spring Cloud, this is done using **Eureka Client**. However, when using Go, we need to manually handle the communication between the Go microservice and Eureka Server.
## Steps to Register and Integrate a Go Microservice with Eureka
### Registering the Microservice:
To register a Go microservice instance, send a `POST` request to the endpoint `/eureka/v2/apps/${appID}`, where `${appID}` is the name of the microservice.
The body of the request should follow this structure:
```json
{
  "instance": {
    "instanceId": "go-ms-1",
    "hostName": "localhost",
    "app": "go_ms",
    "vipAddress": "go_ms",
    "secureVipAddress": "go_ms",
    "ipAddr": "127.0.0.1",
    "status": "STARTING",
    "port": {
      "$": 8080,
      "@enabled": "true"
    },
    "securePort": {
      "$": 8443,
      "@enabled": "true"
    },
    "healthCheckUrl": "http://localhost:8081/healthcheck",
    "statusPageUrl": "http://localhost:8081/status",
    "homePageUrl": "http://localhost:8081",
    "dataCenterInfo": {
      "@class": "com.netflix.appinfo.InstanceInfo$DefaultDataCenterInfo",
      "name": "MyOwn"
    }
  }
}
```
#### Example Go code for registering:
```go
func registerApp() {
  appId := "go_ms-1"
  appName := "go_ms"
  body := buildBody(appId, "STARTING")
  
  var buf bytes.Buffer
  error := json.NewEncoder(&buf).Encode(body)
  if error != nil {
    log.Fatal(error)
  }
  
  resp, err := http.Post("http://localhost:8761/eureka/apps/"+appName, "application/json", &buf)
  if err != nil {
    log.Fatal(err)
  }
  
  defer resp.Body.Close()
  responseBody, parseErr := io.ReadAll(resp.Body)
  if parseErr != nil {
    log.Fatal(err)
  }
  
  fmt.Println(string(responseBody))
}
```
The `buildBody` function should create the JSON object that Eureka expects to register a new instance.
### Updating the Microservice Status:
Once the microservice is ready to receive requests, you need to update its status to `UP`. This is done by sending the same request as before, but with the `status` field set to `"UP"`.
#### Example JSON body:
```json
{
  "instance": {
    "instanceId": "go-ms-1",
    "hostName": "localhost",
    "app": "go_ms",
    "vipAddress": "go_ms",
    "secureVipAddress": "go_ms",
    "ipAddr": "127.0.0.1",
    "status": "UP",
    "port": {
      "$": 8080,
      "@enabled": "true"
    },
    "securePort": {
      "$": 8443,
      "@enabled": "true"
    },
    "healthCheckUrl": "http://localhost:8081/healthcheck",
    "statusPageUrl": "http://localhost:8081/status",
    "homePageUrl": "http://localhost:8081",
    "dataCenterInfo": {
      "@class": "com.netflix.appinfo.InstanceInfo$DefaultDataCenterInfo",
      "name": "MyOwn"
    }
  }
}
```
#### Example Go code for updating status:
```go
func updateAppStatus(status string) {
  fmt.Println("Updating app status")
  
  appId := "go_ms-1"
  appName := "go_ms"
  body := buildBody(appId, status)
  
  var buf bytes.Buffer
  error := json.NewEncoder(&buf).Encode(body)
  if error != nil {
    log.Fatal(error)
  }
  
  resp, err := http.Post("http://localhost:8761/eureka/apps/"+appName, "application/json", &buf)
  if err != nil {
    log.Fatal(err)
  }
  
  defer resp.Body.Close()
  responseBody, parseErr := io.ReadAll(resp.Body)
  if parseErr != nil {
    log.Fatal(err)
  }
  
  fmt.Println(string(responseBody))
}
```
### Sending Heartbeats:
Eureka requires a "heartbeat" from the service every 30 seconds to keep it active. This can be done by sending a `PUT` request to the endpoint `/eureka/apps/{APP_NAME}/{INSTANCE_ID}`.
#### Example Go code for sending a heartbeat:
```go
func sendHeartbeat(appName string, appId string) {
  req, err := http.NewRequest("PUT", "http://localhost:8761/eureka/apps/"+appName+"/"+appId, nil)
  if err != nil {
    log.Fatal(err)
  }
  
  resp, err := http.DefaultClient.Do(req)
  if err != nil {
    log.Fatal(err)
  }
  
  fmt.Println(resp.Body)
}
```
### Deregistering the Microservice:
If the microservice is shutting down, its status should be updated to `DOWN`, and it should be deregistered from Eureka by sending a `DELETE` request to the endpoint `/eureka/apps/{APP_NAME}/{INSTANCE_ID}`.
#### Example Go code for deregistering:
```go
func deleteApp(appName string, appId string) {
  fmt.Println("Deregistering app")
  
  req, err := http.NewRequest("DELETE", "http://localhost:8761/eureka/apps/"+appName+"/"+appId, nil)
  if err != nil {
    log.Fatal(err)
  }
  
  resp, err := http.DefaultClient.Do(req)
  if err != nil {
    log.Fatal(err)
  }
  
  fmt.Println(resp.Body)
}
```
First, update the app status to `DOWN` using `updateAppStatus`, then call `deleteApp` to remove it from Eureka.