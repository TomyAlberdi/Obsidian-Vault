#Theory 
An operating system (OS) is a set of programs that allows managing memory, disk, information storage media, and the different peripherals or resources of our computer. Based on what has been studied so far, we could say that an operating system is the [[software]] that manages the hardware; that is, it administers the resources offered by the hardware and acts as an intermediary between the computer and its user. From the user's point of view, it is a set of programs and functions that hide the hardware details, offering the user a simple and flexible way to access it.
### Tasks of the operating system:
- Manages random access memory and runs applications, allocating the necessary resources.
- Administers the CPU, thanks to the scheduling algorithm.
- Directs data input and output (through drives) via input and output peripherals.
- Manages information for the proper functioning of the PC.
- Directs user access permissions.
- Manages files.
### Types of operating systems:
#### By User:
- **Multi-user:** Multi-user operating systems can serve multiple users simultaneously, either through terminals connected to the computer or remote sessions on a communication [[network]]. Examples of these operating systems can be Unix, Linux, or Solaris.
- **Single-user:** Single-user operating systems, as the name suggests, support only one user at a time, regardless of how many processors the computer has or how many tasks the user performs, it can only serve one. Examples could be the early versions of Windows for home computers, like Windows 1.0.
#### By task management:
- **Multitasking:** Multitasking operating systems allow us to perform several tasks simultaneously; these are much more common today.
- **Single-tasking:** Single-tasking operating systems are characterized by being able to perform only one task at a time without interruption. These are the most primitive operating systems, like DOS. For example, if we want to print a file on these operating systems, we will not be able to perform any other task until the computer prints and can receive another instruction.
### Types of internal structures:
- **Monolithic:** The monolithic structure consists of a single program composed of a series of interwoven routines, so they can communicate with each other. These operating systems are usually custom-made, so they are very fast but lack flexibility to support different types of applications.
- **Hierarchical:** As user needs grew and systems improved, greater organization of the operating system software became necessary, where one part of the system contained subparts and was organized in levels. This operating system is known as a hierarchical structure, as it is subdivided into layers or rings, perfectly defined and with a clear interface concerning the rest of the resources.
- **Virtual Machine:** Virtual machine-type operating systems separate two concepts that are usually united in other systems: multiprogramming and the extended machine. The goal of virtual machine operating systems is to integrate different operating systems, giving the impression of being several different machines.
- **Client-Server:** The client-server operating system serves all kinds of applications, so it is general-purpose and performs the same activities as conventional operating systems. The idea is to maintain the user's view of a personal computer, but the [[network]] allows sharing disk space or the printer to economize resources.
#### Client-Server Architecture:
The client-server architecture aims to process information in a distributed manner. This way, they can be dispersed in different locations and access shared resources. Besides transparency and independence from hardware and software, a client-server implementation must have the following characteristics:
- Use asymmetric protocols, where the server waits for a client to initiate a request.
- Transparent, multi-platform, and multi-architecture access.
- Facilitate scalability, making it easy to add new clients to the infrastructure (horizontal scalability) or increase the server's power by adding more servers or enhancing their computational capacity (vertical scalability).
##### Components:
- **Client:** Generally refers to a computer with limited capabilities, but in client-server environments, it is called the front end, as it requests services from the server through a user request. A client process interacts with the user and is built with tools that allow implementing graphical interfaces (GUI).
- **Server:** Generally a high-performance computer, but in this context, a server is a process that offers resources and services to clients that request them (back end). Depending on the type of server implemented, we will have a different type of client-server architecture. Centralized programs and data facilitate integrity and maintenance.
- **Middleware:** The part of the system software that handles message transport between the client and server and facilitates the interconnection of heterogeneous systems without using proprietary technologies. It runs on both sides of the structure. Middleware allows clients and servers to be independent and offers more control over the business by gathering information from different sources and offering it jointly. Another feature is that systems are loosely coupled, interacting through message exchange.
### Fundamental Characteristics of an Operating System:
- **[[Network]] Support:** Essential for providing connectivity.
- **Wide Hardware Compatibility:** Crucial for fully utilizing the server's features, prioritizing updated OS with significant driver support.
- **Security:** Vital for the server's role, requiring up-to-date OS with strict access policies, firewalls, and antivirus. Backup tools are also necessary to minimize data loss in case of fatal failures.
- **Fault Tolerance:** Prioritize OS architectures that allow fault tolerance, such as server farms that operate as a single processing unit, where another server can take over if one fails.
Given these almost non-negotiable characteristics when choosing a server OS, it's common to ask why specific OS versions are used for servers and not the same OS installed on our computers or workstations. This is based on some differences:
- **Different Hardware Management:** Due to different purposes, workstation OS cannot utilize all available hardware, such as RAM management (e.g., Windows 10 64-bit can handle 6TB of RAM, while Windows Server 2019 can handle 24TB).
- **Supported Features:** Some functionalities are not natively available in workstation OS due to kernel limitations or disablement (e.g., virtualization in some Windows 10 versions).
- **Support:** When our business or application depends on an OS, the support provided by the manufacturer/developer is crucial. Workstation OS support is specific, and deploying a web server architecture on it might work but lack technical support, as the manufacturer will indicate that the "Server" version is for that purpose.
### Services Offered by Operating Systems:
A service is an entry point the OS offers to execute programs, manipulate files, or allocate resources.
##### Web Publishing Service:
Software that dispatches website content to the user. The dispatch process starts in the web browser, performing a DNS search to find the hosting server, requesting the site content, and the web server processes and sends the content to the browser, resulting in site visualization. Commonly used: Apache (multi-platform), Internet Information Services (Windows), Nginx (multi-platform), LiteSpeed (Linux).
##### Database Service:
A [[database]] server organizes information using tables, indexes, and records. Increasingly popular are non-relational databases (No-SQL). The fundamental function is to provide information to other web applications or hosts, allowing tasks like selection, update, and deletion of data. Commonly used: MySQL, PostgreSQL, Microsoft SQL SERVER, Mongo DB.
##### Email Service:
A mail server sends and receives emails between hosts, users, or servers, handling message processing, filtering, storage, sending, receiving, and forwarding. It uses the TCP/IP protocol for global communication. Components: MTA (Mail Transport Agent) transfers emails between hosts, and MDA (Mail Delivery Agent) receives emails from MTA and delivers them to the inbox, communicating with POP or IMAP servers.
##### File Service:
A central server in a [[network]] that provides file access to connected clients, offering centralized storage available to authorized users. File sharing services depend on client platforms. Commonly used: CIFS/Samba (Linux), NTFS Share (Microsoft), NFS (UNIX).
##### [[Network]] Service:
OS services used for routing, firewall, or proxy needs, often based on Linux systems with packages/software resulting in routers, firewalls, or proxies. Commonly used: PFSense (BSD-based), OPNSense (derived from PFSense and Monowall), DD-WRT (Linux-based, used in home routers).
##### Domain Services:
A domain controller (DC) authenticates and verifies users in computer [[Network]], organizing users and devices hierarchically. The DC's main responsibility is to authenticate and validate user access. Commonly used: Active Directory (Windows, using LDAP, Kerberos, and DNS), NIS and NIS+ (Linux, originally YellowPages), and LDAP implementations in Linux coexisting with Active Directory.