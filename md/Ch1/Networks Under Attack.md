## Network Under Attack
### Put Malware into Your Host Via the Internet
* **malware**
  * Feature
    * self-replicating
      It seeks entry into other hosts over the Internet from the affected host
  * Form
    * Viruses: require user interaction
    * Worms: without any explicit user interaction
* **botnet**
### Attack Servers and Network Infrastructure
* DoS attacks (denial-of-service)
  * Vulnerability attack
    send a few well-crafted messages to stop service or crash host
  * Bandwidth flooding
    send a deluge of packets to clog access link, reject legitimate users
  * Connection flooding
    establishes a large number of half-open / fully open TCP connections. Host are bogged down with bogus connection
* DDoS (Distributed DoS)
  * Based on Botnets
  * Overall access rate $\approx$ access rate of Target

### Sniff Packets
Placing a passive receiver in the vicinity of the wireless transmitter, that receiver can obtain a copy of every packet that is transmitted

This kind of passive receiver is called **packet sniffer**

Sniffers can also be deployed in wired environments since cable access technologies also broadcast packets

Since sniffers are passive, it is difficult to detect. Instead, we use cryptography

### Masquerade as someone you trust
**IP spoofing**: The ability to inject packeys into the Internet with a false source address 
Solution: *end-point authentication*