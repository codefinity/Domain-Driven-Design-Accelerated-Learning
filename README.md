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
- Need a context of an entity to be relevant
- Comparable: Considered equal if they have the same value
- Behaviour Rich: 
  - Should expose expressive donain-oriented behavior, through methods
  - Encapsulate state 
  - All primitive types in it should be private or protected
- Cohesive: A value object should contain related concepts





## Entities

## Aggregates
