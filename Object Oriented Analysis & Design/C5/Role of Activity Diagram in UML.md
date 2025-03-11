___
**How can we generate the process to fulfill the use cases?**
- Use Case: We only stop at what we have in the system (not efficient and hard to understand) and how the role interacts with the system.
⇒ **Activity diagram**: can fulfill it - the deeper level of understanding what we are going to design to follow the descriptions and expectations from the product owner.
___
# Why is an Activity Diagram?
- Activity Diagrams describe the workflow of the system.
- Activity Diagrams are useful for analysing a use case by describing what actions need to be performed and where they occur.
- Benefits include clarity, decision timing and problem identification.
___
# When to Use Activity Diagrams?
- Activity diagrams show behavior that spans over multiple use cases to describe the workflow of the overall process.
- For multiple objects and their high-level interaction, activity diagrams are particularly helpful for representing an overview of concurrent processes.
- Do not use activity diagrams to see how objects collaborate. An interaction diagram is simpler and gives you a clearer picture of collaborations.
- Activity diagrams are not accurate for describing how an object behaves over its lifetime. Use a state diagram instead.
___
# How to create an Activity Diagram?
We have two ways (perspectives) to create the modeling of a single use case:
- Conceptual Perspective:
	- Focuses on **high-level understanding** of the process.
	- Represents activities **without considering implementation details**.
	- Uses **actors** and **abstract steps** to define the sequence of actions.
	- Helps business analysts and non-technical stakeholders understand the flow.
	- *Example*: Actions (Tasks or Steps), Decision Nodes (Branches), Forks & Joins (Parallel Execution), Start & End Points
- Specification Perspective:
	- Focuses on **detailed system implementation**.
	- Defines **how** activities are performed and **who** performs them.
	- Includes interactions with the **database, APIs, and system components**.
	- Used by developers to understand the logic of a use case.
	- *Example*: System Methods (API calls, database operations), Business Logic (Validation, Computations), External Systems (Third-party integrations)
___
# NOTE
Tìm hiểu thêm về BPMN (Businesses Process Modeling and Notations) - thiên về economic 
- Có cấu trúc tượng tự Activity Diagram (thiên về kĩ thuật)