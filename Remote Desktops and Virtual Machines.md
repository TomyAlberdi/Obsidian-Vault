#Theory 
## Remote Desktops:
A remote desktop is a technology that allows a user to work on a computer through its graphical desktop from another terminal device located elsewhere.
## Virtual Machines:
Servers generally used only 30% of their total capacity, so the other 70% was constantly wasted. To solve these resource underutilization problems, virtualization was created, allowing multiple [[Operating System|operating systems]] to run on the same machine, simulating real [[Computer|computers]].
### Images:
An image in computing can be divided into two forms:
1. The digital form of a photo. That is, a moment is captured through a digital camera, where what the photographer sees is immortalized in a set of bits in a file, for example, in a .jpg format.
2. Instead of capturing a moment, it "photographs" configurations and data from a file system, like a program or system. The most well-known or used format of the second type of images is `.iso`, which is generally used to make copies of entire file systems. This way, the image of a program or operating system can be transferred and installed on any computer.
### Operating System Execution:
Currently, guest operating systems of the Microsoft and Linux types can be created in almost all their versions. The versions of each operating system and compatibility with the host system must be considered.
### Virtual Machine Manager:
From the management tool, all physical and virtual resources of the guests, which are the virtual instances created for specific uses, are managed. From the same management, clustering with other virtual machine managers can be established for high availability and fault tolerance. Additionally, it manages all virtual resources of our virtual machines.
### Base Operating Systems:
This is the operating system responsible for managing physical devices (hardware) and providing an abstraction layer to virtual environments.
### [[Hardware]] (physical servers):
Microprocessors, both Intel and AMD, have a feature called CPU virtualization. It applies to servers or desktop machines.
### Benefits of Virtualization:
- **Efficiency:** Allows [[software]] and hardware updates of virtual machines without significant impacts on the productivity of the involved systems.
- **Uptime:** Has the ability to avoid unnecessary downtime by maximizing resource utilization. Even economical virtualization services can offer almost 99.99% uptime.
- **Cost:** Using a virtualization system is more economical as it does not require any hardware components.
- **Deployment:** Resource implementation is considerably faster when using virtualization technology. The time spent creating local [[Network|networks]] or configuring physical machines can be significantly saved. Therefore, all you need is at least a single access to the virtual environment. Additionally, deploying virtual machines is simpler than deploying physical versions, having ready-to-deploy images beforehand.
- **Energy Savings:** Using virtualization means the system is more energy-efficient as no hardware or software beyond what is intended for virtualization is used.
- **High Availability:** Many virtualization systems allow the use of virtual machines with the HA (High Availability) option, ensuring redundancy between 2 or more environments. This guarantees that in case of a failure in one of them, there is no service disruption.
- **Backups:** Backups of the virtual server can be made, and virtual machines can migrate between each other. The disaster recovery process is very simple in a virtualized environment. By having a "backup" of the guest machine's hardware configuration files and a copy of the virtual disks, it is enough to quickly recover the entire environment.
- **Snapshots:** These provide a record of changes for the virtual disk and are used to restore a virtual machine to a particular point in time when a failure or error occurs in the system.