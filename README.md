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
  
 
