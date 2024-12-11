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


