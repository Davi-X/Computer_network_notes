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