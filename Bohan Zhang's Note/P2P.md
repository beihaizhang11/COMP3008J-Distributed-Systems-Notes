# P2P
## 推荐阅读
* https://luyuhuang.tech/2020/03/06/dht-and-p2p.html
## Definition
* A set of networked devices that have equal responsibility and which share resources and workload as necessary.
* Each device is both a client and a server.
* There is no (or little) centralized control.
## Examples
* File Sharing Applications e.g. Gnutella, BitTorrent, Kazaa
* Instant Messengers and Telephony e.g. Skype, Yahoo, MSN
## Advantage
* Peer-to-Peer Systems **most effective** when used to store very large collections of immutable data
* Their design **diminishes their effectiveness** for applications that store and update mutable data
## Aim 
To deliver a service that is fully decentralised and self-organising, dynamically balancing the storage and processing loads between all the participating computers as computers join and leave the service
## Problem 
How to deal with the placement and accessing of shared resources in a manner that balances the workload and ensures availability, but does not add undue overheads?
## Types
* Centralized systems: peer connects to server which coordinates
* Decentralized systems: peers run independently with no central services.
* Hybrid systems: peers connect to a server to discover other peer

# Middleware Systems
* Aim: To be application independent; To share resources, storage and data present in computers at the edges of the internet on a global scale.
## Routing Overlays
### Aim
Clients wishing to invoke an operation on a resource submit a request, which includes a GUID (unique identifier) for the resource, to the routing overlay algorithm. It directs the request to a node on which a replica (or the original) of the resource resides.
### Be Responsible for
* Creating GUID’s for all new resources
* Announcing the existence of the new resources to ensure that the resource is reachable by all clients.
* Handling the removal of references to shared resources that are no longer in the system
* managing the addition/removal of nodes to/from the system.
### DHT
* Decentralization: the nodes collectively form the system without any central coordination.
* Scalability: the system should function efficiently even with thousands or millions of nodes.
* Fault tolerance: the system should remain reliable even with nodes continuously joining, leaving, and failing. Mainly through the replication of objects

## Routing Overlays vs IP Routing


