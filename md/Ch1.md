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

## Delay, Loss and Throughput in Packet-switched Networks

### Overview of Delay in Packet-Switched Networks
Packet suffers from several types of delays at each node
* Nodal processing delay
* Queuing delay
* Transmission Delay
* Propagation Delay
* ...
These are accumulated to called **Total nodal Delay**

#### Types of delays (Nodal delay / single router)
* Processing Delay
  * examine the packet's header
  * determine where to direct the packet
  * check for bit-level errors (from upstream to router)
  * Then send to the buffer or send directly
  * Microseconds or less
* Queuing Delay
  * Depend on the number of earlier-arriving packets that are queued and waiting
  * microseconds ~ milliseconds
* Transmission Delay
  * First-come-first serverd manner
  * Store-and-forward mechanism
  * delay = L/R (talked above)
  * microseconds to milliseconds
* Propagation Delay
  * Time reuqired to propagate from the beginning of the link to another router
  * Propagation speed depends on the physical medium of the link
    (equal or a little less than the speed of light)
  * t = d/s (d = distance / s = propagation speed)
  * Milliseconds
* Difference between Propagation delay & Transmission delay
  * Propagation Delay: time from a tollbooth to the next toolbooth
  * Transmission Delay: time for tollbooth to serve the car
* $d_{nodal} = d_{proc} + d_{queue} + d_{trans} + d_{prop}$
  * $d_{proc}$ is always negligible, it strongly influences a router's maximum throughput (max rate at which a router can forward packets)

### Queuing Delay and Packet Loss
* Factors to affect $d_{queue}$ 
  * rate at which traffic arrives at the queue
  * transmission rate of the link
  * traffic arrives periodically / bursts
* $a$ : average rate at which packets arrive at the queue 
* $R$ : transmission rate 
* $L$ : all packets consits of L bits
* **traffic intensity**: $\frac{La}{R}$
  * If $\frac{La}{R} > 1$
    * Queue tends to increase without bound
    * Queuing delay approach infinity 
    * *Design your system so that the traffic intensity is no greater than 1*
  * Otherwise, nature of arriving traffic impacts significantly
    * Periodically: 
      * every packet arrives every $\frac{L}{R}$ seconds,
      * empty queue 
      * no queuing delay
    * In burst but periodically :
      * every N packets arrive simultaneously every (L/R)N seconds
      * Average $d_{queue} = \frac{(N-1)L/R}{2}$ 
      ![](https://images2018.cnblogs.com/blog/1126979/201803/1126979-20180309140232977-1827553384.png)

#### Packet Loss
* The fraction of lost packets increases as the traffic intensity inccreases
* The performance at a node is not only measures in terms of delay, but also in terms of probability of packet loss
* A lost packet may be retransmitted on an end-to-end basis to ensure all data transferred to the destination

### End-to-End Delay
* uncongested network ($d_{queue} \approx 0)
* N - 1 routers
* $d_{proc}$ at each router and at the source
* $d_{prop}$ on each link 
* $d_{trans}$ out of each router and source 
* $d_{end-end} = N * (d_{proc} + d_{trans} + d_{prop})$

#### End System, application, and other delays
Additional significant delays 
* transmit a packet into a shared medium
  puerposefully delay its transmission as part of its protocol for sharing the medium with other end systems
* media packetization delay
  * in VoIP applications (Voice-over-IP)
  * Must fill a packet with encoded digitized speech 
    Time to fill a packet (packetization delay)
* ...
  
### Throughput in Computer Networks
Another critical performance measure
* **instantaneous throughput** at any instant of time is the rate at which Host B is receiving the file
* ** average throughput** F bits file takes T seconds to transfer
  $\frac{F}{T}$
* Some applications are desirable to have a low delay and an instantaneous throughput consistently above some threshold
  (e.g. Internet telephony)
* Others are likely to have the highest possible throughput and not worry about delay (e.g. file transfer)
* **Bottleneck link**
* If no intervening traffic (e.g. Ethernet / p2p) throughput can be approximated as the minimum transmission rate
* More generally, depend not only on the transmission rates of the links, but also on the intervening traffic 

## Protocol Layers and Their Service Models
### Layered Architecture
Each layer provides its service by
1. performing certain actions within that layer
2. using the services of the layer directly below it

* A layered architecture makes it much easier to change the implementation of the service provided by the layer

* As long as the service provided from the layer is unchanged, changing its implemenetation would not affect other layers 
  
#### Protocol Layering
* Each protocol belongs to one of the layers, similiar with each function in the airline architecture
* Services that a layer offers to the layer above, **service model** of a layer
* Services provided by layer n might be implemented by using an unreliable edge-to-edge message delivery service of layer n-1 and adding layer n functionality to detect and retransmit lost messages
* A protocol layer can be implemented in software, hardware, or both
  * Application-layer is implemented in software(HTTP / SMTP..)
  * Transport-layer is the same
  * Physical layer and data link layers are implementd in a *network interface card* (since they are responsible for handling communication over a specific link)
  * Network layer is a mixed of both
* Pros
  * A structured way to discuss system components
  * Modularity makes it easier to update system components 
* Cons
  * One layer may duplicate lower-layer functionality
  * functionality at one layer may need information that is present only in another layer (which violates the goal of separation of layers)
* Internet / TCP/IP protocol stack consists of 5 layers
* OSI consists of 7 layers

#### Application Layer
* HTTP (Web document request and transfer)
* SMTP (transfer for e-mail messages)
* FTP  (files tranfer between end systems)
* DNS is done by the help of application-layer protocol
* information in packets at this layer is called a **message**

#### Transport Layer
Transport messages between endpoints
Two transfer protocols
* TCP 
  * connection-oriented 
  * guaranteed delivery
  * provided flow control
  * congestion-control mechanism 
    (source throttles its transmission rate when the network is congested)
* UDP
  * connectionless service
  * no reliability
  * no control flow
  * no congestion control
* Transport layer packet: **segment**
  
#### Network Layer
responsibles for moving network-layer packets **datagrams**
* TCP / UDP passes last-layer segment / packet + a destination address to this layer
* IP protocol
  * defines the fields in the datagram
  * how the end systems and routers act on these fields
* Routing protocols
  determine the routes that datagrams take 
* Referred as the *IP layer*

#### Link Layer
Move the datagram to the next node along the route
* At this node, network layer passes the datagram down to the link layer and delivers
* At the next node, link layer passes the datagram up to the network layer
* Services provided by this layer depend on the specific protocol (e.g. Ethernet, WiFi, cable access network;s DOCSIS)
* As datagrams need to traverse several links to travel from source to destination, they are handled by different link-layer protocls at different links along its route
* Link-layer packet: **frames**
  
#### Physical Layer
Move the *individual bits* within the frame from one node to the next
* Link independent
* further depend on the actual transmission medium of the link
* There are many physical-layer protocols, but in each case, bits are moved across the link differently

#### OSI Model
TODO