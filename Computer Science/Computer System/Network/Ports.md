Created: 2024-09-16 20:30
## Family Tree:
1. Computer
2. [[Network]]
-- -
When we need to access a service from the Internet, it is absolutely necessary to open a port on our router.
We currently have two protocols in the transport layer: TCP and UDP. Therefore, depending on the type of service we want to use, we will have to open the TCP or UDP port, although there could also be services that need to open both TCP and UDP ports simultaneously.
Within Internet communication, the TCP and UDP protocols are responsible for establishing the connection, assembling the data packets after transmission, and then sending them to the programs they were intended for on the receiver.
For this transfer to take place, the Operating System must generate and open entries. Each entry is assigned a specific identification number.
After transmission, the receiving system knows where to deliver the data thanks to the port number. The data packet always includes two port numbers: the sender's and the receiver's. Ports are numbered consecutively from 0 to 65535. Some of these numbers are standardized and assigned to certain applications. The Internet Assigned Numbers Authority (IANA) is responsible for registration.
Alongside these, there is also a wide range of port numbers that are assigned dynamically. A browser uses such a port during a visit to a web page. Once the user leaves the page, the number becomes free again.
The TCP protocol is a connection-oriented, reliable protocol. This means it can retransmit packet segments in case of loss from the source to the destination. If we are using any protocol in the application layer — such as HTTP, FTP, or SSH, all of which use the TCP protocol — this message exchange will take place in the first communication. Below, we list some of the main TCP ports used by many application layer protocols and applications:
- **Port 21:** Generally used for FTP server connections on its control channel, as long as we haven't changed the listening port of our FTP or FTPES server.
- **Port 22:** Generally used for secure SSH and SFTP connections, as long as we haven't changed the listening port of our SSH server.
- **Port 25:** Used by the SMTP protocol for sending emails. This protocol can also use ports 26 and 2525.
- **Port 53:** Used by the DNS (Domain Name System) service.
- **Port 80:** Used for non-secure web browsing (HTTP).
- **Port 443:** Also used for web browsing, but in this case, it uses the HTTPS protocol, which is secure and uses the TLS protocol underneath.
- **Port 3306:** Used by MySQL databases.
- **Port 8080:** An alternative to port 80 TCP for web servers. This port is usually used in testing.
- **Port 53:** Used for DNS services. This protocol allows the use of both TCP and UDP for communication with DNS servers.