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
