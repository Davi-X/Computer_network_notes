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
