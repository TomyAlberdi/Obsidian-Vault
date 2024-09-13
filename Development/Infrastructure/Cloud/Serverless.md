Serverless is a cloud-native development model that allows developers to design and run applications without managing servers directly. While servers are still used, they are abstracted away from the development process. The cloud provider handles routine tasks like server provisioning, maintenance, and scaling of [[infrastructure]].
Once deployed, serverless applications respond to demand and automatically scale based on need. Public cloud providers typically offer serverless technologies using an event-driven execution model, meaning costs are incurred only when functions are executed. When functions are idle, no charges apply.
In traditional Infrastructure-as-a-Service (IaaS) models, developers pre-purchase server capacity and pay for resources that are continuously running to support their applications.
## Cloud Providers' role:
Cloud providers handle the physical infrastructure and dynamically allocate resources to users who deploy code directly to production. They also:
- Manage the [[operating system]] and filesystem.
- Apply security patches.
- Balance load.
- Manage capacity.
- Adapt resources as needed.
- Maintain logs.
- Monitor the system.
## Serverless classifications:
- **Backend-as-a-Service (BaaS)**: Provides developers access to external applications and services. Cloud providers may offer services like [[authentication]], encryption, or databases that are accessible from the cloud.
- **Function-as-a-Service (FaaS)**: Functions are usually invoked through API calls. When referring to serverless, FaaS is often the focus. Developers write custom server-side logic, which is then executed in containers fully managed by the cloud provider.
Serverless architecture is ideal for asynchronous, stateless applications that can be quickly spun up. It is also a good choice for applications with unpredictable demand spikes.
## Common Serverless use cases:
- **Incoming data streams**
- **Chatbots**
- **Scheduled tasks**
- **Business logic**
- Web applications, backend APIs, business service automation, serverless websites, and system integrations.
## Pros and Cons of Serverless
### Advantages:
- **Increased developer productivity**: Developers can focus on writing code rather than managing infrastructure.
- **Reduced operational costs**: Pay only for processing time in the cloud as needed, rather than running and managing servers continuously.
### Disadvantages:
- **Limited flexibility and customization**: Cloud providers impose strict limits on how users can interact with their infrastructure, which affects flexibility.
- **Vendor lock-in**: Switching providers may involve costly system upgrades to meet the new provider's specifications.