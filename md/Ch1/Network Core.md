## Network Core
### Packet Switching
1. End systems exchange *messages* which are broken into *packets* through communication links + packet switches
2. Packets are transmitted over link at a rate equal to the *full transmission* rate of the link

#### Store-and-Forward Transmission
Def: Packet switch must receive the entire packet before onto the outbound link

R: Link transmission rate: bits/second
L: size of packets: bits

* Ignore propagation delay(time taken for the bits to travel across the wire ate near the speed of light), time taken to transmitted is 2L/R
L/R to the router, L/R to the end system
* Otherwise (Not using S-a-f, still ignore propagation dalay), time = L/R

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

Internet has a number of special routing protocols that determine the shortest path and configures forwarding tables.

### Circuit Switching
Another approach to pass data

1. In circuit-switched networks, the resources needed to be reserved for the duration of communication

2. The network firstly establish a stable connection so that they can transfer information, which is called a **circuit**.

3. Also, it also reserves a constant transmission rate (which is guaranteed)

4. In contrast, packet-switched network does not reserving any link resources

* In practice, when 2 hosts would like to communicate, the networks establishes a dedicated **end-to-end connection**
* If there are N circuits/cables for each link, the connection gets $\frac{1}{N}$ transmission capacity

#### Multiplexing in Circuit-Switched Networks
A circuit in a link is implemented with either 
* FDM (frequency-division multiplexing) 
  * uses frequency spectrum of a link which is segmented among the connections
  * Each band is assigned a **bandwidth** (e.g. 4kHz)
* TDM (time-division multiplexing)
  * Time is divided into frames, each frame is divided into **time slots**
  * Each slot is sole use of that connection for transimission
* Circuit switching is wasteful since circuits are idle during **silent periods**
* Establishing and reserving this end-to-end transmission capactity is complicated and requires complex signaling software to coordinate the operation of the switches 
* Note: Transmission time is independent of the number of links

#### Packet Switching Vs Circuit Switching
* Circuit switching pre-allocates use of the transmission link regardless of demand, with allocated but unneeded link time going unused.
* Packet switching allocates link use on demand.

### A Network of Networks
Access ISPs are interconnected -- *network of networks*

* *Network Structure 1*
  * One global transit ISP
  * at least one router near each ISPs
  * connects to each access ISPs
  * charge each of the access ISPs 
  * Access ISP: **customer**
  * Global transit ISP: **provider**
* *Network Structure 2* 
  * Multiple global transit ISP
  * interconnects with each other
  * 2-tier hierarchy
* *Network Structure 3*
  * Multiple tier-1 ISPs (similar to global transit ISP)
  * including Level 3 Communications, AT&T, Sprint, NTT...
  * Multi-tier hierarchy
  * since need to be economically desirable
  * multiple Regional ISP
* *Network Structure 4*
  * PoPs (Points of Presence)
    All levels of hierarchy, except for the bottom level
    * PoP: a group of one or more routers (at the same location) in the provider's network so that the customer ISPs can connect
  
      So that the customer ISP can lease a high-speed link from a third-party telecommunications provider to directly connect one of its routers to a router at the PoP
  * multi-homing: coonnect to two or more provider ISPs
  
    Can also connect to the Internet even if one of its providers has a failure.

  * peering
    Since the cost of the connection is reflecting the traffic, to reduce the cost, we can connect directly (may using cables) with the nearby ISPs, instead of through upstream intermediaries

  * IXPs(Internet exchange points)
    A third-party company create IXP which is a meeting point where multiple ISPs can peer together.
* *Network Structure 5*
  * NS 4 + **content-provider networks**
    * Private TCP/IP network
    * nevertheless seperate from the public Internet
    * only carries traffic to/from Google servers
    * bypass the upper tiers of Internet by peering with lower-tier ISPs
      * directly connecting 
      * connecting at IXPs
    * Inevitably, have to connect to tier-1 ISPs
  * Pros of own network
    * reduces costs to upper-tier ISPs
    * gretaer control of how its services delivered
