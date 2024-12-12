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
Ensure that any node can access any resource by routing each request through a sequence of nodes.
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
### Scalability
* IP Routing: 2*32 addressable nodes; hierarchical nature
* Routing Overlays: 2*128; flat structure
### Load Balancing
* IP Routing: Loads on routers are determined by network topology and associated traffic patterns.
* Routing Overlays: Object locations can be randomized and hence traffic patterns are not determined by the network topology.
### Network Dynamics
* IP Routing: IP routing tables are updated asynchronously on a best-efforts basis with time constants of the order of one hour.
* Routing Overlays: Routing tables can be updated synchronously or asynchronously with fractions of a second delays.
### Fault Tolerance 
* IP Routing: Redundancy is designed into an IP network by its managers, ensuring tolerance of a single router or network connectivity failure
* Routing Overlays: Routes and object references can be replicated n-fold, ensuring tolerance of n failures of nodes or connections.
### Target Identification
* IP Routing: Each IP address maps to exactly one target node.
* Routing Overlays: Messages can be routed to the nearest replica of a target node.
### Security and Anonymity
* IP Routing: Addressing is only secure when all nodes are trusted
* Routing Overlays: Security can be achieved even in environments with limited trust.

# Pastry
## Advantage 
* Supports Replication
* Fault-resistant
* Scales well
## Key mechanisms
### Node IDs and State:
* Each node has a unique 128-bit identifier (NodeID)
* Leaf set: Numerically closest NodeIDs
* Routing table: Enables logarithmic routing
* Neighborhood set: Physically closest nodes
### Routing Process:
* Messages are assigned destination keys in same ID space as NodeIDs
* At each hop, message is forwarded to node whose ID is numerically closer to destination
* Node chooses next hop from its routing table that shares longest common prefix with destination
* If no such entry exists, message is forwarded to leaf set node closest to destination
### Performance
* Routes messages in O(log N) hops on average, where N is number of nodes
* Each node maintains O(log N) routing state
* Self-organizing and self-repairing when nodes join/leave
* Accounts for network locality to reduce latency

# BT
再说