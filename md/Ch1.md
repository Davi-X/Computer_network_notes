# Computer network and Internet
Internet is a network of network
## What is Internet?

### Hardware + Software components overview
All devices connected to the internet are categorized by  hosts & end systems

End Systems are connected by a network of **communication links** and **packet switches**
* Each communication has its transmission rate measured in bit/second
* Data segement + header bytes known as **packets**
* Packet switches 
  takes a packet arriving on one of its incoming communication links and forwards that packet on one of its outgoing communication links
  * Routers (Access network)
  * Link-layer switches (Core)
* Sequence of communication links and packet switches traversed by packets is known as *path* / *route*

#### ISP
End systems access the Internet through ISP(Internet Service provider)
Each ISP ia a network of communication links and packet switches

Each ISP is interconnected and managed independently, runs the IP protocols, conforms to certain naming and address conventions

Lower-tier ISPs are interconnected through national and international upper-tier ISPs 

upper-tier ISPs consists of high-speed routers and interconnected with high-speed optics fibers

#### Protocols 
Definition:  
A protocol defines the format and the order of messages exchanged between two or more communicating entities, as well as the actions taken on the transmission and/or receipt of a message or other event.
* TCP/IP
    * TCP (Transmission Control Protocol)
    * IP (Internet Protocols)
* Internet Standards
  developed by IETF(Internet Engineering Task Force)
* IETF Standards Docs 
  is called RFCs(Requests for comments)

### From Infrastructure of Service view
Internet can also be regarded as *Infrastructure that provides services to applications* 

These applications are called **Distributed Applications** which involves with multiple end systems

Q: How does the Internet help end systems to deliver data?
A: End Systems attached on the Internet provides a **Socket Interface** which consists of rules for program to deliver data

## The Network Edge
* Edge of the Network:
    Applications and End systems
* Access network:
  Network which physically connects end systems to the first router (*edge router*)

Two most prevalent types of broadband residential access:
* DSL (Digital Subscriber Line)
  DSL is offered by the same company(telco), your local telephone company

  * The data are translated digital data to high-frequency tones to the CO, converted back to digital format by DSLAM (Digita Subscriber Line Access Multiplexer).

  * Data and telephone signals are transmited by the same wire simultaneously, which are encoded at different frequencies

  * DSL providers purposelly limit the residential rate
  1. Different rate, different prices
  2. Max rate would be limited due to some reasons
      * Distance
      * Gauge of the twisted-pair line
      * Degree of electrical interference
* Cable Internet Access
  Since both fiber and coaxial cables are involved, also referred as 'HFC (Hybrid fiber coax)'
  1. Fiber optics connect the cable head end to the neighborhood-level junctions, each could support 500-5000 homes
  2. Then use coaxial to reach individual house 
  3. Use Cable Modems
  4. CMTS (Cable Modem Termination System) plays the role similar with DSLAM at the head end of cable (CO of cabel television company)
  5. It **shares broadcast medium**, so if many users are reuqesting the web simultaneously, the stream would be very low
  6. For this reason, it also needs a distributed multiple access protocol to coordinate transimisson and avoid collisions
* FTTH (Fiber to the Home)
  TODO

## Network Core
### Packet Switching
1. End systems exchange *messages* which are broken into *packets* through communication links + packet switches
2. Packets are transmitted over link at a rate equal to the *full transmission* rate of the link

#### Store-and-Forward Transmission
Def: Packet switch must receive the entire packet before transmisson

R: Link transmission rate: bits/second
L: size of packets: bits

* Ignore propagation delay(time taken for the bits to travel across the wire ate near the speed of light), time taken to transmitted is 2L/R
L/R to the router, L/R to the end system
* Otherwise, time = L/R

* Multiple packets, one router, delay = m * L / R
* One packet, N links (N - 1 routers), delay = N * L / R

#### Queuing Delays and Packet Loss
For each attacked link of the packet switch, it has an **output buffer/queue** which stores packets that the router is about to send into that link.

So that if an arriving packet finds the link is occupied by other packets, it will wait in the buffer, which cause **queuing delay**.

Since the queue is finite, if there are packets arriving in the full buffer, either the arriving packet or some packet in the queue would be discarded, which cause the **packet loss**

Mind the speed of the router sending and receiving packets, which may cause the Internet congestion would discard packets

#### Forwarding Tables and Routing Protocols
Packets forwarding from routers is done differently by types of networks.

Every end system has an unqiue IP address, and that of destination is included in the packet header.

Since the IP address is in hierarchical structure, the router examines the portion of IP address and send to the corresponding router (appropriate outbound link).

In this mechanism, each router has a **forwarding table** that maps portions of destination addresses to the outbound links 

Internet has a number of special routing protocols that are used to automatically set the forwarding tables.

### Circuit Switching
Another approach to pass data

1. In circuit-switched networks, the resources needed to be reserved for the duration of communication

2. The network firstly establish a stable connection so that they can transfer information, which is called a **circuit**.

3. Also, it also reserves a constant transmission rate (which is guaranteed)

4. In contrast, packet-switched network does not reserving any link resources

* In practice, when 2 hosts would like to communicate, the networks establishes a dedicated **end-to-end connection**
* If there are N circuits/cables for each link, the connection gets $\frac{1}{N}$ transmission capacity

#### Multiplexing in Circuit-Switched Networks
TODO

#### Packet Switching Vs Circuit Switching
* Circuit switching pre-allocates use of the transmission link regardless of demand, with allocated but unneeded link time going unused.
* Packet switching allocates link use on demand.

### A Network of Networks
Access ISPs are interconnected -- *network of networks*

* *Network Structure 1*
  * One global transit ISP
  * connects to each access ISPs
  * charge each of the access ISPs 
  * Access ISP: **customer**
  * Global transit ISP: **provider**
* *Network Structure 2* 
  * Multiple global transit ISP
  * interconnects with each other
  * Two-tier hierarchy
  * economically desirable
  * Reality
    * Regional ISP
    * connects to tier-1 ISPs
    * including Level 3 Communications, AT&T, Sprint, NTT...
* *Network Structure 3*
  * PoPs (Points of Presence)
    All levels of hierarchy, except for the bottom level
    * PoP: a group of one or more routers (at the same location) in the provider's network so that the customer ISPs can connect
  
      So that the customer ISP can lease a high-speed link from a third-party telecommunications provider to directly connect one of its routers to a router at the PoP
  * multi-homing: coonnect to two or more provider ISPs
  
    Can also connect to the Internet even if one of its providers has a failure.
  * peering
  * IXPs(Internet exchange points)
  * 