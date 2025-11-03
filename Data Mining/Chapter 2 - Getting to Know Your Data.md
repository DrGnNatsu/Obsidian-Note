---
tags:
  - data_mining
---
___
## Types of the Data Sets
| Type                              | Description/Examples                                                                                                                       |
| :-------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------- |
| **Record**                        | Relational records, Data matrix (e.g., numerical matrix, crosstabs), Document data (term-frequency vector). (See example table on page 2). |
| **Transaction data**              | Items bought together (e.g., Beer, Bread, Milk). (See example table on page 2).                                                            |
| **Graph and network**             | World Wide Web, Social or information networks.                                                                                            |
| **Molecular Structures**          |                                                                                                                                            |
| **Ordered**                       | Video data (sequence of images), Temporal data (time-series), Sequential Data (transaction sequences), Genetic sequence data.              |
| **Spatial, image and multimedia** | Spatial data (maps), Image data, Video data.                                                                                               |
## Important Characteristics of Structured Data
- **Dimensionality**: Curse of dimensionality.
- **Sparsity**: Only the presence counts matter.
- **Resolution**: Patterns depend on the scale.
- **Distribution**: Centrality and dispersion.
## Data objects
- Data sets are made up of data objects.
- A data object represents an entity.
- **Examples**: students/professors in a university DB.
- Called **samples, examples, instances, data points, objects, and tuples.**
- Attributes describe data objects.
    - Database rows $\rightarrow$ data objects; columns $\rightarrow$ attributes.
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

---
# Basic Statistical Descriptions of Data
- Motivation: To better understand the data: central tendency, variation, and spread.
- Data Dispersion Characteristics:
	- Measures include: median, max, min, quantiles, outliers, variance, etc.
	- Numerical dimensions correspond to sorted intervals.
	- Dispersion was analyzed with multiple granularities of precision (Boxplot or quantile analysis on sorted intervals).
	- Dispersion analysis on computed measures (folding measures into numerical dimensions, Boxplot/quantile analysis on the transformed cube).
- Numerical Dimensions
- Dispersion analysis on computed measures
## Measuring the Central Tendency
**Mean:** The average of the data
$$
\bar{x}= \dfrac{\sum_{i=1}^{n}w_ix_i}{\sum_{i=1}^{n}w_i}
$$
- Trimmed mean: chopping extreme values.
- Population: $\mu = \frac{\sum x_i}{N}$
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
- **Quartiles**: $Q_1$ (25th percentile), $Q_3$ (75th percentile).
- **Inter-quartile range (IQR)**: $IQR = Q_3 - Q_1$.
- **Five number summary**: min (inliers), $Q_1$, median, $Q_3$, max (inliers).
- **Boxplot**: Visual representation using the five-number summary.
 - **Outlier:** The value point is in the range $$x < Q_1 -1.5 \times IQR \quad or \quad x > Q_3+1.5 \times IQR$$
- **Variance ($\sigma^2$) and Standard Deviation ($\sigma$)**:$$\sigma^2 = \frac{1}{N} \sum_{i=1}^{N} (x_i - \bar{x})^2$$
> [!note] Note
Standard deviation $\sigma$ is the square root of variance $\sigma^2$.

- **Min and Max:** the min and max value but it is not outliers (only use to calculate midrange)
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
## Data Matrix and Dissimilarity Matrix
- **Data matrix**: $n$ data points with $p$ dimensions. (Page 17)
- **Dissimilarity matrix**: Triangular matrix registering distances $d(i, j)$. (Page 17)
## Proximity Measure for Nominal Attributes
Can take 2 or more states, e.g., red, yellow, blue, green(generalization of a binary attribute)
$$
d(i,j)=\dfrac{p-m}{p}
$$
m: number of matches, p: total number of variables
## Proximity Measure for Numeric Data
- **Minkowski distance** (L-h norm):
$$d(i, j) = \left( \sum_{k=1}^{p} |x_{ik} - x_{jk}|^h \right)^{1/h}$$
- **Properties (Metric)**: Positive definiteness ($d(i, i) = 0$), Symmetry ($d(i, j) = d(j, i)$), Triangle Inequality ($d(i, j) \le d(i, k) + d(k, j)$).

### Special Cases of Minkowski Distance
- **$h=1$**: Manhattan (City block, $L_1$ norm). (Hamming distance for binary vectors). $d(i,j) = |x_i - x_j| + |y_i + y_j| + \cdots$
- **$h=2$**: Euclidean distance ($L_2$ norm). $d(i,j) = \sqrt{(x_i - x_j)^2+(y_i - y_j)^2 + \cdots}$
- **$h \rightarrow \infty$**: "Supremum" ($L_{\max}$ norm): $\max_f |x_{if} - x_{jf}|$.
## Proximity Measure for Binary Attributes (slides)
*Proximity Measure for Binary Attributes*
•  *Use contingency table* for binary data  

| Object i / Object j | 1   | 0   | sum   |
|----------------------|-----|-----|-------|
| *1*               | q   | r   | q + r |
| *0*               | s   | t   | s + t |
| *sum*             | q+s | r+t | p     |

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
> [!note] Note: Jaccard coefficient is the same as coherence:  
  $$
  coherence(i,j) = \frac{sup(i,j)}{sup(i) + sup(j) - sup(i,j)} = \frac{q}{(q+r) + (q+s) - q}
  $$
  
## Standardizing Numeric Data
Used to compare attributes with different units/scales using the **Z-score**:
$$Z = \frac{x - \mu}{\sigma}$$
An alternative uses **mean absolute deviation** ($S_f$) instead of standard deviation ($\sigma$).
## Ordinal Variables
- Can be treated like interval-scaled variables by replacing values with their **rank** ($r_{if} \in \{1, \ldots, M_f\}$) and normalizing: $Z_{if} = \frac{r_{if} - 1}{M_f - 1}$. 

## Attributes of Mixed Type
A weighted formula can combine effects:
$$d(i, j)= \frac{\sum_f P_f \delta^{(f)}_{ij} d^{(f)}_{ij}}{\sum_f P_f \delta^{(f)}_{ij}}$$
Where $\delta^{(f)}_{ij}$ is 0 if $X_{if} = X_{if}$ (for binary/nominal) or 1 otherwise. Normalization is used for numeric attributes.
## Cosine Similarity
Used for vectors (e.g., term-frequency vectors, documents):
$$\cos(d_1, d_2) = \frac{d_1 \bullet d_2}{||d_1|| \ ||d_2||}$$