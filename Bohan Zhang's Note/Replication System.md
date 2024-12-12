# Consistency
In replication systems, consistency refers to the correctness of the replicas within the system.
## Linearisability
* A linearisable system is a system in which all the operations appear to have been performed in some sequential and non-overlapping order
## Sequential Consistency
* The interleaved sequence of operations meets the specification of a (single) correct copy of the objects
* Absolute time and total ordering of operations is not required. Instead, ordering is relative to the order of events at each separate
client
## Difference
As a result, Linearisation requires that the ordering of events conform to the real-world, while Sequential Consistency requires only that the operations be ordered relative to each process.

# Replicate Patterm
## Passive Replication 
* Primary RM handles all requests and sends updates to the backup RMs.
* The primary and backups are organized as a group, and the primary uses view-synchronization group communication to send updates to the
backups
* When a primary fails, it is replaced by a unique backup.
* The GMS will eventually deliver a new group view to one of the backups. (Using Election Algorithms)
* Linearisability
* To survive up to f process crashes, a passive replication system requires f+1 replica managers.

## Active Replication
* All RMs handle all requests concurrently.
* Front Ends multicast their requests to the group and all the RMs
process the requests independently, but identically, and reply.
* Sequential Consistency
* When a process fails there is no impact on the performance of the
service:
   - The remaining RMs continue to respond in the normal way
   - The FE collects and compares the responses it gets before sending a response to the client

# The Gossip Architecture

## Introduction
- A framework for implementing highly available services
- Data is replicated close to client groups that need it
- Replica Managers exchange periodic "gossip" messages to convey updates

### Basic Operations
1. Query (read-only)
2. Update (modify-only)

### System Guarantees
1. Client Consistency:
   - Clients obtain consistent service over time
   - Queries reflect at least the updates client has observed
   - Works even when communicating with "less advanced" replica managers

2. Relaxed Replica Consistency:
   - All replicas eventually receive all updates
   - Updates are applied with ordering guarantees
   - Supports multiple consistency models (causal, total, immediate)

## Request Processing Flow

### Request Steps:
1. **Request Submission**
   - FE sends request to single replica manager
   - FE can switch RMs if current one fails/overloads
   - Blocking for queries, non-blocking for updates

2. **Update Response**
   - RM replies immediately after receiving update

3. **Coordination**
   - RM waits for ordering constraints before applying

4. **Execution**
   - RM executes the request

5. **Query Response**
   - For queries, RM replies after execution

6. **Agreement**
   - RMs exchange gossip messages containing recent updates
   - Update frequency varies based on configuration

## Frontend (FE) Timestamps

### Vector Timestamp Management
- Each RM maintains last update timestamp
- FE maintains list of latest timestamps for each RM
- Timestamps sent with every request
- FE merges returned timestamps with previous ones

### Client Communication
- Clients can exchange data through:
  - Same gossip service
  - Direct client-to-client communication
- Vector timestamps piggybacked on client messages

## Replica Manager State Components

### Core State Elements
1. **Value**
   - Current application state
   - State machine starting with initial value
   - Updated through operation application

2. **Value Timestamp**
   - Vector timestamp reflecting applied updates
   - One entry per RM

3. **Update Log**
   - Records all received update operations
   - Only stable updates applied to value

4. **Replica Timestamp**
   - Represents accepted updates
   - Tracks updates in manager's log

5. **Executed Operation Table**
   - Stores unique FE update identifiers
   - Prevents duplicate update application

6. **Timestamp Table**
   - Contains vector timestamps from other RMs
   - Used to track update propagation

## Gossip Message System

### Message Structure
- Contains:
  - Log entries
  - Replica timestamp

### Processing
1. Log merging
2. Stable update application
3. Cleanup of processed updates

### Operation Requirements
- Query operations require: `q.prev ≤ valueTS`
- Updates tracked through vector timestamps

## System Benefits
- High availability
- Flexible consistency models
- Scalable update propagation
- Fault tolerance
- Support for dynamic RM selection

This architecture provides a robust foundation for distributed systems requiring reliable data replication and eventual consistency.

# Medianode: A Distributed Multimedia System

## Overview

A distributed multimedia system designed for sharing teaching materials among lecture groups.

### Key Design Goals
- High Availability
  - Connected and Disconnected Modes
  - Geographically distributed replicas
- Consistency management for concurrent updates and failures
- Location and Access Transparency
- Cost-efficient update transport
- Quality of Service (QoS) Support

## Data Structure

### Presentation Data Types
1. Presentation Contents
2. Presentation Description Data (XML)
3. Metadata
   - User information
   - System information
   - Domain information
   - Organization information
4. System resource usage information
5. User session information

## Replica Classification

### 1. Metareplicas
- Purpose: Replicated meta-data objects
- Example: Lists of medianodes containing up-to-date file replicas
- Characteristics: Metadata management

### 2. Softreplicas
- Purpose: Small non-persistent meta-data objects
- Examples:
  - System resource information
  - User session information
- Characteristics: Temporary, lightweight

### 3. Truereplicas
- Purpose: Large persistent objects
- Example: Media content files
- Characteristics: Main content storage

## Replication Mechanism

### File Management
- Replica Managers maintain local file tables
- File tables include replica information
- Replica creation information stored in each file table

### Access Control
- Read access permitted for local replicas
- Local cached replicas valid until invalidation notice
- Update process triggers multicast-based signals

### Update Distribution
- Multicast-based update notification system
- Multicast addresses linked to replica sub-groups
- Sub-group organization examples:
  - File directories
  - Topic-based presentation sets

## System Features

### Availability
- Support for both connected and disconnected operations
- Geographic distribution of replicas
- Robust replica management

### Consistency Management
- Handles concurrent updates
- Failure management protocols
- Maintains data integrity

### Efficiency
- Cost-effective update transport mechanism
- Optimized multicast-based communications
- Efficient resource utilization

This system represents a practical implementation of distributed system concepts, specifically designed for educational content sharing while maintaining high availability and consistency.