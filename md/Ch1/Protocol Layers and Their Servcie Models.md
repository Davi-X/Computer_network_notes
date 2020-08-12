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
* TCP / UDP passes   segment / packet + a destination address to this layer
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
* Services provided by this layer depend on the specific protocol (e.g. Ethernet, WiFi, cable access network's DOCSIS)
* As datagrams need to traverse several links to travel from source to destination, they are handled by different link-layer protocls at different links along its route
* Link-layer packet: **frames**
* data synchronization
* control flow 
* 
#### Physical Layer
Move the *individual bits* within the frame from one node to the next
* Link independent
* further depend on the actual transmission medium of the link
* There are many physical-layer protocols, but in each case, bits are moved across the link differently

#### OSI Model
OSI model: **Open Systems Interconnection** consistes of seven layers
Two additional layers
* Presentation layer: provide services that allow communication applications to interpret the meaning of data exchanged 
  * data compression
  * data encryption
  * data description
    frees the apps from worrying about the internal format(which may differ from computers) in which data are represented/stored 
* Session layer: provide for delimiting and synchronization of data exchange 
  * include means to build a  ckeckpoint + recovery scheme

Q: Why some developers uses 5 layers rather than OSI model?
Q: Are the services of these 2 additional layer not important?
A: It is up to the app developer to decide

### Encapsulation
Link-layer switch has 2 bottom layers
Routers has 3 bottom layers
Hosts implement all 5 layers

* Transport-layer segment = header $H_t$ + application-layer messgae  
* Network-layer datagram = header $H_n$ + transport-layer segment
* ...
* At each layer, contains 2 parts
  * header fields
  * payload field (packet from the above layer)
* In reality, have to consider about reconstruction
