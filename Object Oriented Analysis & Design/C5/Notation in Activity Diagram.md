![[Structure of Activity Diagram.png]]
___
# Notation
- The **Initial node** is unique and must appear in the Activity Diagram, notation is the black point. Two types:
	- Initial node for use cases
	- Initial node for the system
- The **Final node** can have many in the Diagram (or empty based on the context), notation is the black point with the ring. Two types:
	- Final Node for use cases
	- Final Node for the system
- **Decision point**:
	- A decision point shows where the exit transition from a state or activity may branch in alternative directions depending on a condition.
	- A decision involves selecting one control-flow transition out of many control-flow transitions based on a condition.
	- Guard expression (inside `[]`) label the transitions coming out of a branch. (same as the if statement).
	- The return value of the Guard (boolean expression) is a boolean ( `true` or `false`)
![[Guards_DecisionPoint.png]]
- **Swimlanes**:
	- A swimlane is a way to group activities performed by the same actor on an activity diagram or activity diagram or to group activities in a single thread.
	- Swimlanes are indicated by vertical dashed lines, which separate the diagram into zones.
	- Swimlanes allow the partition an activity diagram so that parts of it appear in a swimlane relevant to that element in the partition.
- **Concurrent Activities:**
	- The difference between flowcharts and activity diagrams is that in the activity diagram, parallel behavior can be expressed.
	- This is important for business modeling, where unnecessary sequential processes can be designed for parallel execution.
	- Enabling to graphically l**ay out what threads you have and when they need to synchronize**.
	- **Synchronization Bars**: initiate concurrent sections in AD. In these concurrent sections, triggers can occur in parallel and no sequential order is established.
![[Synchronisation_bar.png]]
## Activity Edge vs Trigger
| Feature            | **Activity Edge**                                                          | **Trigger**                                                               |
| ------------------ | -------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| **Definition**     | A connector that represents the flow between nodes in an activity diagram. | A condition or event that causes a transition from one action to another. |
| **Representation** | A **solid arrow** connecting activity nodes.                               | A label on a transition (event-driven change).                            |
| **Function**       | Defines **the sequence of execution** between activity nodes.              | Defines **what causes an action to start**.                               |
| **Connections**    | **Connects nodes** (Activity Nodes, Decision Nodes, Forks, Joins).         | **Connects actions** by specifying conditions for transition.             |
| **Example**        | **"Login" → "Dashboard"** (Edge connecting two activity nodes).            | **"User clicks login"** → Starts "Authenticate User".                     |
## Activity Vs Process

|Feature|Activity|Process|
|---|---|---|
|**Definition**|A single step or action within a system.|A sequence of multiple activities forming a complete workflow.|
|**Granularity**|**Smallest unit** of work (e.g., "Enter User Details").|**Larger workflow** made up of multiple activities (e.g., "User Registration Process").|
|**Scope**|Focuses on a **specific action**.|Focuses on **how multiple actions** interact to complete a goal.|
|**Example**|"Send Confirmation Email"|"User Registration" (includes activities like filling a form, validating details, sending a confirmation email, etc.)|
___
# Note
An **Activity Diagram** without a final node represents an **ongoing process (waiting process)** or a **looping system** where there is no definite termination.
## **Case Study: Live Stock Market Monitoring System**

A stock market monitoring system continuously fetches, analyzes, and updates stock prices in real-time. Since stock markets are always active during trading hours, the process does not have a final node.