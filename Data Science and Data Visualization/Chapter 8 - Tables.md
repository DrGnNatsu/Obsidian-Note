#DataScienceAndDataVisualization 
#Chart #Data #DataSetTypes #Design 
[[Chapter 3 - Data#Data]]
___
## Scale of Tables
- Need different approaches for 'normal' and 'high-dimensional' tables
- **How many dimensions?**
	- ~ 50 - tractable with 'just' visualisation ~1000 – need analytical methods"
- **How many records?** 
	- ~ 1000 – 'just' vis is fine → 10 000 – need analytical methods
- **Homogeneity**
	- Same data type? 
	- Same scales?
___
## Techniques and Tasks
External Link: https://ft-interactive.github.io/visual-vocabulary/
- Magnitude:
	- Show size comparison:
		- Relative: to see bigger/larger
		- Absolute: to see differences
		- ==Eg==: Usually for “counted” numbers rather than a calculated rate or per cent
		- Chart: Bar chart
- Distribution: 
	- *Aggregating large data vectors*
	- Instead of showing all data points, show a data’s distribution
	- Pro: Compact representation
	- Con: Works only if data is “well behaved” for the type of distribution visualisation
	- Chart: Histogram
	- Different distributions: slides 30
- Ranking:
	- ==Eg==: Slides 50 → 55
	- Chart: Table lens, Lineup
- Part to whole: **Show how a single entity can be broken down into its component elements**
	- If the interest is solely in the size of the component
	- Consider magnitude-type chart
	- Chart: Stacked Bar Chart, Pie Chart, Donut Chart, Tree-map, Stack Area
- Deviation:
	- ==Eg==: Slides 34 
- Correlation
- Change over time:
	- ==Eg==: Slides 36 → 48
	- Chart: Line chart, Stacked Area, Multiple Line Charts, Horizontal Graph, Clipped Graphs, Heat Map
		- Sparklines: Small line charts. can be embedded in text or part of a table
		- Connected Scatterplot: Two Variables + Time: Only one per Chart! Labels important
___
## Histogram
[[Chapter 8 - Tables#Techniques and Tasks]]
- Good bins hard to predict
	- Unequal bin width: Slides 21
- Make interactive
- Rules of thumb:
$$
bins = sqrt(n)
$$
$$bins = log_2(2) +1$$
___
## Plots
- Density plots (Slides 22)
- Box Plots (Slides 23 → 26)
- Comparison (Slides 27)
- Bar Chart Vs Dot plots (Slides 28)
- Violin Plots = box plot + probability density function (Slides 29)
___
## Data Flaws
### Detecting Data Flaws (slides 32)
\- Tricky with aggregate visualization: Bin size/ kernel type/ bandwidth/ visualization choice all affect different situations 
___
## Combiner Function
- Weighted sum $$Score = w_2A + w_bB + W_cC$$ → Serial
- Maximum $$Score = max (A, B, C)$$ → Parallel
- Product Nesting → Complex
- ==Eg==: Slides 58 → 62
