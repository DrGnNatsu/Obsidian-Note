#data_mining  #

___
## Types of the Data Sets
- Records:
- Graph and Network:
- Ordered:
- Spatial, Image and Multimedia:
## Important Characteristics of Structured Data
- Dimensionality
- Sparsity
- Resolution
- Distribution
## Data objects
- Made up the datasets
- Represents an entity
- Called: samples, examples, instances, data points, objects, tuples
- Described by attributes
- In the Databases:
	- The row represents *Data objects*.
	- The column represents *Attributes*.
### Attributes
- Called: Dimensions, features, variables
- A data field
- Represents one of the characteristics of data objects
- Main types:
	- Nominal: categories, states
	- Binary: two states (*0 or 1*), two types:
		- Symmetric binary: both outcomes are equally important:
			- Ex: gender
		- Asymmetric binary: outcomes are not equally important
			- *Note:* Which one is more important, denoted by 1
			- Ex: medical test (positive and negative)
	- Ordinal: values have a meaningful order (ranking), but the magnitude between successive values is not known.
		- Ex: Size = {small, medium, large}.
	- Numeric: quantitative attributes
		- Interval-scaled: Measured on a scale of equal-sized units
			- Values have order: temperatures
			- No true zero-point
		- Ratio-scaled: Measured on a scale of equal-sized units
			- We can speak of values as being an order of magnitude larger than the unit of measurement
			- Inherent zero-point
#### Discrete vs. Continuous Attributes

| Discrete                                                                      | Continuous                                                                                       |
| ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| A finite or countably infinite set of values                                  | Real numbers as attribute values                                                                 |
| Sometimes, represented as integer variables                                   | Continuous attributes are typically represented as floating-point variables                      |
| *Note:* Binary attributes are a special case of discrete attributes           | Practically, real values can only be measured and<br>represented using a finite number of digits |
| E.g., zip codes, profession, or the set of words in a collection of documents | E.g., temperature, height, or weight                                                             |

# Basic Statistical Descriptions of Data
___
- Motivation
- Data Dispersion Characteristics
- Numerical Dimensions
- Dispersion analysis on computed measures
## Measuring the Central Tendency
**Mean:** The average of the data
$$
\bar{x}= \dfrac{\sum_{i=1}^{n}w_ix_i}{\sum_{i=1}^{n}w_i}
$$
**Median:** Middle value if odd values, or the average of twos middle values of the sequences
$$
median = L_1 + \frac{\tfrac{n}{2} - \left(\sum freq \right)}{freq_{median}} \times width
$$
**Mode:** Value that occurs most frequently in the data
- Unimodal
- Bimodal
- Trimodal
$$
mean-mode = 3 \times(mean-median)
$$
**Variance:**
- Standard variant is $\sigma$ is the square root of $\sigma^2$
$$
\sigma^2 = \dfrac{1}{N} \sum_{i=1}^{N} (x_i - \bar{x})^2 
$$
## Symmetric vs. Skewed Data
If $mean = mode = median$ ⇒ Sysmetric
If $mode < median < mean$ ⇒ Negative skewed
If $mean < median < mode$ ⇒ Positive skewed

## Boxplot
- **Quatiles:** Q1 , Q3
- **Inter-quartile range:** $IQR = Q_3 - Q_1$
- Five number summary: min, $Q_1$, median, $Q_3$, max
- **Outlier:** The value point is in the range $$x < Q_1 -1.5 \times IQR \quad or \quad x > Q_3+1.5 \times IQR$$
- **Min and Max:** the min and max value but it is not outliers
## Properties of Normal Distribution Curve
The normal (distribution) curve
# Measuring Data Similarity and Dissimilarity
___
## Similarity and Dissimilarity
**Similarity**:
- Numerical measure of how alike two data objects are
- Value is higher when objects are more alike
- Often falls in the range [0,1]
**Dissimilarity** (e.g., distance):
- Numerical measure of how different two data objects are
- Lower when objects are more alike
- Minimum dissimilarity is often 0
- Upper limit varies
- Dissimilarity Matrix: slides
**Proximity** refers to a similarity or dissimilarity
## Proximity Measure for Nominal Attributes
Can take 2 or more states, e.g., red, yellow, blue, green(generalization of a binary attribute)
$$
d(i,j)=\dfrac{p-m}{p}
$$
m: number of matches, p: total number of variables
## Proximity Measure for Binary Attributes (slides)
*Proximity Measure for Binary Attributes*

•  *Use contingency table* for binary data  

| Object i / Object j | 1   | 0   | sum   |
|----------------------|-----|-----|-------|
| *1*               | q   | r   | q + r |
| *0*               | s   | t   | s + t |
| *sum*             | q+s | r+t | p     |

---

•  Distance measure for **symmetric** binary variables: 
  $$
  d(i,j) = \frac{r+s}{q+r+s+t}
  $$

•  Distance measure for **asymmetric** binary variables:
$$
d(i,j) = \frac{r+s}{q+r+s}
$$

•  *Jaccard coefficient* (similarity measure for asymmetric binary variables):  
  $$
  sim_{Jaccard}(i,j) = \frac{q}{q+r+s}
  $$

•  *Note*: Jaccard coefficient is the same as coherence:  
  $$
  coherence(i,j) = \frac{sup(i,j)}{sup(i) + sup(j) - sup(i,j)} = \frac{q}{(q+r) + (q+s) - q}
  $$