Created: 2024-09-16 20:29
## Family Tree:
1. Computer
2. [[Network]]
-- -
It is a conceptual interconnection model that allows various systems to communicate through a standard. It can be understood as a universal communication language between networks, computers, servers, etc., based on the idea of dividing a communication system into seven layers where each one works on the previous one. We can say that each layer contains data units that are converted into those of the upper layer.
### Physical Layer: Bits
This layer involves the physical devices participating in data transfer and converting them into a sequence of bits. In other words, it represents the change from electricity to bits.
### Data Link Layer: Frames
Facilitates data transfer between two devices located on the same network. It takes the packets from the network layer and breaks them into smaller pieces called frames. Like the network layer, this layer is responsible for flow and error control within that network communication. It contains the "MAC Address (Addresses > MAC Address)" sublayer that helps control the flow of data packets to and from a network interface card through a shared channel in a network.
### Network Layer: Packets
Responsible for enabling data transfers between two different networks -the concept of routing. Its goal is to fragment, in the sending device, the transport layer data into smaller units called packets and reassemble them later in the receiving device. The network layer also seeks the best physical path for the data to react its destination, known as routing. Some call it the Internet layer.
### Transport Layer: Segments
This layer is responsible for coordinating data transfer across network connections. It helps regulate various elements involved in data transmission between end systems and hosts. These factors include the size, sequence, speed, and destination of the data packet. Once the transport layer has effectively managed and verified the data packets, they pass to or from the network layer. Some of the best-known examples of the transport layer include the Transmission Control Protocol (TCP) and the User Datagram Protocol (UDP).
### Session Layer: Data
Responsible for opening and closing communications between two devices, its function is to create a session or connection that allows two devices to communicate with each other. Once the session is formed, the data is passes to the transport layer. In addition to setting up a session, the resulting connection between the machines is also managed and terminated once the session ends in this layer. The session layer is also responsible for authentication and reconnection in case of network interruption.
### Presentation Layer: Data
The main function of this layer is to define the format and encryption of the data, manage network security and confidentiality, compression, and text packaging. It encodes messages from the user-dependent format to the common format and vice versa for communication between different systems.
### Application Layer: Data
This is the layer that interacts with user data. Software applications, such as web browsers and email clients, depend on the application layer to initiate communications.