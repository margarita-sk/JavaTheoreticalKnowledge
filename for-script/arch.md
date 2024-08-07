<details>
  <summary>What stands for SOLID?</summary>
mnemonic acronym for five design principles intended to make object-oriented designs more understandable, flexible, and maintainable.

- The [**S**ingle-responsibility principle](https://en.wikipedia.org/wiki/Single-responsibility_principle): Every class should have only one responsibility.
- The [**O**pen–closed principle](https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle): "entities should be open for extension, but closed for modification."
- The [**L**iskov substitution principle](https://en.wikipedia.org/wiki/Liskov_substitution_principle): - An inheriting class should complement, not replace, the behavior of a parent class (if we replace the subclass with the main class it should work)
- The [**I**nterface segregation principle](https://en.wikipedia.org/wiki/Interface_segregation_principle): "Clients should not be forced to depend upon interfaces that they do not use." - lager interfaces should be split into smaller onece
- The [**D**ependency inversion principle](https://en.wikipedia.org/wiki/Dependency_inversion_principle): "Depend upon abstractions, [not] concretions."
</details>


<details>
  <summary>What is DDD?</summary>
Domain-Driven Design (DDD) is a software development approach aimed at managing complex software projects by emphasizing the importance of deeply understanding the domain 
  (the business area or problem space) in which the software will be used. This methodology helps create a shared understanding among all stakeholders, 
  ensuring that the software accurately reflects the real-world processes and needs it is designed to address. The key concepts of DDD include:

Domain-Driven Design is particularly useful for complex domains where a deep understanding of business logic is crucial, and it thrives in environments where continuous collaboration and communication are possible.

Benefits of DDD
- Business Alignment: Ensures the software matches the actual business needs.
- Clear Communication: Promotes better understanding among team members.
- Adaptability: Makes it easier to update the software when business processes change.
  
Challenges of DDD
- Learning Curve: Requires time to understand and implement.
- Complexity: Can add complexity, especially in large projects.
- Initial Effort: Needs significant initial effort to establish a solid domain model and common language.
</details>

<details>
  <summary>What the DDD app consists of?</summary>
  Domain-driven design also defines several high-level concepts that can be used in conjunction with one another to create and modify domain models:

- **Entity**: DO that has an ID and is mutable
- **Value Object**: DO that has no id and is immutable)
- **Aggregate**: A cluster of entities and value objects with defined boundaries around the group.
- **Domain Event**: An object that records a discrete event related to model activity within the system. While *all* events within the system could be tracked, a domain event is only created for event types that the domain experts care about.
- **Domain Services** : Encapsulates *business logic* that doesn't naturally fit within a domain object, and are **NOT** typical CRUD operations – those would belong to a *Repository*.
- **Application Services** : Used by external consumers to talk to your system (think *Web Services*). If consumers need access to CRUD operations, they would be exposed here.
- **Infrastructure Services** : Used to abstract technical concerns (e.g. MSMQ, email provider, etc).
- **Repositories**: Not to be confused with common version control repositories, the DDD meaning of a repository is a service that uses a global interface to provide access to all entities and value objects within a particular aggregate collection. Methods should be defined to allow for the creation, modification, and deletion of objects within the aggregate. However, by using this repository service to make data queries, the goal is to remove such data query capabilities from within the business logic of object models

</details>

<details>
  <summary>What is the difference between domain service and application service?</summary>

  While both Application services and Domain services implement the business rules, there are fundamental logical and formal differences;
- Application Services implement the **use cases** of the application (user interactions in a typical web application), while Domain Services implement the **core, use case-independent domain logic**.
- Application Services get/return Data Transfer Objects, Domain Service methods typically get and return the **domain objects** (entities, value objects).
- Domain services are typically used by the Application Services or other Domain Services, while Application Services are used by the Presentation Layer or Client Applications.
</details>

<details>
  <summary>What is Event Driven Design?</summary>

Event-Driven Design (EDD) is an architectural pattern and methodology used in software development, where the flow of the application is determined 
by events that occur rather than by a sequential flow of control.

Benefits of Event-Driven Design:
- Scalability: Supports scalable and responsive systems by handling events asynchronously.
- Modularity: Promotes modular and loosely coupled architectures, making it easier to add or modify functionalities.
Challenges of Event-Driven Design:
- Complexity: Managing event flows and ensuring proper sequencing of event handlers can be complex.
- Eventual Consistency: Ensuring consistency across distributed systems when events are processed asynchronously.
- Debugging: Debugging and tracing event flows can be challenging compared to traditional sequential programming.
</details>

<details>
  <summary>What are the key aspects of Event-Driven Design?</summary>

- Events: Events are occurrences or happenings within the system or from external sources that are of interest to the application. These can include user actions (like clicking a button), system notifications (like a file being updated), or messages from other services.
- Event Handlers: Event-Driven Design relies on event handlers, which are functions or methods that are executed in response to specific events. When an event occurs, the corresponding event handler is triggered to perform some action or process related to that event.
- Asynchronous Processing: Events are typically processed asynchronously, meaning the application can continue to handle other tasks while waiting for events to occur. This asynchronous nature can improve responsiveness and scalability.
- Loose Coupling: Event-Driven Design promotes loose coupling between components. Components or services that generate events do not need to know anything about the components that handle those events, promoting modularity and flexibility in the system architecture.
- Publish-Subscribe Model: Often, Event-Driven Design utilizes a publish-subscribe (pub-sub) model, where components (publishers) emit events without knowledge of which components (subscribers) will handle them. Subscribers can register interest in specific types of events and receive notifications when those events occur.
</details>

<details>
  <summary>Logs vs Metrics vs Traces?</summary>

**Logs**
Files that record events, warnings, and errors when they occur within a software environment
Limitations: 
- record only that was configured to record
- logs created by containerized applications will disappear permanently when the container shuts down (if they weren’t written somewhere)

**Metrics**
Quantifiable measurements that reflect the health and performance of the application or infrastructure (Transaction per second, CPU consumed, latency and etc.) 
Limitations: 
- record only that was configured to record
- are not detailed - the performance is low, but what is the cause?

**Distributed traces**
Data that tracks an application request as it flows through different parts of the application, where exactly the error occurs.
Limitations: 
- only a part of all application requests is traced in most cases
- takes too much time and consumes too many resources
</details>


<details>
  <summary>What is Distributed System?</summary>
Computer systems whose inter-communicating components are located on different networked computers.
  
Key features:
- Horizontal Scalability: Adding more machines to handle increased load.
- Vertical Scalability: Adding more resources (CPU, memory) to existing machines.
- Fault Tolerance: Systems are designed to continue functioning even in the presence of failures. Achieved through redundancy, replication, and failover mechanisms.
- Consistency: Ensuring all nodes see the same data at the same time.
- Availability: Systems are designed to be operational 24/7.
- Partition Tolerance: The system continues to operate despite network partitions.
</details>

<details>
  <summary>Distributed System Common Architectures</summary>

- Client-Server: Clients request services, and servers provide them. Examples: Web applications with web servers and database servers.
- Peer-to-Peer (P2P): Each node (peer) acts as both a client and a server. Examples: File-sharing systems like BitTorrent.
- Microservices: The application is decomposed into smaller, loosely coupled services.
</details>


<details>
  <summary>Name consistency models of distributed system architecture</summary>

- Strong Consistency: Guarantees immediate consistency across all nodes after an update.
- Eventual Consistency: Ensures that, given enough time, all nodes will become consistent.
- Causal Consistency: Ensures that causally related operations are seen by all nodes in the same order.
</details>


<details>
  <summary>Name eventually consistency patterns</summary>

- Event Sourcing: Storing all changes (events) to the state as a sequence of events
- CQRS (Command Query Responsibility Segregation): Separates the read and write models for optimization
- Saga Pattern: 
</details>

<details>
  <summary>What is CAP theorem?</summary>

The CAP theorem, also known as Brewer's theorem, is a fundamental principle in distributed systems that states it is impossible for a distributed data store to simultaneously provide more than two out of the following three guarantees:
- Consistency (C): Every read receives the most recent write or an error. Ensures that all nodes in a distributed system see the same data at the same time.
- Availability (A): Every request (read or write) receives a response, without guarantee that it contains the most recent write. Ensures that the system is always operational and responsive.
- Partition Tolerance (P): The system continues to operate despite arbitrary message loss or failure of part of the system. Ensures that the system can handle network partitions where some nodes cannot communicate with others.

According to the CAP theorem, in the presence of a network partition, a distributed system has to choose between:
- Consistency and Availability
- Availability and Partition Tolerance
- Consistency and Partition Tolerance
</details>
