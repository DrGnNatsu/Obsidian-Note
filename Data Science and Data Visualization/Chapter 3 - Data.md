#DataScienceAndDataVisualization 
#Data #DataTypes #DataSetTypes #Infovis #Scivis
___
## Data
- **Dataset Types**: 
	- **Fields (Continuous)**:
		- Sets of attributes values associated with cells
		- The cell contains data from the continuous domain.
		- *Ex:* 
			- Temperature, pressure, wind velocity. 
			- Measured or simulated: Sampling & Interpolation. 
			- Signal processing & stats
	- **Geometry (Spatial)**:
		- Explicit spatial positions: Points, lines, curves, surfaces, regions, volumes.
		- Important in Computer Graphics, CAD.
		- Not a core visualization topic
	- **Flat Table**s:
		- one item per row
		- Each column is an attribute.
		- Unique (implicit) key
		- ==**No duplicates**==
	- **Multidimensional Tables**: Indexing based on multiple keys
	- **Networks/Graphs**: Set of nodes, set of edges, connecting these vertices
		- A bipartite graph: Vertices can be partitioned into two independent sets.![[BipariteGraph.png]]
		- An articulation point Is a vertex that, if deleted, would break up a connected graph. ![[ArticalationPoint.png]]
	- **Trees**: which is a graph with no cycles.
- **Data Types**: Structural or mathematical interpretation of data: Items, Attributes, 
	- **Links**: Express the relationship between two items. Ex: Friendship on Facebook
	- **Positions:** Spatial data -> location in 2D or 3D. Ex: Pixels in photo, Voxels in MRI scan, latitude/longitude.
	- **Grids:** A sampling strategy for continuous data. Ex: How many Voxels in an MRI scan, positions of weather stations in a city
		- Uniform grid: Geometry & topology can be computed
		- Rectilinear Grid: Nonuniform sampling
		- Structured grid: Allow curvilinear grids.
		- Unstructured grid: full flexibility, store position and connection
	⇒ *Different from data types in programming!*
![[Data(set)Type.png]]

| Structure                        | Unstructured                                                                                               |
| :------------------------------- | :--------------------------------------------------------------------------------------------------------- |
| - Know data types, semantics<br> | - No predefined data model<br>- Text, interspersed with facts (dates, times, locations)<br>- Video, Images |
**Translate into structured data** ⇒ NLP, text mining, object recognition, and tracking. 
___
## Items and Attributes
- **Items**: individual entity, discrete (e.g., Patient, Car, Stock, city) “independent variable”
- **Attribute**: measured, observed, logged properly (e.g., Patient: height, blood pressure Car: horsepower), make “dependent variable”.
	- Categorial (nominal): Compare equality: Operations: =, ≠
	- Ordinal (ordered): Great/ less than defined: Operations: =, ≠, >, <
	- Quantitative (arithmetic possible): length, weight
		- Interval (location of zero arbitrary): Operations: =, ≠, >, <, +, - (distance)
		- Ratio (zero fixed): Operations: =, ≠, >, <, +, -, ×, ÷ (proportions)
___
## Collections
- **Sets**: *Unique items, unordered*
- **List**: *Duplicates allowed, ordered*
- **Clusters**: *Group of similar items*
___
## Academic Subfields

| Information Vis                                                                                       | Visual Analytics                                                                | Scientific Vis                                                                                              |
| :---------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------- |
| - Abstract Data: Tables, Graphs, Maps<br>- Free to choose the spatial layout<br>- Perception Research | - Info Vis + Stats + ML<br>- Applied to work<br>- Systems<br>- Funding buzzword | - Spatial Data: Fields<br>- Not free to choose the spatial layout<br>- Find the best way to depict reality. |
![[InfoVis_SciVis.png]]
___
## Sequential and Diverging Data
| Sequential                   | Diverging                                                                                                         | Cyclic                                                          |
| :--------------------------- | ----------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| - Homogenous from min to max | - Two / multiple sequence to meet                                                                                 | - Time <br>- Aggregation: Might be patterned on multiple levels |
|                              | - Elevation dataset: above sea level & below sea level<br>- Temperature of water: below or above freezing/boiling |                                                                 |
___
## Data vs Conceptual Model
| Data model                          | Conceptual Model                        |     |
| :---------------------------------- | --------------------------------------- | --- |
| - Low-level description of the data | - Mental construction                   |     |
| - Set with operations               | - Includes semantics, support reasoning |     |
| 19.5, 29.0, -1 (floats)             | Temperature                             |     |
| 1D floats                           | Temperature                             |     |
| 3D vector of floats                 | Space                                   |     |
⇒ To Datatypes:
- Continuous to 4 significant digits (Q)
- Hot, warm, cold (O)
- Burned vs Not burned (N)
⇒ Networks can have attributes. Attributes have hierarchies. Data types can be transformed