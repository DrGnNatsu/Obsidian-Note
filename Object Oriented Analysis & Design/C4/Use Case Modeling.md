![[Use_Case_Modeling.png]]
In the domain model, we can see how many classes, the data transfer and the interaction between the classes.
In the use case model, we focus on the abstract of the class that is the functionality of the system. With the specified actor, they will have different functionality. 
___ 
# Usefulness of Use Case Diagram in UML
![[Role_of_ Use_Case_Diagram.png]]
- The Use Case Diagram is the first phase to develop the software by transforming the requirements into the diagram.
___
# Components of Use Case
1. An actor: is external to a system, **interacts with the system**, may be a human user or another system, has a goal and responsibilities to satisfy in interacting with the system.
	1. An actor **is a role** that a user or other system plays concerning the system to be developed.
	2. A single actor in a use case diagram can represent multiple users (or systems).
	3. A single user (or system) also may play multiple roles.
	4. **Actors don’t need to be human**, e.g., an external system that needs some information from the current system.
2. Use Case:
	1. Identify functional requirements
	2. Describe actions performed by a system
	3. Capture interactions between the system and actors
	4. The “case aspect” in a use case represents a high-level description of a desired action in which the actor is involved. We understand that the use case is a set of functions that represents a process.
		1. Ex: Purchase is a use case. Inside the purchase process, we have many steps (we do not need to separate it to many steps to treat as use cases)
	5. Each UseCase specifies a unit of useful functionality that the subject provides to its users.
3. Relationships: Actors are connected to the use cases with which they interact by a line, which represents a relationship between the actors and the use cases.
![[UseCase_Relationship.png]]