# Item Management System (TGS_IMS)

## Introduction

This system is built for the Management of Industry resource (Machine, Tools, Materials & more), by implementing a robust relations model and secured industrial architecture.
The core of the system is designed to take in a highly customizable model, although for the current requirements a finished system will be templated to easily manage 4Ms ( Man, Machine, Material & Method) of an Ideal Manufacturing Plant.

## Architecture Overview

This design will focus on high operational flexibility, Industrial Grade Security, Scalability & Hardware failure resistance.

In technical terms, we need to ensure:-
- Horizontal scalability in Storage & Compute
- Appropriate ACID-compliant operations on the Database
- Secured authorization and access to the services
- Absolute Information Isolation between unrelated parties, right from the level of DB Model to Application Model
- Restfulness on every user action and prevent any system-level Bottlenecks.

### User Authorization
TGS_IMS is meant to comply with other TGS services, and allow users to access the service per TGS_UMS. For any TGS_UMS user to access TGS_IMS, has to register to TGS_IMS through explicit means, as IMS requires identification of the user in its database to execute Appropriate ACID-compliant operations.
 
### Data Base
The proposed model of TGS_IMS requires a storage framework that supports a relational model with sufficient atomicity and consistency, which means the model is meant for both NoSQL Graph DB or RDBMS (with some minor relational fixture in Data structure).

*Arguably a NoSQL DB has limited atomicity and consistency to improve the availability of the DB, however, in our Architecture, we can proceed with Neo4J, as Neo4J has a very effective locking mechanism on the Nodes which are meant to undergo update operation in Cypher Query, which makes Neo4J ACID compliant.*
 
### Restful Backend Drivers
These are the well-tested source code designed to perform various operations with or without the data. The source code must be modular & tested to ensure that it does exactly what it is meant to do.
The driver modules are meant to be integrated with Backend servers, but must not be intrinsic with the server's source code.
 
### Restful Server
These servers may implement tested Backend Drivers for all their operations. however, parsing validation of user input must be performed by the servers. These servers must be replicable for vertical scalability.
 
### Front End Drivers
These drives are essential & well-tested JS libraries with can be crucial to operation in the frontend and reliable interaction with the backend.

____

## User Authorization
<need more planning>

## Data Base

## Backend Drivers

