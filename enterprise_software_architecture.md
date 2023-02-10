# Enterprise Software Architecture Overview

## Kruchten's 4+1 Model
* Development View - describes the programmer's perspective of the system and is focused on software management and domain UML diagrams. Component diagram and package diagram are often used to visualize relationship between system components and packages respectively
* Logical View - concerned with system behavior and the functionality provided to end users
* Physical View - describes the perspective of a system and network engineer and this concerns the distribution and topology of software effects on a physical layer and how they are interconnected
* Process View - concerned with system processes, control flow concurrency and data flow
* Scenarios - uses a set of scenarios or use cases to start off system testing, verify the design of the system actually makes sense and will satisfy stakeholder requirements

## Software Architecture Pattern

### Multi-Tiered Architecture (Layered Architecture)
* Each layer performs a specific role and has its own responsibility
* Most common adaptation is 3-tiered architecture system, consisting of *presentation layer*, *business layer* and *data access layer*.
* The more complex the system is, the more tiers in a tiered architecture system
* Advantages:
  * allow for clear separation of concerns between components, easier to define roles
  * easier to develop and test components
  * suitable for anykind of application
* Drawbacks:
  * lead to monolithic application
  * high coupling between layers
  * low scalability and potentially performance issues as system grows

### Client-Server Architecture
* Distributed application structure
* Server provides a service which client requests
* Promotes centralized computing where lots of resources are dedicated to a small number of computers
* Lite clients don't have much processing power, these clients send requests to server, and server will definitely need much more resources to handle large number of clients
* Advantages:
  * centralization promotes security check at server side
  * backup procedure is simplified
  * easier management, upgrading and scaling
* Drawbacks:
  * introduce single point of failure, to be mitigated via high availability resources and redundancy
  * prone to network congestion
  * cost becomes an issue as higher power servers are needed as service grows
  
### Model-View-Controller (MVC) Architecture
* Advantages:
  * low coupling between each part
  * promoting high cohesion
  * promotes parallel development
  * promotes code reuse
* Drawbacks:
  * steep learning curve, challenging for inexperienced developers
  * not suitable for large, complex applications (UI-related pattern)

### Service Oriented Architecture
* Based on loosely copied services together make up the system
* Can be implemented in different technologies (web services)
* A service is defined as a logical representation of a business activity with a specified outcome, self-contained and is a black box for customers
* Advantages:
  * promotes low coupling especially between services since the service should be a black box and self-contained
  * promotes reusability not only at the code level but also of entire services
  * easier to maintain and test since each service is an independent entity
  * one can scale up the service that is currently a bottleneck in the system
  * promotes parallel development
* Drawbacks:
  * can become complex as each service will require its own monitoring and deployment process will become more complex as new services are added
  * increased complexity and cost compared to monolithic software
  * increased overheads in the system
  * not very suitable for GUI based app since these would require large amounts of data transfer between services or apps which are standalone and short lived.

### Microservices Architecture
* Main difference between microservices and service oriented is that in microservice architecutre the services are more fine grained, have a clearly defined scope tied to a business or deck function and they are lightweight.
* Advantages:
  * improves modularity, making the system easier to build, test and maintain
* Drawbacks:
  * infrastructure costs are usually higher due to number of services and inter-process communication
  * overhead integration testing becomes more complex due to large number of microservices that need to be tested together
  * service management and deployment become more tedious

### Domain Driven Architecture
* In domain driven design sofware experts work with domain experts to build a ubiquitous language which describes the system
* The ubiquitous language will help form the structure of the object oriented design of the software and guides you in diving the objects into value objects, entities and aggregates roots.
* Advantages:
  * helps avoiding communication issues between dev team and biz tea.
  * make the system more maintainable
* Drawbacks:
  * requires very good knowledge of the domain driven process to implement correctly
  * initial investment is also costly, need a domain expert to work hand-in-hand with the development team.
  * not suitable for systems that do not have a complex domain model or which are not going to be used for a long time.

### Event Driven Architecture
* Promotes the production, direction, consumption and reaction to events
* An event can be defined as a change in the system's state.
* Producers generate events while event consumers listen for events and consume them
* Producers are decoupled from the consumers, so producers are not aware of the consumers.
* Consumers are decoupled from each other, meaning consumers are not aware of other consumers consuming the same event
* Implemented in one of two different ways:
  * Publish subscribe model where the messaging infrastructure keeps track of consumers that have subscribed to particular events and once an event has been generated it is forwarded to each of its subscribers
  * Event stream model where events are written to a log so clients don't subscribe to events. They are responsible for reading events from the log file
* Advantages:
  * decoupling between consumers and producers and between consumers themselves
  * eaiser to add/remove consumers
  * allows for scalability and distribution
* Drawbacks:
  * not suitable when the guarantees of the event ordering between consumers
  * difficult to manage when changes to producers are required affecting all consumers of the particular events.