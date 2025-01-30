Created: 2024-09-16 20:23
## Family Tree:
1. Computer
2. [[Network]]
-- -
Just as people's homes are identified and located through a numbering system or addresses, the way to locate computers within the respective network they connect to is through addresses. These can be:
## MAC Address:
The MAC address or Physical Address is a unique and unrepeatable address that identifies a single device in the world. All devices have a MAC address, which is assigned by the manufacturer at the time of the creation of the connection device. It is composed of 48 bits, which are alphanumeric, and are divided into two segments, where one identifies the manufacturer and the other the device.
Example: `01:3A:1D:54:6B:32`
- `01:3A:1D` : Manufacturer's Unique Identifier (OUI)
- `54:6B:32` : Product Identifier (UAA)
## IP Addresses:
An IP address is a unique number that represents the location of a device within the Internet or within a network. It is a string of numbers separated by dots. This address can be IPv4 or IPv6.
IPv4 addresses are expressed as a set of four numbers, such as 192.158.1.38. Each number in the set can range from 0 to 255, and therefore, the full IP addressing range goes from 0.0.0.0 to 255.255.255.255.
There are two types of IP addresses: public and private.
- **Public IP Addresses:** These addresses are all those that serve to identify us on the Internet, that is, to identify devices on the big network.
- **Private IP Addresses:** These are the numbers assigned to a device within a private network. That is, to identify our cell phone or notebook within the same Wi-Fi network at home. Certain address ranges are reserved for this purpose.
- **Static or Dynamic IP Address**: The IP address will be static or dynamic depending on whether it is always the same or changes over time. Depending on the case, it will be assigned by the Internet service provider, a router, or the administrator of the private network to which the device is connected.
### Subnet Mask:
A subnet is a combination of numbers that serves to delimit the scope of a computer network. The TCP/IP protocol uses the subnet mask to determine if a host is on the local subnet or on a remote network. Its function is to indicate to the devices which part of the IP address is the network number, including the subnet, and which part corresponds to the host.
IP numbers have a part that corresponds to the network and another that corresponds to the host: 
* 192.168.80.1 ➡️ 1 = host.
How does the system distinguish which part is the network and which part is the host? Through the subnet mask:  
* 192.169.80.1 ➡️ IP number 
* 255.255.255.0 ➡️ Subnet mask
The subnet mask will assign the 255 to the position of our IP that does not vary and put a 0 to the variable.
### Important IP Addresses:
There are some IPs within networks that only one device can have, so if another device assigns itself one of them, the network might not function correctly.
- **Router:** The first available address (e.g., 192.168.1.1) corresponds to the router, the device that links with other networks, such as the Internet. Thus, all devices that want to query something on the Internet must first send the request to the router's address, which will handle redirecting the request.
- **Broadcast:** It is the highest address in the network to which the device belongs and is used by the router to send a broadcast message to all devices that have an assigned IP within the network. In home networks, it is usually 192.168.1.255.
### IPv6 Addresses:
IPv6 is version 6 of the Internet protocol. It is intended to replace the IPv4 standard, as the previous version has a limit of network addresses that prevents its growth.
**Advantages of IPv6:**
- **Almost unlimited number of unique IPs:** This new protocol allows each device connected to the Internet to have its own IP address. An advantage that is gradually becoming a requirement with the continuous advancement of the Internet of Things.
- **Autoconfiguration:** It has better methods for automatic configuration, which is a significant improvement over the classic DHCP used in IPv4.
- **More security:** The IPv6 protocol can be enhanced with IPsec (Internet Protocol Security) to manage encryption and authentication between hosts. It provides a solid end-to-end security framework for data transfer.
- **More efficiency:** Packet management is much more efficient in IPv6.