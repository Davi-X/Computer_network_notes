## Principles of Network Application
Core is to write applications that run on different end systems and communicate with each other over the network
* Web application
  * Browser on user's host
  * Web server program on server host
* P2P file-sharing system
    One program in each host

Can only write software that run on end systems

2 predominant architectural paradigms
* client-server 
  * clients do not directly communicate with each other
  * Each server has an IP address
  * Data center for keeping up with all requests
  * Each can have hundreds of thousands of servers
  * Service providers must pay recurring interconnection & bandwidth costs
* P2P
  * Minimal (/ no) reliance on dedicated servers
  * Most traffic-intensive applications are based on P2P
  * **self-scalability**
  * cost effective
  * potential risks of security, performance and reliability
* Hybrid
  e.g. servers track users' IP addresses, messages are sent in P2P

### Processes Communicating
* It is not programs communicating, but **processes**
* On the same end system, processes communicate through interporcesses communication
* Interested in how processes running on different hosts(possibly different OS) communicate
* On two different end systems, processes communicate by exchanfing messages 

#### Client and Servcer Processes
A network application consists of pairs of processes.
* Client: The process that initiates the communication
* Server: The process that waits to be contacted to begin the session

#### The Interface Between the Process and the Computer Network
**Socket**: The network through a software interface
where messages need to pass through
* also referred as the **API(Application Programming Interface)** between application and the network
* Application developers have little control of the transport-layer side 
  * choice of transport protocol
  * fix a few parameters
    * max buffer
    * max segment sizes
    * ...

#### Addressing Processes
Uses IP address to specify two hosts
IP address: 32 bit 
Sending process must also identify the receiving process running in the host (Which kind of message for which process)
(Since a host could be running many network applications)

Here introduce **port number**
* Web server: 80
* Mail server: 25
* ...

### Transport Services Available to Applications
Classify services (Transport-layer) along dimensions:
1. Reliable data transfer
   * Loss-tolerant applications (e.g. multimedia apps)
   * Otherwise  
     need protocol to provide reliable data transfer (process-to-process) to prevent devastating consequences
2. Throughput
   * The rate at which the sending process can deliver bits to the receiving process
   * Service: guaranted available throughput at sine specified rate
   * Bandwidth-sensitive apps: Apps that have throughput requirements
     * Many multimedia apps
   * Elastic apps: otherwise
     * Electronic mail
     * File transfer
     * Web transfer
3. Timing
    * Appeal to interactive real-time applications
    * e.g. socket to socket no more than 100 msec later
    * Non-real-time applications, no tight constraint is placed on delays
4. Security 
  * Confidentiality (Encrypt + decrypt...)
  * Data integrity
  * end-point authentication

### Transport Services Provided by the Internet
* TCP
  * Connection-oriented (Handshaking)
    TCP connection exist after handshaking, be tour down when finishes
  * Reliable data transfer service
    TCP ensures no missing or duplicate bytes
  * congestion-control (benefits network not processes)
    throttles process when network is congested between two processes
* UDP
  * Connectionless (No handshaking)
  * unreliable data transfer
  * may arrive out of order
  * not include congestion-control mechanism
    So the sending side can pump data into the next layer at any rate it pleases
* TCP-enhanced-with-SSL 
  * Not a third transport protocol, but replace the general socket as the the SSL (Secure Sockets Layer)
  * Needs to include SSL code in both the client and server sides to implement it
  * Then pass the encrypted data to the normal TCP
  
#### Services Not Provided by Internet Transport Protocols
Throughput and timing guarantees services are not provided by today's Internet transport protocols

Internet provide satisfactory service to time-sensitive apps, but not guarantees about timing or throughput

Most of applications prefer TCP now even if multimedia apps cause many firewalls would block UDP traffic. So TCP in this situation would use TCP as a backup

### Application-Layer Protocols
Other details are defined in application-layer protocol
* Types of messages exchanged
* Syntax of various message types
* Semantics of the field
* Rules for determining when & how a process communicates

* In the public domain
  * Specified in RFCs
* Private domain
  * use proprietary protocols

Application-layer protocol is only one piece of a network application

Web App (HTTP example)
* A standard for document formats(HTML)
* Web browsers
* Web servers (Apache & Microsoft servers ...)
* Application-layer protocol (HTTP)
  
Internet Email App (SMTP example)
* Mail servers
* Mail clients (Outlook...)
* A standard for defining the structure 
* Application-layer protocol (SMTP)