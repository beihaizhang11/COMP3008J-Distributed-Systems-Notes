# Grid Computing Notes

## 1. What is the "Grid"?

### Basic Concept
- Based in the idea of computing resources being consumed like electricity is from the power grid
- Resources supported by heterogeneous computer hardware, operating systems, programming languages and applications
- Management required to co-ordinate the use of resources

### Key Features
- Middleware designed to enable the sharing of resources on a very large scale:
  - files
  - computers
  - software
  - data
  - sensors
- Typically shared by groups of users in different organisations who are collaborating to solve a problem:
  - via sharing of data
  - via sharing of computing power
- Distributed system that is loosely coupled, heterogeneous, and geographically dispersed

---

## 2. Example: World Wide Telescope

### Project Overview
- Project owned by Microsoft Research to deploy data resources that are shared by the astronomy community
- Archives of observations covering:
  - particular time period
  - part of the electromagnetic spectrum
  - part of the sky
- Made by different instruments distributed worldwide

### Data Characteristics
- Each team's data is gathered locally (order of terabytes and growing exponentially)
- Data is analysed and stored as derived data for use by others
- Requires common data labelling/format
- Metadata to describe:
  - when it was collected
  - where it was collected
  - the instrument used
- Derived data specifies parameters used when filtering from the raw data

### Project Goals
- Unify the world's astronomy archives into a giant database containing:
  - astronomy literature
  - images
  - raw data
  - derived datasets
  - simulation data
  
---

## 3. Requirements of a Grid

1. Remote Access to Resources
2. Processing where it is stored and managed
3. Dynamic Service Creation
4. Metadata to describe:
   - characteristics of the data in the archive
   - characteristics of the service
5. Directory Services: to find services based on metadata
6. Management Software:
   - manage queries
   - data transfers
   - reservation of resources
   - resource rationing

---

## 4. Open Grid Services Architecture (OGSA)

### Overview
- Standard for grid-based applications
- Framework within which the requirements may be met
- Based primarily on web services
- Resources managed by application-specific grid services

### Application-level grid services
1. Web services implementing standard grid-service interfaces:
   - interface to service data (metadata)
   - context for service instance management
2. Standard grid services (two layers):
   - OGSA Layer
   - OGSI Layer

### OGSI Layer Details
- Service instances created dynamically
- Two-level naming scheme:
  - Grid Service Handle (GSH)
  - Grid Service Reference (GSR)
- Service Data requirements
- Fault Model:
  - Common approach for reporting faults
  - XML scheme with timestamp and originating service

### OGSA Services
- Built on OGSI services
- Management Services include:
  - task submission
  - Quality of Service agreement
  - advance reservation
  - Service Level Agreements (SLAs)

## 5. Globus Toolkit

### History and Development
- Began in 1994
- First version appeared in 1997
- OGSA came from second version
- Major version is version 5 (2010)
- Latest release October 2014 (version 6.0)
- Maintained by Globus Alliance as open source project

### Core Components
Four key services:
- Execution Management
- Data Management
- Security
- Common Runtime

### Status
- The defacto standard for grid computing
- Founded on the Web Services Core
- Most current work on grid computing assumes the use of the Globus Toolkit