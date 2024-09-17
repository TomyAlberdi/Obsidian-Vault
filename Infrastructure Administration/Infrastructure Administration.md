Created: 2024-09-16 20:45
## Family Tree:
1. [[Computer]]
-- -
## Introduction
Currently, daily activities rely heavily on the proper functioning of IT systems —and the ability to operate those systems. The dependence of the productive sector on these complex IT systems is such that an issue with a work terminal can practically render any user's operational capacity ineffective. In situations like these —given the complexity of modern technological platforms and the variety of users with different levels of access and expertise— the presence of a reliable professional is required to intervene quickly and effectively, with skills and abilities beyond those of the regular operator.
The role of this professional —known as an infrastructure administrator— is to provide solutions to common hardware and software issues in any computerized environment. They approach problems by assessing them and determining the best solution. This service must be handled by professionals who can guide, configure, prevent, and resolve incidents, keeping the systems in optimal condition. Additionally, the infrastructure administrator must be capable of offering administration and support services for core systems and infrastructure elements used in IT applications, such as servers, mass storage devices, other hardware devices, operating systems (Operating System), virtual machines, network administrators, communication services through public and private networks, switching devices, firewalls, database engines, and more. They can also provide management services for the technological infrastructure on which this software operates, intervening as needed to resolve infrastructure issues or operational efficiency problems, and diagnosing incidents that arise during the system's regular operation.
The goal is to contribute concrete solutions to the IT infrastructure support issues encountered by almost all public and/or private institutions, accelerating the training of human resources who are skilled and in demand by organizations with IT infrastructure.
### Q&A
#### What is IT Infrastructure?
Information technology infrastructure, or IT infrastructure, refers to the combined components required for the operation and management of a company's IT services and IT environments.
#### What is the profile of an infrastructure analyst?
The functions of an infrastructure analyst include:
- Managing servers, base software, communications, and other subsystems, maximizing resource utilization and anticipating potential issues.
- Managing data communication networks (whether wired or wireless), ensuring service accessibility and optimizing resources.
- Addressing incidents that affect IT infrastructure support, diagnosing their root causes, and resolving or coordinating their resolution.
- Installing or replacing IT infrastructure support components or adapting it to new external service conditions while minimizing risks to security and service continuity.
- Migrating or converting systems, applications, or data, aiming to minimize risks to security and service continuity.
- Understanding contingencies and risks that may impact IT infrastructure support.
- Generating innovative proposals and/or productive ventures within the realm of IT infrastructure support management.
This person typically works in data processing centers, either within companies or organizations that use information technology. Their job title is often referred to as network administrator or systems administrator, and they work alone or in small teams to manage IT infrastructure resources and handle incidents to minimize potential service interruptions that could affect the IT applications provided to organizations.
#### Importance of an IT Infrastructure:
Technology drives nearly every aspect of modern businesses, from the tasks of individual employees to the operations of goods and services. When connected properly, technology can be optimized to enhance communication, create efficiency, and boost productivity.
If an IT infrastructure is flexible, reliable, and secure, it can help a company achieve its goals and provide a competitive advantage in the market. Conversely, if an IT infrastructure is not properly implemented, companies may face connectivity, productivity, and security issues, such as breaches or system downtime. In general, a well-implemented infrastructure can be a key factor in a business's profitability.
With an IT infrastructure, a company can:
- Provide a positive customer experience by ensuring uninterrupted access to its website and online store.
- Develop and launch solutions to the market quickly.
- Collect real-time data for fast decision-making.
- Improve employee productivity.
## Infrastructure Automation
As mentioned earlier, IT infrastructure is the combination of devices and software applications necessary for any company to operate. It consists of elements such as software, hardware, networks, facilities, and everything required to develop, control, monitor, and support the services provided by the IT department.
On the other hand, automation involves using technology to perform tasks with minimal human intervention. It can be implemented in any sector where repetitive tasks are carried out. IT automation —also known as infrastructure automation— refers to using software systems to create repeatable instructions and processes to replace or reduce human interaction with IT systems. Automating tasks saves time and maximizes the productivity of IT infrastructure.
In the era of cloud computing, this message is repeated constantly: How to do more with less. How to ensure that IT professionals in our company spend more time generating value for the company and less time on repetitive tasks that could be automated.
### Benefits of Automation:
- Increase business productivity.
- Reduce operational costs.
- Minimize the risk of failures.
- Enhance information security.
- Improve response capability.
- Ease of adaptation.
- Host larger amounts of data.
- Boost business competitiveness.
### Common IT tasks for Automation:
- **IT Task Provisioning:** Automate the process of enabling machines through service setup for new staff members in the organization.
- **Configuration Management:** Save time and effort by automating the configuration of enabled machines according to the IT department's objectives.
- **Security and Compliance:** Implement automated security policies and compliance actions in machine management.
- **Cloud Organization:** Ensure information security and maintain its availability through automation, generating greater efficiency.
- **Application Deployment:** Some applications need installation or configuration; this task can be automated in IT areas.
## Configuration and Maintenance of the system
One of the roles of the IT team is the **DevOps Engineer**, in charger of automating the processes of the Development and Operations areas. His function is to make the relationship between these two teams more friendly and efficient.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdnzmti3iOzo7pRKrNIaSgZQ7KQn_9E3Ml4FvRotvGcy9Qn-ukVy2rcKzpCOY_pSlN-ihqGNIASbU7Rl2v5OZx0sZj4qfq62W0Y_8F1O-3Rd67zJ90Ewwp4NUdbgv9_WXiknv3UvF7cybSQ86pU?key=4HNxQ73WcggcMKM9eeZQaw)
### Infrastructure and Services:
First we have to analyze the devices we have in our IT network: if we have legacy servers or services contracted by a cloud provider. Of the two previous options, what we have to take into account is the operating system they work with (MAC, Linux, Windows).
Among the best known cloud providers we have:
- AWS
- Google Cloud
- Microsoft Azure
The choice is made on the basis of cost and the range of services available. The latter is becoming increasingly robust and complete (load balancing, backup, clustering, security, etc).
### Code management:
We start from where we host our working code if we are programmers. The most widely used versioning manager and code integrator is Git. The most popular repositories in the cloud are GitLab, GitHub, Bitbucket, Gitea, among others.
These repositories store our application code, which can be in different programming languages depending on what we need.
We can also automate the deployment of our code with CI/CD (refers to the combined practices of continuous integration and continuous delivery). Some tools to do this are:
- Jenkins
- GitActions
- JetBrains
### Containers:
Containers are becoming the software packaging model for the product we develop. They allow the virtualization of transportable compatible working environments, fully configured so that our code works on all computers. The most popular is Docker.
When we manage many containers, we have to migrate to a cluster of containers, managed by container orchestrators. For example. Kubernetes or Docker Swarm.
### Work Environments (Working Environments):
Then, we must take into account the environment in which our cluster is located.
In each environment we work with different technologies, depending on the degree of exposure of the product. By automating these processes we will have more efficiency, transparency, ease of replication and recovery.
The most popular environments are:
- Ansible
- Chef
- Puppet
- Terraform
### Network monitors:
It is very important to have the monitoring of the devices in our network and services, and to program alerts in case of any change.
For this we can use:
- Nagios
- Prometheus
- Icinga2
- DataDog
### Scripting languages:
We need to work closely with developers and the system administrator to automate operator and developer tasks (such as backups, cron jobs, system monitoring).
Depending on the operating system, we can use Bash or PowerShell.
But there are also OS-independent scripting languages, such as Python, Ruby or Go. The most popular is Python, as it has many libraries and is easy to read and learn.