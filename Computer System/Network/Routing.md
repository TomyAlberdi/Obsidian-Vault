Created: 2024-09-16 20:33
## Family Tree:
1. Computer
2. [[Network]]
-- -
With the evolution of networks, the way information is transmitted has also evolved and is now done through routing. This method interconnects computers using devices called routers, which are responsible for establishing the path that information must follow to reach its destination.
**Functions of the router in the network:**
- Receives data packets.
- Searches for the destination address.
- Checks the configured routing table.
- Proceeds to send the packet to its destination via the best possible route.
#### How does a router send and receive information?
It uses routing tables, which are a set of rules that determine the path data packets should follow. The routing tables contain all the necessary information to ensure that one or more data packets can travel through the network using the best possible path.
#### Components of a routing table:
- **Destination network:** Corresponds to the destination network where the data packet should go.
- **Next hop:** The IP address of the network interface through which the data packet will travel to continue its journey.
- **Outgoing interface:** The network interface through which the packets must exit to subsequently reach their destination.
### Types of routing:
#### Static Routing:
The tables are created manually. The network administrator configures them with information on how to reach different remote networks. This person is responsible for ensuring the networks are accessible and free of bugs and inconsistencies.
- **Advantages:** Although maintenance is complicated, no network bandwidth is consumed to send messages between routers.
- **Disadvantages:** Any change in the network requires the administrator to add or remove routes affected by those changes.
- **Characteristics:**
    - Consumes less bandwidth.
    - Consumes less memory.
    - Used for small networks.
    - Not scalable.
#### Dynamic Routing:
The information needed to create and maintain updated tables is obtained from other routers in the network. These use routing protocols to exchange information with their neighboring routers.
- **Advantages:** The administrator only initiates automatic routing, then the routing tables adjust automatically to changes in the network.
- **Disadvantages:** Consumes a lot of bandwidth due to the messages exchanged by routers to configure themselves automatically.
- **Characteristics:**
    - High bandwidth consumption.
    - High memory consumption.
    - Used for large networks.
    - Automatic.