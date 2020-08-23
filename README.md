# Accelerated Implementation of Domain Driven Design

> "DDD is not about structuring data in a normalized fashion. 
> It is about modelling the Ubiquitous Language in a consistent Bounded Context" 
>
> ~Vaughn Vernon, IDDD

## Value Objects

- Have no identity
- Immutable
  - Once created, a value object can never be changed. Attempt at changing the values should result in creation of new value object.
  - Have readonly variables
- Combinable
- They are an Entity's State, describing something about the entity or the thing that it owns
- Premitive types must be wrapped up into cohesie value objects that explicitly represent the concept they are modelling
- Cohesively groups the behaviours of a concept
- Can contain methods that implement the behaviour
- Side Effect free 
- Testable
- They tell us something about another object
- Value Obkects need a context of an entity to be relevant
- Comparable: Considered equal if they have the same value
- Behaviour Rich: 
  - Should expose expressive donain-oriented behavior, through methods
  - Encapsulate state 
  - All primitive types in it should be private or protected
- Cohesive: A value object should contain related concepts
- Self Validating
  - Should never be in an invalid state
  - They should validate themselves
  - Constructor chould check if the values are valid and throw an exception in case they are not.
- Patterns
  - Static Factory Methods
  - Micro Types
  - Collection Aversion
- Persistance
  - NoSql -- Better Suited because the structure of the record matches with the structure of the Aggregate
  - SQL
    - Flat DeNormalization
    - Normalizing into Separate Tables





## Entities

## Aggregates

## Factories

- It is recommended that you separate use from construction and explicitly encapsulate cretion logic within a factory object if it is complex or expressed better.
- Object creation is not a domain concern, but it does live within the domain layer of an application.
- You can use factories to reconstitue a domain objet from a persistance model, or you can use them to create new domain objects, encapsulating complex creation logic.
- It hides the complexities of creating objects.
- Factories an exist on an Aggregate.
- Factror method can create Aggregate Itself from another Aggregate.
- Factories can de-clutter your domain to ensure that it remains expressive.
- Use a factory where elements needed for construction logic are not the concern of the dependent class.

## Domain Events

- In response to events, event handlers are executed.
- When creaing event handlers that trigger asynchronous flow, you need to be clear about transactional boundaries. For example, if one event handler updates the database, and another publishes a message, you would want both operations to rollback if either of them failed.

-Internal vs External Events

  - Internal events are internal to a domain model and they are not sgared between bounded contexts.
  - They are limited in scope to a single bounded context.
  - It is ok to put domain objects on them. This poses no rosk , because other boubded context cannot become coupled to these domain objects.
  - External events tend to be flat in structure, exposing just a few properties, most of the time corellation IDs.
  - External events need to be versioned to avoid breaking changes.
  - If you change the internal events, your code wil not compile and you need to adjust othe code around it.
  
- Domain Event Handlers
  - They invoke domain logic, such as domain service.
  - Application service event handlers are more infractural in nature, carrying out tasks like sending e-mails and publishing events to other bounded contexts.
  - Event handlers delegete to domain service.
  - Event handlers in the application layer trigger communication with external bounded context. They also manage communication with external services like payment gateways.
- Domain Events can be implemented
  - Using events.
  - In-Memory Bus, like NService Bus
  - Udi Dahan's Static DomainEvents Class
    - Handling threading issues. Use [ThreadStatic] on the collection handler. Using this attribute, each thread gets its own collection, meaning the handlers registered on thread are not visible to another thread. thread static should never be used in an ASP.Net Application. [Not Useful]
  - Injecting the event dispatcher in the domain event class.
  - Each aggregate keeps a record of domain events in a field and they are triggered and executed once the aggregate is saved in the application layer.
  - Using IOC container to scan all the Event Handlers and invoke them in Aplication Layer.
-Testing Domain Events

## Domain Services

- IDDD
- A stateless operation that fulfills a domain specific task.
- Best Indication that you should create a domain service in the domain model is when the operation you need to perform feels out of place as a method on an aggregate or value object.
- We DON't want to house business logic in an Application Service, but we DO want business logic housed in a Domain Service.
- Domain service is a client to Application Service.
- Operation name of Domain Service is a part of Ubiquitous Language. 


### Inspired By

#### Github


#### Event Storming

- [mariuszgil/awesome-eventstorming](https://github.com/mariuszgil/awesome-eventstorming)
- [ddd-crew
/
eventstorming-glossary-cheat-sheet](https://github.com/ddd-crew/eventstorming-glossary-cheat-sheet)

#### Articles


#### Books

- [Implementing Domain-Driven Design](https://www.oreilly.com/library/view/implementing-domain-driven-design/9780133039900/)
- [Patterns, Principles, and Practices of Domain-Driven Design](https://www.oreilly.com/library/view/patterns-principles-and/9781118714706/)
- [Domain-Driven Design: Tackling Complexity in the Heart of Software](https://www.oreilly.com/library/view/domain-driven-design-tackling/0321125215/)
- [Hands-On Domain-Driven Design with .NET Core](https://www.packtpub.com/in/application-development/hands-domain-driven-design-net-core)
 
