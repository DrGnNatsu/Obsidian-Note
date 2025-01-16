#DataScienceAndDataVisualization 
#Detail #Overview #Partition #Why
[[Chapter 6 - Interactions]]
___
## Design choices for Multiple Views
![[Multiple Views Designs.png]]
___
## Why Multiple Views?
- **Eyes beat memory**: Showing two views side by side is easier to compare than changing views over time.
- **No single visual encoding is optimal for all possible tasks**: Use different encoding for one data.
- **Too many to be shown in one view**
### Linked Views
- Multiple views are simultaneously visible and linked together.
- Actions in one view affect the others.
#### Options
- Highlighting (slides 6, 7): to link, or not.
- Navigation: to share, or not
- Encoding: same or multiform
- Dataset: Shared all, subset, or none
![[Linked View Options.png]]
### Multiform
\- Different visual encodings are used between views: 
- shared data: either all data or a subset of data (overview + detail)
\- Rational:
- Single view has strong limits on the number of attributes that can be shown simultaneously.
- Different views support different tasks.
==Eg==: Slides 10 → 12
___
## Overview + Detail
[[Chapter 6 - Interactions#Overview + Detail]]
\- One view shows (often summarized) information about the entire dataset
\- Additional view(s) show more detailed information about a subset of the data
\- Rational: For large or complex data, a single view of the entire dataset cannot capture fine details
==Eg==: Slides 14 → 17
___
## Small Multiples for Graph Attributes (Slides 19)
\- **Each view uses the same visual encoding but shows a different subset of the data**
\- Rational: Quickly compare different parts of a dataset, relying on eyes instead of memory.
==Eg==: Slides 19 → 22
___
## Partitioning
\- **Action on the dataset that separates the data into groups**
\- **Design Choices:**
- How to divide data up between views, given a hierarchy of attributes
- How many splits, and order of splits
- How many views (usually data-driven)
\- Partition attribute(s): Typically categorical
==Eg==: Slides 25 & 26
![[Partition Example.png]]
### Trellis
#### Plots
- **Panel variables** are encoded in individual views.
- **Partitioning variables** assigned to columns and rows.
- **Main-effects ordering**: order partitioning variable based on derived data support perception of trends and structure in data
![[Trellis.png]]
==Note==: Define the Plots
![[Trellis's Variables.png]]
____
## Recursive Subdivision
\- **Partitioning:** Flexibly transform data attributes into a hierarchy using **treemaps** as space-filling rectangular layouts
==Eg==: Slides 32
___
## Layering
\- **Combining multiple views on top of one another**
\- **To form a composite view**
\- **Rational**: It supports a larger, more detailed view than using multiple views
\- **Trade-off**: Layering imposes constraints on visual encoding choice, as well as the number of layers that can be shown.
==Eg==: Slides 36 → 39 
### Dynamic Layering
==Eg==: Slides 44 → 46 
___
## Dual Axis (Slides 40 & 41)
___
## Combined
\- Partitioned + layered graph
\- Synchronised through highlighting
![[Combined Graph.png]]