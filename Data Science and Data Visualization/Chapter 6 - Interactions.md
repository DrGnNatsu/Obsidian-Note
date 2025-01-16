#DataScienceAndDataVisualization 
#Design #Interaction  #Purpose #Why 
[[Chapter 5 - Design Guideline]]
___
## Spectrum
| Static Content | Dynamic Content                                               |
| :------------- | ------------------------------------------------------------- |
| Infographics   | For animated content ‘Auto-play’, the user is not in control. |
| Books          | Interactive content. <br>Changes are a result of user actions |
___
## Why Interaction with Visualization
**⇒**Need to explore data that is big / complex.
- Too much data ⇒ Too many ways to show it
\- **Interaction amplifies cognition**:
- Understand things better if we can touch them.
- When we can observe cause and effect.
___
## Direct Manipulation.
| Interact directly with objects  | Indirect interact |
| :------------------------------ | :---------------- |
| Continuous feedback and updates | Query, slides     |
___
## Types of interaction

| **Single view**        | **Multiple views**             |
| :--------------------- | :----------------------------- |
| Change over time       | Selections (Details on demand) |
| Navigation             | Linking and Brushing           |
| Semantic Zooming       | Adapting representation        |
| Filtering and Querying |                                |
| Focus and Context      |                                |
___
## Purpose of Interaction
| Data & View Specification                         | View Manipulation                                                   | Process & Provenance                                                 |
| :------------------------------------------------ | :------------------------------------------------------------------ | -------------------------------------------------------------------- |
| ***Visualize*** data by choosing visual encodings | ***Select*** items to highlight, filter, or manipulate them         | ***Record*** analysis histories for revisitation, review and sharing |
| ***Filter*** out data to focus on relevant items  | ***Navigate*** to examine high-level patterns and low-level details | ***Annotate*** patterns to document findings                         |
| ***Sort*** items to expose pattern                | ***Coordinate*** views for linked, multi-dimensional exploration    | ***Share*** views and annotations to enable collaboration            |
| ***Derive*** values or models from source data    | ***Organize*** multiple windows and workspaces                      | ***Guide*** users through analysis tasks or stories                  |
___

___
## Transitions
### Change over time
- Use slides to see view with data at different times 
- Sometimes better to show difference explicitly
- Doesn't have to be ==literal time== → Change as you go as part of an analysis process

___
## Why transitions ?
- Different representations support different tasks: Bar chart vs stacked bar chart
- Change ordering 
- Transition make it possible for users to track what is going on.
___
## Animated Transitions
\- Smooth interpolation between states or visualization techniques
### Warning
- Changes can be hard to track
- Eyes over memory
- Show all states in multiple views
___
## Navigation
- **Pan**: Move around
- **Zoom**: Enlarge/make smaller
- **Rotate**
- **Scroll**
### Scroll-telling
| Pros                         | Cons                                    |
| :--------------------------- | --------------------------------------- |
| Telling an interactive story | Continuous scrolling vs discrete states |
| Interaction by scrolling     | Direct access                           |
|                              | Unexpected behaviour                    |
### Zooming: Semantic zooming
- Update content on zooming"
* More detail as more space becomes available
* Ideally readable at multiple resolutions
___
## Focus + Context
\- Carefully pick what to show
\- Hint at what you are not showing
\- Synthesis of visual encoding and interaction
\- User selects regions of interest (focus) through navigation or selection
\- Provide context through: aggregation, reduction, layering, and embedding (slides 26)
- **Elision**: Focus item shown in detail: Other items summarized for context
___
## Degree of Interest (DOI)
\- Represent objects in the neighborhood in detail, and only major landmarks far away Balance between local detail and global context
$$
DOI(x) = I(x) – D(x,y) 
$$
 - I(x): interest in object x 
 - D – a distance function to the current focus y of x 
 - There may be many foci.
### DOI tree
- An interactive tree with animated transitions that fit within a bounded region of space layout depends on the user's estimated DOI.
	- logical filtering based on DOI
	- Geometric distortion of node size based on DOI
	- Semantic zooming on content based on node size.
	- Aggregate representations of elided subtrees
![[DOI Tree.png]]
___
## Superimpose
- The focus layer is limited to a local region of view. 
- Instead of stretching across the entire view
### Tool-glass & Magic lenses
\- **Magic lenses**: details/different data are shown when moving a lens over a scene.
![[Magic Lenses.png]]
### Distortion
\- Use geometric distortion of the contextual regions to make room for the details in the focus regions(s)
- Distortion Corner:
	- Unsuitable for relative spatial judgements
	- Overhead of tracking distortion.
	- Visual communication of distortion gridlines, shading
	- Target acquisition problem lens displacing items away from screen location.
	- Mixed results compared to separate views and temporal navigation.
![[Distortion.png]]
### Perspective Wall
![[Perspective Wall.png]]
### Fish Eye (slides 38)
### Hyperbolic Geometry (slides 39)
___
## Overview + Detail
\- One view shows an overview and Other shows detail![[Overview and Detail.png]]
___
## Filter and Dynamic Querying
### Mantra
\- Visual information seeking matra (Shneiderman, 1996)
1. Overview first
2. Zoom and filter
3. Then details on demand
\- Related history, extract
### Dynamic Queries (slides 48)
\- Define criteria for inclusion/exclusion.