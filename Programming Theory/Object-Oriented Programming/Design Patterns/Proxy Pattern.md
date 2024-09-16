Let’s see how we can use this [[Design Patterns|Pattern]] to control access to an object, allowing us to perform something before or after the request reaches it.
## Purpose
The aim is to develop the function of acting as an intermediary that adds functionality to a class without modifying the class itself.
## Solution
Define a Proxy class with the same interface as the original service object. Then, update our application so that clients communicate with the proxy and not directly with the target service. Upon receiving a client request, the proxy will forward it to the service, but as an intermediary, we can perform operations either before or after forwarding the request.
## Advantages
- The proxy works even if the service object is not ready or available.
- **Open/Closed Principle**: We can introduce new proxies without changing the service or the clients.
## Disadvantages
- Adding an extra layer between the client and the real service may cause a delay in response time.
## Implementation
- If there is no pre-existing service interface, one should be created so that both proxy and service objects are interchangeable.
- The Proxy class is created. It must have a field to store a reference to the service.
- We implement the proxy methods according to its purposes. In most cases, after performing some task, the proxy should delegate the work to the service object.
## Example
**Let's think of a real-life scenario.** In some places, like at university or work, the network that connects us to the internet is restricted, and we don’t have access to all websites.
It may be that we have a proxy restricting access, and instead of connecting directly to the internet, we are communicating with the proxy, which ultimately connects to the internet.
### Implementation:
We define the interface.
```java
public interface IInternetConnection {
    public void connectTo(String url);
}
```
We define the service that connects us to the internet.
```java
public class InternetService implements IInternetConnection {
    @Override
    public void connectTo(String url) {
        System.out.println("Connecting to " + url);
    }
}
```
We define the proxy, which performs the same function as the internet service, but with extra logic. In this case, we will check if the address we want to connect to is on the list of blocked sites.
```java
public class ProxyInternet implements IInternetConnection {
    private InternetService internetService;
    private List<String> blockedSites;

    public ProxyInternet(List<String> blockedSites, InternetService internetService) {
        this.blockedSites = blockedSites;
        this.internetService = internetService;
    }

    @Override
    public void connectTo(String url) {
        if (!this.blockedSites.contains(url))
            this.internetService.connectTo(url);
        else
            System.out.println("Access denied");
    }
}
```
Main class:
```java
public class Main {
    public static void main(String[] args) {
        List<String> blockedSites = new ArrayList<>();
        blockedSites.add("www.youtube.com");
        blockedSites.add("www.facebook.com");

        IInternetConnection proxy;
        proxy = new ProxyInternet(blockedSites, new InternetService());

        proxy.connectTo("www.google.com");
        proxy.connectTo("www.youtube.com");
    }
}
```