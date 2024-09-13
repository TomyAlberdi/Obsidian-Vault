Configuration Management and Change Management are two fundamental processes within the ITIL ([[Information]] Technology [[Infrastructure]] Library) methodology [[frameworks|framework]].
## Change Management
ITIL describes change management as the process of controlling and managing a change throughout its lifecycle with the goal of minimizing risk.
**What is a change?** According to ITIL, a change is the modification or removal of anything that may directly or indirectly affect services. Essentially, any change in an organization's IT infrastructure can impact its operations.
**Example:**
- Hardware replacement
- Installing software on a server
- Modifying a system configuration that will alter its behavior
## Configuration Management
Configuration management is the process of managing the configuration changes of files in our systems, whether [[software]] or [[hardware]]. It allows an organization to maintain a historical record and apply controls, such as an approval process for changes that meet certain criteria.
Each IT asset in this process is known as a _Configuration Item (CI)_, and these are stored in a _Configuration Management Database (CMDB)_.
## Change Management + Configuration Management
These two processes complement each other. Change management contributes to the governance of changes within an organization’s IT infrastructure, while configuration management helps manage a CMDB with the information of our assets (CIs) and a history of changes made to each of them.
For example, if a critical failure occurs in a server and forces us to restore it, the configuration management process provides a view of all changes made to that asset since its creation, allowing us to reproduce these changes and return the system to its state before the failure.
## Configuration Management Tools
### Chef:
Chef is a configuration management platform with a client-server architecture, primarily oriented towards Linux. Configurations are defined and assigned on the server, and the Chef client makes them effective on the assets we wish to configure. Chef operates in "pull" mode, meaning the client periodically checks the server for configuration updates.
Configurations in Chef are written in **Ruby**.
### Puppet:
Like Chef, Puppet is a configuration management platform with a client-server architecture, also primarily for Linux. The client in Puppet, like Chef, detects and corrects deviations caused by manual interventions. Puppet configurations are written in a **Domain-Specific Language (DSL)** created by Puppet Labs.  
Puppet's key difference from Chef is its **reporting capabilities**.
### PowerShell DSC:
Desired State Configuration (DSC) is part of PowerShell, originally developed to manage Windows Server configurations, but it is now cross-platform and can also configure Linux hosts. It can operate in both client-server mode ("pull") or standalone mode ("push"). When in "push" mode, the configurations are defined locally and applied by the Local Configuration Manager (LCM).
DSC configurations are written in **PowerShell** scripting language.
### Ansible:
[[Ansible]] is a configuration management tool developed in **Python**. Unlike Chef or Puppet, Ansible does not require an agent installed on the servers. Instead, it connects via SSH to deploy configurations. Ansible has evolved beyond configuration management and is now also used as an **orchestration tool** for cloud deployments and application release processes.
Configurations in Ansible are written in **YAML** format.
## Configuration As Code
In modern Configuration Management processes, the ability to define server configurations as code (Configuration As Code) is crucial. Managing IT infrastructure "like cattle" (i.e., treating servers as replaceable resources rather than unique entities) would not be possible without using a Configuration Management system.
### Key Benefits:
1. **Automation:**  
   Anything defined as code can be automated, making it easier to deploy, update, and maintain configurations across multiple servers.
2. **Testability:**  
   Code can be subjected to tests, ensuring that configurations work as expected before they are deployed.
3. **Self-Healing and Self-Remediation:**  
   CaC is a foundational step towards enabling _Self-Healing_ and _Self-Remediation_, two modern infrastructure practices that implement processes for automatic recovery and repair.
### ITIL Change Management Compatibility:
CaC aligns with ITIL’s Change Management process because changes are made not directly on the assets but in a version-controlled repository. This allows changes to be tested in lower environments before being deployed to production, ensuring controlled, safe updates.
CaC does not replace ITIL’s Configuration Management process but complements it by enhancing the ability to track, automate, and version control configurations.
### Challenges of Adopting CaC:
1. **Transition Considerations:**  
   The first challenge is to assess whether transitioning to modern processes like CaC makes sense for the organization. It requires an evaluation of the current IT infrastructure and the benefits of moving to code-based configurations.
3. **Scope of Implementation:**  
   How far should the organization go with CaC implementation? Will it adapt existing systems or adopt the practice only for new systems? These are critical decisions that must be made.
3. **Resistance to Change:**  
   Abandoning traditional methods of managing servers can meet resistance from teams accustomed to older workflows. Overcoming this resistance requires proper change management and training.
4. **Rethinking Server Builds:**  
   The shift to CaC may require the organization to reconsider how servers are built and managed, possibly requiring significant adjustments to existing processes.