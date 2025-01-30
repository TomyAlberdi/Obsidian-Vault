Created: 2024-09-17 16:25
## Family Tree:
1. Computer
2. [[Infrastructure Administration]]
-- -
Ansible is a tool for managing configuration automatically and remotely, allowing centralized management of numerous servers, network devices, and cloud providers in a simple and automated way. It uses SSH to connect to servers and execute configuration tasks. Ansible allows you to control and configure nodes from a central server.
What sets Ansible apart from similar tools is that it leverages existing SSH infrastructure. The project originated in 2013 and was acquired by Red Hat in 2015.
## Advantages
1. **No Agents:**  
   Ansible doesn't require agents to be installed on the systems it manages. As long as the target system is accessible via SSH and can run Python, Ansible can configure it.
2. **Idempotent:**  
   Ansible’s architecture revolves around idempotency, meaning that configurations are applied only if needed and can be repeatedly applied without causing unintended side effects.
3. **Declarative:**  
   Unlike scripts, where you need to write the logic for configuring systems, Ansible allows you to describe the desired state of a server or group of servers. Ansible ensures this description is applied in an idempotent manner.
4. **Easy to Learn:**  
   Ansible is designed to be user-friendly and easy to pick up.
### Idempotency:
Idempotency is defined as the property of performing an action multiple times while still achieving the same result as if it were done just once. In modern infrastructure processes, where configurations are defined as code and often declaratively, idempotency is essential for achieving high predictability.
## Architecture
![[Computer Science/Infrastructure Administration/attachments/image 7.png]]
### Inventory:
The inventory is a list of nodes that Ansible can access. By default, the inventory is supported by a configuration file located at `/etc/ansible/hosts`. Nodes can be listed by name or IP and grouped into categories like "web servers" or "db servers." The inventory can be written in formats such as YAML or INI, with YAML being the most widely used in the industry.
**Example**:
```ini
mail.example.com

[webservers]
foo.example.com
bar.example.com

[dbservers]
one.example.com
two.example.com
three.example.com
```
### Playbooks:
Playbooks are YAML files that describe the desired state of the systems you want to configure. Ansible takes care of applying this description to the servers, regardless of their current state. Playbooks make new installations, updates, and daily management repeatable, predictable, and reliable. They are simple to write, maintain, and evolve.
Playbooks contain **Plays**, which include **Tasks**. Tasks invoke **Modules**.
**Example:** This playbook installs the latest version of Apache and ensures it is running on servers listed under the `webservers` group in the inventory.
```yml
- hosts: webservers
  remote_user: root

  tasks:
  - name: Ensure Apache is installed.
    yum:
      name: httpd
      state: latest

  - name: Ensure Apache is running.
    service:
      name: httpd
      state: started
      enabled: yes
```
### Modules:
Ansible includes over 1000 modules for automating various aspects of an environment. Modules can be seen as plugins that do the actual configuration work. Modules are independent and can be written in any standard scripting language (Python, Perl, Ruby, Bash, etc.). One of their core principles is **idempotency**.
**Example**: You can invoke modules directly from the command line to test them or perform specific tasks.
```sh
ansible 127.0.0.1 -m service -a "name=httpd state=started"
ansible localhost -m ping
```
### Python:
Ansible is developed in Python, which influences some of its features. You don’t need to be a Python developer to use Ansible, but some familiarity with Python concepts can be helpful.
- **Templating Language (Jinja2):** Allows you to dynamically generate content in playbooks.
- **Ternary Operator:** Can be used within Jinja templates to alter playbook behavior based on conditions.
- **Error Handling:** Errors in Ansible may appear in formats familiar to Python developers, which can make debugging easier.
## Use cases
1. **Provisioning:** 
   Ansible can be used to instantiate servers or virtual machines, configuring the virtualization system.
2. **Configuration Management:**  
   Manage and maintain server configurations.
3. **Application Deployment:**  
   Distribute and deploy applications.
4. **Continuous Delivery:**  
   Use Ansible as part of a CI/CD pipeline to automate deployment after code compilation.
5. **Security and Compliance:**  ]
   Ansible’s idempotent nature makes it a reliable tool for distributing security-related configurations, regardless of the current state.
6. **Orchestration:**  
   It can orchestrate cloud operations or "configure" cloud resources.
## Configuration Management with Ansible
Ansible is the simplest tool for implementing a configuration management strategy. It is designed to be minimalist, consistent, secure, and highly reliable. Any developer, tester, or infrastructure administrator can easily use Ansible to configure a set of nodes. Moreover, any IT personnel can write and understand a playbook, as the configurations are described in a human-readable format.
Ansible only requires the password or private key of the user who will be used to access the systems being configured.