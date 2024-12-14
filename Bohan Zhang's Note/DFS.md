Here's a Markdown summary of the distributed file systems content:

# Distributed File Systems

## Introduction & Overview
---
- Key goal: Sharing resources, particularly stored information
- Implementation approaches:
  - Databases
  - Distributed Shared Memory
  - Remote Objects
- Underlying requirement: Persistent data storage through file systems

### General File System Responsibilities
- Organization
- Storage
- Retrieval
- Naming
- Sharing
- Protection of files

### Core Components
1. File Servers:
   - Hardware (secondary storage)
   - Software (handles service requests)
2. Clients:
   - Transmits file service requests
   - Provides user interface
3. File Services:
   - Specifies primitive file operations

## File Access Models
---
### Upload/Download Model
- Operations:
  - Read: Transfers entire file from server to client
  - Write: Transfers entire file back to server
- Advantages:
  - Simple file service interface
- Disadvantages:
  - Requires sufficient client storage
  - Inefficient for large files

### Remote Access Model
- Operations executed directly on servers
- Advantages:
  - Minimal client space requirements
  - Efficient for partial file access
- Disadvantages:
  - Repeated access overhead (mitigated by caching)

## Caching
---
### Cache Location Options
1. Disk Caches
   - More reliable
   - Cached data persists during recovery
2. Main-memory Caches:
   - Enables diskless workstations
   - Faster data access
   - Better performance with larger memories

### Cache Update Policies
1. Write-through:
   - Immediate disk writes
   - Reliable but poor performance
2. Delayed-write:
   - Modifications written to cache first
   - Better performance but lower reliability

### Cache Consistency
- Challenge: Maintaining consistency between cached copy and master copy
- Approaches:
  1. Client-initiated:
     - Client checks validity
     - Server verifies consistency
  2. Server-initiated:
     - Server tracks client caches
     - Server manages potential inconsistencies

### Benefits of Caching
- Efficient handling of remote accesses
- Better performance for infrequent writes
- Lower network overhead
- Optimized disk access routines

## Naming and Transparency
---
### Naming Schemes
- Uses textual labels mapped to physical storage
- Typically employs directory-based hierarchical structure
- Example: `/etc/passwd`

### Types of Transparency
1. Location transparency:
   - File name doesn't reveal physical storage location
2. Location independence:
   - File name remains unchanged when physical location changes
3. Access transparency:
   - Common operations for both local and remote files

### Global Naming
- Challenge: Providing global context for file names
- Solution: Total integration of component file systems
- Implementation example: X.500 Naming Scheme and Andrew File System (AFS)
## Abstract DFS Architecture
---
- Common framework underpinning both Network File System (NFS) and Andrew File System (AFS)
- Designed as a stateless implementation
- Three core components:
  - Flat File Service 
  - Directory Service
  - Client Module

## Stateful vs Stateless File Services
---
### Stateful Service
- Server keeps copy of requested file in memory until client finishes
- Advantages:
  - Increased performance
  - Fewer disk accesses
  - Can read ahead blocks for sequential access
- Example: Andrew File System (AFS)

### Stateless Service
- Treats each request as self-contained
- Each request must identify file name and data position
- No need for open/close operations
- Example: Network File System (NFS)

### Key Differences
- Failure Recovery:
  - Stateful servers lose volatile state in crashes
  - Stateless servers can handle failures more easily
- Penalties for stateless:
  - Longer request messages
  - Slower request processing

## File Replication
---
### Purpose
- Multiple physical copies of single logical file
- Benefits:
  - Performance Enhancement: Spread requests across servers
  - Increased Availability: File accessible despite failures

### Challenges
- Update Problem: Updates must be reflected across all replicas
- Demand Replication: Reading non-local replica creates new copy
- Concurrency Problem: Handling concurrent updates

## Security
---
- Controls data access and authenticates client requests
- Two main approaches:
  1. Name Resolution Security Check
     - Check performed when name resolved to UFID
     - Capability returned with security check results
  2. RPC Check
     - User identity submitted with every RPC
     - Encrypted digital signature
     - Server checks every operation

## NFS (Network File System)
---
### Architecture
- Client-server model
- Each workstation can be both client and server
- Key Protocols:
  - Mount Protocol
  - NFS Protocol
- Uses stateless operations

### Key Features
- Virtual File System (VFS)
  - Supports access transparency
  - Separates generic operations from implementation
- File Handles contain:
  - File System Identifier
  - inode number
  - inode generation number
- Client and Server Caching
  - Write-through or Write-on-commit strategies
  - Timestamp-based consistency checks

### Security
- Stateless - each RPC includes authentication
- Uses user ID and group ID
- Supports encryption