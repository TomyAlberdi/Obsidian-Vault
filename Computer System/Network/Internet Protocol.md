Created: 2024-09-16 20:27
## Family Tree:
1. Computer
2. [[Network]]
-- -
The Internet Protocol, known by its acronym IP, is the main protocol of the Internet protocol family and its importance is fundamental for message exchange in computer networks. In other words, these are rules that govern the exchange of information through a network of computers or devices.
The IP protocol, along with the Transmission Control Protocol (TCP), lays the foundation of the internet. For the sender to send a data packet to the recipient, the IP protocol defines a packet structure that groups the data to be sent. Thus, the IP protocol establishes how the information about the origin and destination of the data is described and separates it from the useful data in the header of each information packet sent.
The IP protocol identifies each device connected to the network by its corresponding IP address. The IP address is used to uniquely identify both the device and the network to which it belongs, thus being divided into two parts:
* An address that identifies the network.
* An address that identifies the device within the network.
There cannot be two devices connected with the same IP address on the same network, and therefore not on the internet either. The IP address is unique and exclusive for each device connected to the Internet
However, we usually do not memorize IP addresses; it would be almost impossible to memorize the IPs of the websites we want to access. For this purpose, domain names were created. So every time we want to access a web page, we use its domain name, such as [google.com](http://google.com/) instead of using its IP address 78.45.789.03. The protocol responsible for these translations between domain names and IP addresses is the Domain Name System (DNS) protocol configured on our device.
## Internet Protocols:
- **Internet Protocol (IP)**
- **Transmission Control Protocol (TCP)**
- **DNS Protocol**
- **TCP/IP Protocol**: The TCP/IP (Transmission Control Protocol/Internet Protocol) consists of a combination of the previously mentioned protocols and is the cornerstone of modern computer networks.
- **UDP Protocol**: The User Datagram Protocol (UDP) is a transport layer protocol based on the exchange of datagrams (a datagram is a data packet, and a data packet is each of the blocks into which information is divided for sending). Its function is to allow the sending of datagrams over the network without a previously established connection since the datagram itself incorporates enough addressing information in its header.
- **HTTP Protocol**: The Hypertext Transfer Protocol (HTTP) is a transaction-oriented protocol and follows the request-response scheme between a client and a server. The client (usually a web browser) makes a request by sending a message, in a certain format, to the server. The server (usually called a web server) sends a response message, allowing communication between the two.
- **HTTPS Protocol**: The Hypertext Transfer Protocol Secure (HTTPS) is intended for the secure transfer of hypertext data. It encrypts the data sent between clients and servers using encryption algorithms, so all sensitive information, such as credit card numbers, phone numbers, access keys, among others, can be sent securely.