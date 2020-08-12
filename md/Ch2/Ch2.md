# Application Layer
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
Sending process must also identify the receiving process running in the host
(Since a host could be running many network applications)

Here introduce **port number**
* Web server: 80
* Mail server: 25
* ...