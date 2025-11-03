---
tags:
  - "#data_mining"
  - "#Overview"
---
____
# What is Data Mining?
Example 1: Web usage mining (E-commerce website)
- Given: Click stream (click on), Interaction behaviour
- Problem: Prediction of user behaviour.
- Data: Historical records of embryos and outcomes (web log - times: activity).
Example 2: Cow culling
- Given: cows described by 700 features
- Problem: Selection of cows that should be culled
- Data: Historical records and farmers’ decisions (experience provided by humans)
## Core Concept: Extracting Information
Extracting:
- Explicit: information is not discovered
- Previously unknown: 
- Potentially useful
	Information from data
Needed: programs that detect patterns and regularities in the data (only using a computer to detect the patterns = data mining).
**Strong patterns $\rightarrow$ good predictions.**
## Challenges/Problems with Patterns
- Problem 1: Patterns are not interesting
- Problem 2: Patterns may be inexact (or spurious)
- Problem 3: Data may be garbled or missing

**Data Mining**: Extraction of interesting patterns or knowledge from a **huge amount of data**. The **process** of **analysing data** from diverse perspectives and summarising it → useful information.
- Alternative name: Knowledge discovery in DB (KDD)
- Attributes:
	- Must be automatic or semiautomatic.
	- The patterns discovered must be meaningful → advantages
---
# Data Mining Goals
- Extract information from a data set.
- Transform it into an understandable structure for further use.
- The ultimate goal of data mining is **prediction**.
----
# Stages of the Data Mining Process
**Levels:**
1. **Data Sources**: Paper, Files, Web documents, Scientific experiments, Database Systems.
2. **Data Preprocessing/Integration, Data Warehouses**.
3. **Data Exploration**: Statistical Summary, Querying, and Reporting.
4. **Data Mining**: Information Discovery.
5. **Data Presentation**: Visualization Techniques.
6. **Decision Making** (End User / Business Analyst).
## KDD Process
This view comes from typical database systems and data warehousing communities. Data mining plays an essential role in the KDD process.
**Stages:**
1. Databases $\rightarrow$ Data Integration $\rightarrow$ Data Cleaning $\rightarrow$ Data Selection $\rightarrow$ Data Warehouse.
2. **Data Mining** (Pattern discovery, classification, clustering, etc.).
3. Post-Processing (Pattern evaluation, visualization).
Input Data → Data preprocessing → Data Mining → Post-processing → Pattern information knowledge
----
# Data Mining Techniques
Data Mining:
- ML
- Pattern Recognition
- Statistics
- Visualization
- Applications
- Algorithm
- DB technology
- High-performance computing
## Why the Confluence of multiple disciplines?
- A tremendous amount of data
- High-dimensionality of data (different types of data - picture, text, number)
- High complexity of data (different ways to present data)
- New and sophisticated applications
## ML techniques
Algorithms for acquiring structural descriptions from examples
Structural descriptions represent patterns explicitly
- Predict the outcome in a new situation
- Understand and explain how prediction is derived
## Can machines really learn?
- **Dictionary definition** of "learning" (gaining knowledge, becoming aware) is **difficult to measure** or **trivial for computers**.
- **Operational definition**: Things learn when they change their behavior to perform better in the future. This leads to the question: Does learning imply intention?
----
# Knowledge Representation Methods
- Tables
- Data cubes
- Linear Models
- Trees
- Rules
- Instance-based Representation
- Clusters
---
# Applications
The result of learning is deployed in practical applications:
- Processing loan applications (American Express).
- Screening images for oil slicks.
- Electricity supply forecasting.
- Diagnosis of machine faults.
- Marketing and sales (Customer loyalty, Market basket analysis).
- Separating crude oil and natural gas.
- Scientific applications (biology, astronomy, chemistry).
- Monitoring intensive care patients.