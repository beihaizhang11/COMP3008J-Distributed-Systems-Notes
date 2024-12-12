# Clocks知识结构
```shell

# 时钟类型概述
|-- 物理时钟
`-- 逻辑时钟
    |-- Lamport逻辑时钟
    `-- 向量时钟


# 物理时钟同步方法
|-- 集中式
|   |-- Cristian算法
|   `-- Berkeley算法
|
`-- 分布式
    |-- 平均算法
    `-- NTP

# 问题与解决方案流程
1. 基本时间问题
   |-- 地球自转不均匀性
   `-- 解决方案：原子时(铯133)

2. 分布式时间挑战
   |-- 计算机之间的时钟偏差
   `-- 解决方案：
       |-- 物理同步(UTC广播)
       `-- 逻辑同步(Lamport方法)

3. 事件排序挑战
   |-- 物理时间限制
   `-- 解决方案：
       |-- Lamport逻辑时钟("happened-before"关系)
       `-- 向量时钟(因果关系检测)
```
# Physical Clocks
## Clock Synchronization Algorithms
### Centralized Algorithms
* A **single** component of the system is responsible for delivering a common global system time.
* **Examples**: Cristian’s Algorithm; Berkeley Algorithm
### Decentralized Algorithms
* Multiple components of the system are responsible for delivering a common global system time.
* **Examples**: Averaging Algorithms; Multiple External Time Sources
### Chistian's Algorithms
![Chistian's Algorithms](Images/Cristians_algorithm_illustration.png)
* The process on the client machine sends the request for fetching clock time(time at the server) to the Clock Server at time T_0.
* The Clock Server listens to the request made by the client process and returns the response in form of clock server time.
* The client process fetches the response from the Clock Server at time T_1 and calculates the synchronized client clock time using the formula: ![Chistian's Algorithms Latex](Images/quicklatex.com-787d0e5f924d43a3aea97d3c61c8163b_l3.svg)
### Berkeley Algorithm
*  An individual node is chosen as the master node from a pool node in the network. This node is the main node in the network which acts as a master and the rest of the nodes act as slaves. The master node is chosen using an election process/leader election algorithm.
*  Master node periodically pings slaves nodes and fetches clock time at them using Cristian’s algorithm.
*  Master node calculates the average time difference between all the clock times received and the clock time given by the master’s system clock itself. This average time difference is added to the current time at the master’s system clock and broadcasted over the network.
### Averaging Algorithms
* Every R seconds, each machine broadcasts its current time
* The local machine collects all other broadcast time samples during some time interval, S.
* The simple algorithm: the new local time is set as the average of the value received from all other machines.
* A slightly more sophisticated algorithm: Discard the m highest and m lowest to reduce the effect of a set of faulty clocks.
### Network Time Protocol (NTP)
* Uses a network of time servers to synchronize all processors on a net.
* Time servers are connected by a synchronization subnet tree.

# Logical Clocks
## Lamport s Logical Clocks
### two observations
* if two processes do not interact, then their clocks do not need to be synchronized
* it does not matter that two processes share a common notion of what the “real” current time is. What does matter is that the processes have some agreement on the order in which certain events occur.
## Vector Clock
A vector clock is an algorithm for generating a partial ordering of events in a distributed system and detecting causality violations.

# Global State
## Cut
?
## Snapshot algorithm
A snapshot algorithm is used to create a consistent snapshot of the global state of a distributed system. Due to the lack of globally shared memory and a global clock, this isn't trivially possible.
* Marker sending rule for a process P :
* * Process p records its own local state
* * For each outgoing channel C from process P, P sends marker along C before sending any other messages along C. (Note: Process Q will receive this marker on his incoming channel C1.)
* Marker receiving rule for a process Q :
* * If process Q has not yet recorded its own local state then
* * * Record the state of incoming channel C1 as an empty sequence or null.
* * * After recording the state of incoming channel C1, process Q Follows the marker sending rule
* * If process Q has already recorded its state
* * * Record the state of incoming channel C1 as the sequence of messages received along channel C1 after the state of Q was recorded and before Q received the marker along C1 from process P.
### **Benefits** 
* Checkpointing: It helps in creating checkpoint. If somehow application fails, this checkpoint can be reused
* Garbage collection: It can be used to remove objects that do not have any references.
* It can be used in deadlock and termination detection.
* It is also helpful in other debugging.

# Mutual Exclusion

## Centralized
a single coordinator controls whether a process can enter a critical region.
### Advantage
* Fair; No process starvation; Easy to implement.
### Disadvantage
* There’s a single point of failure!
* The coordinator is a bottleneck on busy systems.

## Distributed
the group confers to determine whether or not it is safe for a process to enter a critical region.
### Advantage
* There is no single point of failure
### Disadvantage
* Multiple points of failure!
* A “crash” is interpreted as a denial of entry to a critical region.
* one overworked process in the system can become a bottleneck to the entire system so, everyone slows down.
## Token Ring
processes are organised into a logical loop and use a token to determine when to enter a critical region.
### Advantage
* fair
### Disadvantage
* Lost token
* Process failure can cause problems
* Every process is required to maintain the current logical ring in memory

## Comparision
* The “Centralized” algorithm is simple and efficient, but suffers from a single point of failure.
* The “Distributed” algorithm has nothing going for it. It is slow, complicated, inefficient of network bandwidth, and not
very robust.
* The “Token Ring” algorithm suffers from the fact that it can sometimes take a long time to reenter a critical region having
just exited it.
* All perform poorly when a process crashes.
