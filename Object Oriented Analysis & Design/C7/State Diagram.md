___
# Why State Diagram?
- How do we catch the dynamic behaviour and life cycle of an object?
	- Creation and deletion.
	- Attribute and association changes.
- How does the object interact with other objects?
	- Reacting to events and messages received by the object.
	- Triggering actions and sending messages to other objects.
	- Handling of sequences of events and actions triggered.
# State Diagram
State diagrams are a technique to describe the behaviour, i.e., state changes of a single class according to events and messages that the class sends and receives. The states must be unique.
The Initial State is a must-have, and the final state can have many. 
# Activity Diagrams Vs Activity Diagram
- Activity Diagrams are reducible to State Diagrams with some additional notations.
- Activity Diagrams: Vertices **represent the carrying out of an activity**, and the edges **represent the transition from completing one collection of activities** to the commencement of a new collection of activities.
- State Diagrams: Vertices **represent states of an object in a class (changes the object's meaning),** and **edges represent occurrences of events (changes the states of the object)**
# States
- A state: 
	- abstracts from attribute values and associations of an object;
	- represents the internal condition/state of an object for a certain period;
	- Corresponds to an interval of time between two events.
- The response to events may **depend on the state of an object**, which means that the states, the context, and the perspective of the developer define the response messages.
- Object creation comes together with an initial object.
![[States_Example.png]]
# Events
- Internal or External Events **trigger some activity that changes the state** of the system and some of its parts.
- Events pass information, which is elaborated by object operations. Objects realise Events.
- Design involves examining events in a State Diagram and considering how those events will be supported by system objects.
- Events may be declared in a class diagram with arguments shown as attributes.
![[Events.png]]
# Transitions
- A transition represents a change in the internal condition/state of an object.
- A transition is usually triggered (“fired”) by an event. Transitions without event label (“lambda transitions”) fire immediately.
- Transitions fire instantly: from exactly one state to another state or to itself (self-transition).
- Multiple transitions occur either when different events result in a state terminating or when there are guard conditions on the transitions.
- A transition without an event and action is known as an automatic transition.
# Guards
- Guards ensure that a transition only happens under certain conditions.
- A guarded event is an event that has a guard condition associated with it.
- **Syntax**: event (guard) / action (action can be void).
# Actions
