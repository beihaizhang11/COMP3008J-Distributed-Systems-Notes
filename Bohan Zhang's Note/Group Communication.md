# Group Communication知识结构
## 多播类型：
基本多播 -> 可靠多播 -> 群组成员服务 -> 视图同步群组通信
# Group Communication
## Basic Conception
### Definition
A mechanism for sending a single message to a group of processes (almost) simultaneously
### Advantage
* Efficiency: can minimize use of bandwidth by sending one message to n processes instead of n messages to n processes.
* Delivery Guarantees: If a Unicast based approach is used, then failure can lead to only some of the processes receiving the messages & the relative ordering of messages is undefined.
## Types
* Unreliable multicast: No guarantee of delivery or ordering: message only transmitted once
* Reliable multicast: Best effort is made to deliver to all members of the receiving group.
* Atomic multicast: Message is either received by all processes in the receiving group or none of them.
## Basic Multicast
* A primitive multicast protocol that guarantees the delivery of messages to all processes in a (static) group
* Implementation builds on an assumed unicast protocol that guarantees message delivery (e.g. TCP)
* This approach suffers from “ACK-implosion”
## Reliable Multicast
### Reliable Multicast is an extension of the Basic Multicast service:
* Guaranteed Delivery (Basic Multicast)
* Integrity (完整性)
* Validity (有效性)
* Agreement (一致性)
### Implementataion
* IP Multicast: Assumption that IP multicast communication is often successful
* Piggy-backed acknowledgements (ACKs): sent as part of multicast messages
* Negative acknowledgements (NAKs): sent when a process detects that it has missed a message.

## Group Membership Service (GMS)
### Definition
A Group Membership Service (GMS) is a service that provides support for the (dynamic) management of both group membership and multicast communication.
### Main Objectives
* Providing an interface for group membership change.
* Implementing a failure detector.
* Notifying members of changes in membership.
* Performing group address expansion.

## View-Synchronous Group Communication
### Group View
* A group view is an ordered list of the current group members, identified by their unique process identifiers.
* Views are **delivered** whenever a membership change occurs.
* View delivery involves notifying the application of the new membership.
* View Delivery: Order; Integrity; Non-triviality
### Main Objectives
* Agreement: Correct processes deliver the same sequence of views, and the same set of messages in any given view.
* Integrity: If a correct process p delivers message m, then it will not deliver m again.
* Validity: Correct processes always deliver the messages that they send.