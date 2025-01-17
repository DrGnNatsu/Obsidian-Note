#DataScienceAndDataVisualization 
#When #Why 
___
## Problem-Driven Vs Technique-Driven
| Problem Driven                                        | Technique Driven                                        |
| :---------------------------------------------------- | ------------------------------------------------------- |
| Top-down Appproach                                    | Bottom-up approach                                      |
| Identify a problem encountered by users               | Invent new visualisation techniques or algorithms       |
| Design a solution to help users work more effectively | Classify or Compare against other idioms and algorithms |
___
## The Nested Model
![[Nested Model.png]]
___
## Design Process
\- Understand domain problem → Map to abstract task & Data type and other factors → Identify and Implement suitable technique.
### Domain Characterization
- **Details of an application domain**
- **Group of users, target domain, their questions, their data** Varies wildly by domain and must be specific enough to continue with
- **Cannot just ask people what they do** introspection is hard
### Domain Problem Characterization
- Infinite numbers of domain tasks
- Can be broken down into simpler abstract tasks
- We know how to address abstract tasks.
- Identify task – task-data combination: solutions probably exist
- ==Eg==: Slides 7
### Data & task Abstraction
- The what-why, map into generalized terms
- Identify tasks that users wish to perform or already do
- Find data types and a good model of the data.
- Sometimes must transform the data for a better solution this can be varied and guided by the specific task
- ==Eg==: Slides 9
### Encoding & Interactions
- The design of visualisation techniques:
	- Visual encodings
	- Interactions
- Ways to create and manipulate the visual representation of data
- Decisions on these may be separate or intertwined. 
- Visualisation design principles drive decisions.
- ==Eg==: Slides 11
### Tasks
- **Analyze:** 
	- High-level choices
	- Consume vs produce
- **Search:** Find a known/unknown item
- **Query:** 
	- Find out about the characteristics of the item 
	- By itself or relative to others
### High-Level Actions: Analyze
| Consume                                                           | Analyze                       |
| :---------------------------------------------------------------- | ----------------------------- |
| Discover Vs Present                                               | Annotate and Record           |
| - Classic split: Explore Vs Explain<br>- Enjoy: Casual and Social | Derive: Crucial design choice |
![[Analyze.png]]
### Mid-Level Actions: Search, Query
| Search              | Query            |
| :------------------ | ---------------- |
| Target and Location | One, Some or All |
![[Search_Query.png| 480]]
### Low-Level: Targets
![[Targets.png]]
___
## Designing Visualisation
### What is Design?
- Creating something new to solve a problem
- Can be used to make buildings, chairs, user interfaces, etc.
- Design is used in many fields. 
- Many possible users or tasks
### Not Design
- Just making things pretty. 
- Art – appreciation of beauty or emotions invoked
- Something without a clear purpose
- Building without justification or evidence
### Form & Function
- Commonly: Form follows function
- The function can constrain possible forms: The form depends on tasks that must be achieved.

>“The better defined the goals of an artifact, the narrower the variety of forms it can adopt” Alberto Cairo
### When Design?
- **Wicked problems**:
	- No clear problem definition
	- Solutions are either good enough or not good enough.
	- Multiple solutions exist, not true/false.
	- No clear point to stopping with a solution
- Example’?'s of non-wicked (“tame”) problems: Mathematics, chess, puzzles
### Why Does Design Matter for Vis?
- Many ineffective visualisation combinations
- Users with unique problems & data
- Variations of tasks
- Large design space
### Pitfall
\- We need to extend our knowledge (design space) to know what is good or bad ⇒ Consider what we need to use ⇒ Propose ⇒ Select it to project
==Eg==: Slides 22 → 29
### Evaluation Methods
- **Controlled experiment**: Laboratory, crowd-sourced
- **Interviews/questionnaires**: Unstructured, structured, semi-structured
- **Field observation, lab observation**: 
	- Video/audio analysis
	- Coding/classification of user behaviour (speech, gestures)
- **Log analysis**: Algorithmic performance measurement
- Heuristic evaluation: Judge compliance with recognized metrics/usability methods (heuristics) 
- Usability testing, e.g., thinking-aloud tests
- Wizard of Oz:
	- Human simulates the response of the system.
	- Test functionality before it’s implemented
- Eye tracker evaluation
- Expert evaluation
- Insight-based evaluation
- Case studies
### Quantitative Vs Qualitative Evaluation
| Quantitative methods                         | Qualitative methods                                                                                                                                                                                                                                                                       |
| :------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Objective metrics, measurements              | Subjective metrics                                                                                                                                                                                                                                                                        |
| Use numbers/statistics for interpreting data | - Description of situations, events, people, interactions, and observed behaviours, the use of direct quotations from people about their experiences, attitudes, beliefs, and thoughts<br>- Focused on understanding how people make meaning of and experience their environment or world |
### Internal Vs External Validity
| Internal validity                                                          | External validity                                                                        |
| :------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| Can you trust your experiment?                                             | Is your experiment representative of real-world usage                                    |
| High when tested under controlled lab conditions                           | High when the interface is tested in the field (e.g. handheld device tested in a museum) |
| Observed effects are due to the test conditions (and not random variables) | Results are valid in real-world                                                          |
\- **The Trade-off**: The more akin to real-world situations, the more the experiment is susceptible to uncontrolled sources of variation
### Scope of Evaluation
![[Scope of Evaluation.png]]
- **Pre-design**: To understand potential users’ work env. And workflow
- **Design:** To scope a visual encoding and interaction design space based on human perception and cognition
- **Prototype:** to see if a visualization has achieved its design goals, to see how a prototype compares with the current state-of-the-art systems or techniques
- **Deployment:** to see how a visualization influences workflow and work processes, to assess the visualization’s effectiveness and use in the field.
- **Re-design**: to improve a current design by identifying usability problem