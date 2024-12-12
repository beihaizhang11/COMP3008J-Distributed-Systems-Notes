# P2P知识结构
```shell
P2P知识结构
├── 核心概念
│   ├── 分布式系统架构
│   └── 基本特征
│       ├── 节点平等
│       ├── 双重角色(客户端/服务器)
│       └── 去中心化
│           └──> 目标：分布式自组织服务，动态平衡负载
│
├── 系统分类 (根据中心化程度)
│   ├── 中心化(SETI@home) <──> 混合型(Napster) <──> 去中心化(Gnutella)
│   └── 权衡: 纯P2P(难实现) <──> 部分中心化(更高效)
│
├── 技术实现
│   ├── 中间件系统
│   │   └──> 资源共享层
│   │       └──> 核心问题：资源定位
│   │           └──> 解决方案：路由覆盖网络
│   │
│   └── DHT实现
│       ├── 资源标识(GUID)
│       ├── 基本操作(put/get/remove)
│       └── 特性
│           ├── 去中心化
│           ├── 可扩展性
│           └── 容错性
│
├── 应用场景
│   ├── 文件共享(BitTorrent)
│   ├── 即时通讯(Skype)
│   └── 分布式计算(SETI@home)
│
└── 核心问题
    └── 资源定位 ──> 负载均衡 ──> 可用性 ──> 扩展性
```
# P2P
## 推荐阅读
* https://luyuhuang.tech/2020/03/06/dht-and-p2p.html
## Definition
* A set of networked devices that have equal responsibility and which share resources and workload as necessary.
* Each device is both a client and a server.
* There is no (or little) centralized control.
* Every user contributes resources to the service.
* All nodes have the same functional capabilities and responsibilities despite resource differences.
* Operation doesn't depend on centrally-administered systems.
* Can offer limited anonymity to providers and users of resources.
## Examples
* File Sharing Applications e.g. Gnutella, BitTorrent, Kazaa
* Instant Messengers and Telephony e.g. Skype, Yahoo, MSN
* Data Processing Services e.g. Seti@Home
## Advantage
* Peer-to-Peer Systems **most effective** when used to store very large collections of immutable data
* Their design **diminishes their effectiveness** for applications that store and update mutable data
## Aim 
To deliver a service that is fully decentralised and self-organising, dynamically balancing the storage and processing loads between all the participating computers as computers join and leave the service
## Problem 
How to deal with the placement and accessing of shared resources in a manner that balances the workload and ensures availability, but does not add undue overheads?
## Types
* Centralized systems: 
  - Peer connects to server which coordinates and manages communication
  - Centralized discovery and communication
  - e.g. SETI@home
* Decentralized systems: 
  - Peers run independently with no central services
  - Decentralized discovery and communication
  - e.g. Gnutella, Pastry
* Hybrid systems: 
  - Peers connect to a server to discover other peers
  - Centralized discovery but decentralized communication 
  - e.g. Napster

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

## DHT (Distributed Hash Tables)
### Properties
* Decentralization: nodes collectively form the system without central coordination
* Scalability: efficiently functions with thousands/millions of nodes
* Fault tolerance: reliable despite nodes joining/leaving/failing 

### Operations
* put(GUID, data): stores data replicas at nodes responsible for GUID
* remove(GUID): deletes all references and associated data
* get(GUID): retrieves data from one responsible node

### Usage
* Used in systems like BitTorrent
* Provides lookup service similar to hash table
* (key, value) pairs stored distributed across nodes
* Any node can efficiently retrieve values

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