## Virtual Machines in the Cloud
With the growing popularity of cloud computing, businesses are increasingly turning to **virtual machines (VMs)** in the cloud for their computing needs, including mobile applications.
### What is Virtualization?
Virtualization is the process of creating a virtual version of a physical resource, such as an [[operating system]], [[software]] platform, or peripheral device, through special software. With increased global internet access, faster connection speeds, and greater storage capacities offered by many companies, virtual machines can now be run in the cloud.
### Utility of Cloud VMs:
For example, if you need a server running 24/7 to host websites or online services, you have two options:
1. **Physical Server**: Purchase an expensive server, set it up at home or in your business, and handle everything from internet connectivity to security, backups, power management, and more.
2. **Cloud VM**: Hire a service to create a VM in the cloud, which can act as a server. Simply upload your databases and applications. The cloud provider handles maintenance. Major services include **Microsoft Azure**, **Amazon Web Services (AWS)**, and **Google Cloud Platform**.
### Responsibility Model in Cloud Computing:
Cloud computing involves using resources owned by a third party, making the user a tenant of the cloud provider. This **shared responsibility model** defines which tasks are delegated to the cloud provider and which remain the user’s responsibility.
#### Roles:
- **Provider**: The cloud service owner, managing the infrastructure and offering defined services.
- **Consumer**: The user (you) who contracts services from the provider to run applications.
#### Responsibility Breakdown by Service Model:
1. **Data Center**: If you host everything in-house, you are responsible for all tasks related to IT management.
    - **Pros**: Full control over assets.
    - **Cons**: Full responsibility for maintaining, scaling, and securing infrastructure.
2. **[[Infrastructure]] as a Service (IaaS)**: The provider offers virtual machines, but you manage the operating system and applications.
    - **Pros**: Control over the OS, flexibility to install applications.
    - **Cons**: Responsibility for maintaining the OS and applications.
3. **Platform as a Service (PaaS)**: The provider offers a platform with preconfigured resources. You focus on deploying and managing your applications.
    - **Pros**: No need to manage lower-level infrastructure; focus on application development.
    - **Cons**: Limited customization options, potentially higher costs.
4. **Software as a Service (SaaS)**: 
   The provider offers a fully functioning application, like **Trello**, Salesforce, or **Gmail**.
    - **Pros**: Immediate access to a ready-to-use application.
    - **Cons**: Limited control over configuration and new features.
### Types of Virtual Machines:
1. **General Purpose**: Balanced CPU, memory, and network resources, ideal for web servers or code repositories.
2. **Compute-Optimized**: Designed for high-performance applications that are CPU-intensive, like batch processing workloads.
3. **Memory-Optimized**: Optimized for tasks that process large datasets in memory, providing fast performance.
4. **Storage-Optimized**: Suitable for workloads requiring high read/write access to large datasets, offering thousands of operations per second.
5. **Accelerated Computing**: Utilizes hardware accelerators for tasks like graphics processing or pattern matching in large data sets.
## VPC
A **Virtual Private Cloud (VPC)** is a private cloud hosted within a public cloud, enabling businesses to leverage the benefits of a virtualized network while utilizing the resources of the public cloud. VPCs provide secure, isolated environments where data is protected during transit and within the provider’s network, making them ideal for applications that require a high level of security.
VPCs typically connect with remote networks via a **Virtual Private Network (VPN)**, ensuring that external connections are secure. VPCs are often the best choice for organizations in highly regulated industries, like healthcare and finance, where security, privacy, and control are essential. They're also ideal for running critical applications.
### Key Utilities:
1. **Security**: VPCs provide enhanced security by allowing the protection of virtual network environments, including IP addresses, subnets, and gateways. For example, you can securely isolate a database in a private subnet that is not connected to the internet.
2. **Data Control**: Because a VPC is isolated from other clouds at the network layer, data remains separate and secure, mitigating the risk of data mixing with that of other organizations, a potential issue in public cloud environments.
3. **Performance**: VPCs enable prioritization of network traffic for specific applications, helping to optimize performance and avoid network congestion or bottlenecks.
4. **On-Demand Flexibility**: VPCs allow businesses to design a cloud architecture that best fits their needs. For example, a VPC can be configured so that contractors use direct connections without accessing the internal network.
## Providers
### Amazon EC2:
**Amazon Elastic Compute Cloud (Amazon EC2)** is a web service that provides secure, scalable compute capacity in the cloud. It is designed to make cloud computing easier for developers by providing a simple interface to quickly acquire and configure compute resources with minimal friction. EC2 gives full control over computing resources and runs within Amazon's accredited environment. It offers the broadest range of computing platforms, allowing users to select processors, storage, networking, operating systems, and purchase models. EC2 features powerful GPU instances for machine learning training and graphics workloads, along with cost-efficient inference instances. AWS also supports more workloads like SAP, HPC, machine learning, and Windows than any other cloud provider.
### Azure Virtual Machines:
**Microsoft Azure** supports both Windows and Linux operating systems, including Windows Server 2003. Key components of an Azure virtual machine include:
- **Virtual Disk**: Stores the [[operating system]] and data, ensuring persistence.
- **Virtual [[Network]] Card**: Facilitates network connectivity.
- **IP [[Addresses]]**: Used for connecting to the virtual machine, available as private or public.
- **Network Security Groups (NSGs)**: Help manage inbound and outbound network traffic rules based on IP, protocol, or port.
Azure allows configuration of three key elements:
- **VM Name**: Cannot be changed after creation.
- **Operating System**: Core OS that runs on the VM.
- **Size**: Predefined sizes with various [[CPU]], [[memory]], and disk options, allowing vertical scaling (increasing [[hardware]] resources). Changing the size may require a reboot.
### Google VM Instances:
**Google Compute Engine** offers virtual machines (VMs) hosted on Google [[infrastructure]]. Instances can be created via the **Google Cloud Console**, **gcloud CLI**, or the **Compute Engine API**. Google VMs support both Google-provided public images (Linux and Windows) and custom private images. Additionally, [[Docker]] containers can run on instances using the **Container-Optimized OS**.
- **Customization**: Users can choose from predefined or custom machine types to set CPU and memory configurations.
- **Instance Management**: Each instance belongs to a Google Cloud project, and projects can have multiple instances, each defined by zone, OS, and machine type.
- **Storage**: By default, each instance includes a small persistent boot disk with the OS. Additional storage can be added as needed.
- **Access**: Connect to instances using **SSH** for Linux or **RDP** for Windows.
## Conclusion:
Cloud VMs provide flexibility, scalability, and cost savings compared to physical servers. Depending on the chosen model (IaaS, PaaS, SaaS), businesses can offload varying levels of infrastructure management to the cloud provider, focusing more on core operations and less on IT maintenance.