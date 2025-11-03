# Chapter 1 - Introduction to Data Mining
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
___
# Chapter 2 - Getting to Know Your Data
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
___
# Measuring Data Similarity and Dissimilarity
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
- **$h=1$**: Manhattan (City block, $L_1$ norm). (Hamming distance for binary vectors). $d(i,j) = |x_i - x_j| + |y_i - y_j| + \cdots$
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
___
# Chapter 3 - Data Preprocessing
# Data Preprocessing: An Overview
- The first phase of the pipeline: how to correct and explore the data
## Data Quality: Why Preprocess the Data?
*Measures for data quality*: A multidimensional view
- **Accuracy**: Correct or wrong, accurate or not.
- **Completeness**: Not recorded, unavailable, ...
- **Consistency**: some modified but some not, dangling, ...
	- One variable can be defined in many ways; you need to make in the same meaning.
- **Timeliness**: Timely update?
- **Believability**: How trustworthy is the data are correct? Is the survey correct, reliable?
- **Interpretability**: How easily can the data be understood?
## Major Tasks in Data Preprocessing
**Data cleaning**: Fill in missing values, smooth noisy data, identify or remove outliers, and resolve inconsistencies
**Data integration**: Integration of multiple databases, data cubes, or files
**Data reduction**: 
- Dimensionality reduction
- Numerosity reduction
- Data compression
**Data transformation and data discretisation:**
- Normalization
- Concept hierarchy generation
___
# Data Cleaning
Data in the Real World is Dirty: Lots of potentially incorrect data, e.g., instrument faulty, human or computer error, transmission error
- *Incomplete*: lacking attribute values, lacking certain attributes of interest, or containing only aggregate data
	- e.g., _Occupation_ = “ ” (missing data)
	- Data is not always available
		- E.g., many tuples have no recorded value for several attributes, such as customer income in sales data
	- Missing data may be due to 
		- Equipment malfunction
		- Inconsistent with other recorded data and thus deleted
		- Data not entered due to a misunderstanding
		- Certain data may not be considered important at the time of entry
		- Not register history or changes to the data
	- Missing data may need to be inferred
- *Noisy*: containing noise, errors, or outliers
	- e.g., _Salary_ = $−10$ (an error)
	- **Noise**: Random error or variance in a measured variable.
	- **Incorrect attribute values** due to: faulty collection instruments, data entry problems, transmission problems, and naming convention inconsistencies.
	- **Other data problems**: Duplicate records, incomplete data, and inconsistent data.
- *Inconsistent:* containing discrepancies in codes or names, e.g.,
	- _Age_ = “42”, _Birthday_ = “03/07/2010”
	- Was rating “1, 2, 3”, now rating “A, B, C”
	- discrepancy between duplicate records
- *Intentional* (e.g., _disguised missing_ data)
	- Jan. 1 as everyone’s birthday
## How to Handle Missing Data?
Ignore the tuple: usually done when the class label is missing (when doing classification)—not effective when the % of the missing values per attribute varies considerably
- Fill in the missing value manually: tedious + infeasible?
- Fill it in automatically with 
	- A global constant: e.g., “unknown”, a new class?!
	- The attribute mean
	- The attribute mean for all samples belonging to the same class: smarter
	- The **most probable value** (inference-based, like Bayesian formula or decision tree) - predict technique.
## How to Handle Noisy Data?
**Binning**: 
- First, sort the data and partition into (equal-frequency) bins
- Then one can smooth by bin means, *smooth by bin median, smooth by bin boundaries*, etc.
**Regression**: smooth by fitting the data into regression functions
- E.g., Linear Regression, Logistic Regression
**Clustering**: detect and remove outliers
- If the value does not belong to any cluster, that is outlier
**Combined computer and human inspection** detects suspicious values and checks by a human (e.g., deals with possible outliers)
## Data Cleaning as a Process
**Data discrepancy detection**:
- Use metadata (e.g., domain, range, dependency, distribution)
- Check field overloading
- Check the uniqueness rule, the consecutive rule and the null rule
- Use commercial tools:
	- Data scrubbing: use simple domain knowledge (e.g., postal code, spell-check) to detect errors and make corrections
	- Data auditing: by analysing data to discover rules and relationships to detect violators (e.g., correlation and clustering to find outliers)
**Data migration and integration**
- Data migration tools: allow transformations to be specified
- ETL (Extraction/Transformation/Loading) tools: allow users to specify transformations through a graphical user interface
**Integration of the two processes**: Iterative and interactive (e.g., Potter’s Wheels)
---
# Data Integration
**Data integration**: Combines data from multiple sources into a coherent store
**Schema integration**: e.g., `A.cust-id = B.cust-#`
- Integrate metadata (the data describes that data) from different sources
**Entity identification problem**:
- Identify real-world entities from multiple data sources, e.g., Bill Clinton = William Clinton.
Detecting and resolving **Data value conflicts**
- For the same real-world entity, attribute values from different sources are different.
- Possible reasons: different representations, different scales, e.g., metric vs. British units.
## Handling Redundancy in Data Integration
Redundant data often occurs when integrating multiple databases
- _Object identification_: The same attribute or object may have different names in different databases
	- E.g., $DOB = Age$
- _Derivable data:_ One attribute may be a “derived” attribute in another table, e.g., annual revenue
Redundant attributes may be able to be detected by _correlation analysis_ and _covariance analysis_.
Careful integration of the data from multiple sources may help reduce/avoid redundancies and
inconsistencies, and improve mining speed and quality.
## Correlation Analysis (Nominal Data)
$\mathcal{X}^2$ **(chi-square) test**
$$
\mathcal{X}^2 = \sum \dfrac{(Obeserved - Expected)^2}{Expected}
$$

The larger the $\mathcal{X}^2$ value, the more likely the variables are related
The cells that contribute the most to the $\mathcal{X}^2$ value are those whose actual count is very different from the expected count
Correlation does not imply causality
- \# of hospitals and \# of car thefts in a city are correlated
- Both are causally linked to the third variable: population
**Correlation coefficient** (also called **Pearson's product moment coefficient**).

$$r_{A,B}=\frac{\sum_{i-1}^n({a_i-\bar{A})(b_i-\bar{B})}}{n{\sigma}_a{\sigma}_b}=\frac{\sum_{i-1}^n(a_ib_i)-n \overline{AB}}{n{\sigma}_a{\sigma}_b}$$

- $n$ is the number of tuples
- $\bar{A}$ and $\bar{B}$ are the respective means of $A$ and $B$
- ${\sigma}_a$ and ${\sigma}_b$ are the respective standard deviation of $A$ and $B$
- $\sum{(a_i, b_i)}$ is the sum of the $AB$ cross product.
If $r_{A,B}>0$, $A$ and $B$ are positively correlated ($A$'s values increase as $B$'s). The higher, the stronger correlation.
$r_{A,B}=0\;\rightarrow$ independent; $r_{A,B}<0\;\rightarrow$ negatively correlated;
## Correlation (viewed as linear relationship)
Correlation measures the linear relationship between objects. To compute correlation, we standardize data objects, A and B, and then take their dot product. 
$$
a'_k=\frac{a_k -\text{mean}(A)}{\text{std(A)}}
$$
$$
b'_k=\frac{b_k -\text{mean}(B)}{\text{std(B)}}
$$
$$\text{correlation(A,B)}={A'}\cdot{B'}$$

## Covariance (Numeric Data)
Covariance is similar to correlation
$$Cov(A, B)=E((A-\bar{A})(B-\bar{B}))=\frac{\sum_{i=1}^n(a_i-A)(b_i-B)}{n}$$
Correlation coefficient $r_{A,B}=\frac{Cov(A,B)}{{\sigma}_A{\sigma}_B}$
- $n$ is the number of tuples
- $\bar{A}$ and $\bar{B}$ are the respective means of $A$ and $B$
- ${\sigma}_a$ and ${\sigma}_b$ are the respective standard deviation of $A$ and $B$
**Positive covariance:** if $Cov_{A,B}>0$, then $A$ and $B$ both tend to be larger than their expected values.
**Negative covariance**:  if $Cov_{A,B}<0$, then if $A$ larger than their expected values, $B$ is likely to be smaller than its expected value.
**Independence:** $Cov_{A,B}=0$ but the converse is not true
	Some pairs of random variables may have a covariance of 0 but are not independent. Only under some additional assumptions (e.g., the data follow multivariate normal distributions) does a covariance of 0 imply independence

---
# Data Reduction
## Data Reduction Strategies
**Data reduction**: Obtain a reduced representation of the data set that is much smaller in volume but yet produces the same (or almost the same) analytical results
*Why data reduction?* — A database/data warehouse may store terabytes of data. Complex data analysis may take a very long time to run on the complete data set.
*Data reduction strategies:*
- Dimensionality reduction, e.g., remove unimportant attributes - remove columns
	- Wavelet transforms
	- Principal Components Analysis (PCA)
	- Feature subset selection, feature creation
- Numerosity reduction (some simply call it: Data Reduction) - remove rows
	- Regression and Log-Linear Models
	- Histograms, clustering, sampling
	- Data cube aggregation
- Data compression
### Data Reduction 1: Dimensionality Reduction
- Curse of dimensionality
	- When dimensionality increases, data becomes increasingly sparse
	- Density and distance between points, which is critical to clustering, outlier analysis, becomes less meaningful
	- The possible combinations of subspaces will grow exponentially
- Dimensionality reduction:
	- *Avoid the curse of dimensionality*
	- Help eliminate irrelevant features and reduce noise
	- Reduce time and space required in data mining
	- Allow easier visualization
- Dimensionality reduction techniques
	- Wavelet transforms
	- Principal Component Analysis: Identify correlation - if the variables are correlated, we transform the data 
	- Supervised and nonlinear techniques (e.g., feature selection) 

## Attribute Subset Selection
Another way to reduce the dimensionality of data
**Redundant attributes:**
- Duplicate much or all of the information contained in one or more other attributes
- E.g., the purchase price of a product and the amount of sales tax paid
**Irrelevant attributes:**
- Contain no information that is useful for the data mining task at hand
- E.g., students' ID is often irrelevant to the task of predicting students' GPA
## Heuristic Search in Attribute Selection
There are $2^d$ possible attribute combinations of $d$ attributes
Typical heuristic attribute selection methods:
- Best single attribute under the attribute independence assumption: choose by significance tests
- Best step-wise feature selection:
	- The best single attribute is picked first
	- Then the next best attribute condition to the first, ...
- Step-wise attribute elimination: Repeatedly eliminate the worst attribute (brute force to find with attribute is unimportant)
- Best combined attribute selection and elimination
- Optimal branch and bound: Use attribute elimination and backtracking
## Attribute Creation (Feature Generation)
Create new attributes (features) that can capture the important information in a data set more effectively than the original ones
Three general methodologies:
- Attribute extraction: Domain-specific
- Mapping data to new space (see: data reduction): E.g., Fourier transformation, wavelet transformation, manifold approaches (not covered)
- Attribute construction
	- Combining features
	- Data discretization
### Data Reduction 2: Numerosity Reduction
Reduce data volume by choosing alternative, _smaller forms_ of data representation
**Parametric methods** (e.g., regression): Assume the data fits some model, estimate the model parameters, store only the parameters, and discard the data (except possible outliers)
- Ex: Log-linear models—obtain value at a point in _m_-D space as the product of the appropriate marginal subspaces
- **Regression and Log-Linear Models**: Model data to fit a straight line ($Y=wX+b$) or approximate discrete distributions.
- **Regression Analysis**: Estimation using the **least squares method**.
**Non-parametric** methods:
- Do not assume models
- Major families: histograms, clustering, sampling, …
#### Clustering
- Partition the data set into clusters based on similarity, and store cluster representation (e.g., centroid and diameter) only
- Can be very effective if the data is clustered, but not if the data is “smeared”
- Can have hierarchical clustering and be stored in multi-dimensional index tree structures
- There are many choices of clustering definitions and clustering algorithms
- Cluster analysis will be studied in depth in Chapter 10
#### Sampling
- Sampling: obtaining a small sample `s` to represent the whole data set `N`
- Allow a mining algorithm to run in complexity that is potentially sub-linear to the size of the data
- Key principle: Choose a *representative* subset of the data
	- Simple random sampling may have very poor performance in the presence of skew
	- Develop adaptive sampling methods: e.g., stratified sampling:
- Note: Sampling may not reduce database I/Os (page at a time)
#### Data Cube Aggregation
- The lowest level is the **base cuboid**.
- Aggregated data can be referenced at multiple levels to further reduce data size. Queries should use the cube when possible.
___
# Data Transformation and Data Discretization
## Data Transformation
A function that maps the entire set of values of a given attribute to a new set of replacement values.
- **Methods**: Smoothing (noise removal), Attribute/feature construction, Aggregation (summarization), **Normalization**, and **Discretization**.
### Normalization
Scaling data to fall within a smaller, specified range.
- **Min-max normalization**: Scales data to $[new_{min}, new_{max}]$.
$$v' = \frac{v - \min_A}{\max_A - \min_A} (\text{new\_max} - \text{new\_min}_A) + \text{new\_min}_A$$
- **Z-score normalization**: Uses $\mu$ (mean) and $\sigma$ (standard deviation): $v' = \frac{v - \mu}{\sigma}$
- **Normalization by decimal scaling**: $v' = v / 10^j$.
### Discretization
Dividing the range of a continuous attribute into intervals (labels replace actual data values).
- **Three types of attributes handled**: Nominal, Ordinal, Numeric (real numbers).
### Data Discretization Methods (Applied Recursively)
- **Binning** (Top-down split, unsupervised).
- **Histogram analysis** (Top-down split, unsupervised).
- **Clustering analysis** (Unsupervised, top-down split or bottom-up merge).
- **Decision-tree analysis** (Supervised, top-down split).
- **Correlation ($\chi^2$) analysis** (Unsupervised, bottom-up merge).
### Concept Hierarchy Generation
Organizes concepts (attribute values) hierarchically.
- Facilitates **drilling and rolling** in data warehouses.
- Formation can be **explicitly specified** by experts or **automatically generated** (For numeric data, use discretization methods).
### Automatic Concept Hierarchy Generation
Hierarchy level is based on the number of distinct values per attribute (fewer distinct values means higher level in hierarchy).
___
# Chapter 4 - Data Mining Knowledge Representation
# Output: representing structural patterns 
- Many different ways of representing patterns 
- Decision trees, rules, instance-based, … 
- Also called “knowledge” representation. 
- Representation determines inference method. 
- Understanding the output is the key to understanding the underlying learning methods. 
- Different types of output for different learning problems (e.g., classification, regression, …)
___
# Tables 
Simplest way of representing output:  Use the same format as input!
*Main problem:* selecting the right attributes
___
# Linear models 
- Another simple representation 
- Regression model: Inputs (attribute values) and output are all numeric 
	- $Y = w_1X_1 + w_2X_2 + \dots+ w_nX_n$
- Output is the sum of weighted attribute values: The *trick* is to find good values for the weights.
## Linear Models for Classification
- **Regression model**.
	- Inputs (attribute values) and output are all **numeric**.
- Output is the sum of weighted attribute values.
	- The trick is to find good values for the weights.
- Binary classification 
- Line separates the two classes: Decision boundary - defines where the decision changes from one class value to the other.
- Prediction is made by plugging in observed values of the attributes into the expression: Predict one class if $output \geq 0$, and the other class if $output < 0$ 
- The boundary becomes a high-dimensional plane (*hyperplane*) when there are multiple attributes.
---
# Trees 
- *“Divide-and-conquer”* approach produces a tree. 
- Nodes involve testing a particular attribute. 
	- $Node = attribute$
	- $Edge = value$
	- Label
- Usually, an attribute value is compared to a constant.
- Other possibilities: 
	- Comparing values of two attributes 
	- Using a function of one or more attributes 
- Leaves assign classification, a set of classifications, or a probability distribution to instances. 
- Unknown instance is routed down the tree.
## Nominal and Numeric Attributes
- Nominal: 
	- The number of children is usually equal to the number of values ⇒ attribute won’t get tested more than once. 
	- Another possibility: division into many different subsets
	- Ex: Age: 1 → 100, we can categorise it into three subsets: 1 → 30, 31 → 60, 61 → 100
- Numeric: 
	- Test whether the value is greater or less than a constant ⇒ attribute may get tested several times.
	- Other possibility: three-way split (or multi-way split) 
		- Integer: less than, equal to, greater than 
		- Real: below, within, above
## Missing values
Does the absence of value have some significance? 
	- Yes: “missing” is a separate value. 
	- No:  “missing” must be treated specially.
- **Solution A**: Assign instance to the most popular branch.
- **Solution B**: Split the instance into pieces, receiving weight according to the fraction of training instances that go down each branch.
- Classifications from leave nodes are combined using the weights that have percolated to them.
## Trees for Numeric Predictions
- Regression: the process of computing an expression that predicts a numeric quantity
- Regression tree: “decision tree” where each leaf predicts a numeric quantity
	- Predicted value is the average value of training instances that reach the leaf 
- Model tree: “regression tree” with linear regression models at the leaf nodes 
	- Linear patches approximate a continuous function
---
# Rules 
## Classification rules 
- Popular alternative to decision trees 
- Antecedent (pre-condition): a series of tests (just like the tests at the nodes of a decision tree) 
- Tests are usually logically ==AND (logical operand)== together (but may also be general logical expressions) 
- Consequent (conclusion): classes, set of classes, or probability distribution assigned by rule 
- Individual rules are often logically ==OR (logical operand)== together 
- Conflicts arise if different conclusions apply
==Example==: Based on many attributes, we can assign it to the group
### From trees to rules
- **Easy:** converting a tree into a set of rules 
- One rule for each leaf: 
	- An antecedent contains a condition for every node on the path from the root to the leaf
	- Consequent is the class assigned by the leaf 
- Produces unambiguous rules 
- Doesn’t matter in which order they are executed

- **Difficult**: transforming a rule set into a tree 
- A tree cannot easily express the disjunction between rules 
- Example: rules that test different attributes 
```
If a and b, then x 
If c and d, then x
```
- Symmetry needs to be broken 
- Corresponding tree contains identical subtrees ⇒ “replicated subtree problem”
### Interpreting rules
- What if two or more rules conflict? 
	- Give no conclusion at all? 
	- Go with the rule that is most popular on the training data? 
- What if no rule applies to a test instance? 
	- Give no conclusion at all? 
	- Go with the class that is most frequent in the training data?
### Special case: boolean class 
- Assumption: if an instance does not belong to class “yes”, it belongs to class “no” 
- Trick: only learn rules for class “yes” and use the default rule for “no” 
- The order of the rules is not important. No conflicts! 
- Rule can be written in disjunctive normal form
## Association rules 
- Association rules:
	- can predict any attribute and combinations of attributes 
	- are not intended to be used together as a set 
- Problem: an immense number of possible associations 
- Output needs to be restricted to show only the most predictive associations ⇒ only those with high support and high confidence
### Support and confidence in a rule
**Support**: number of instances predicted correctly 
**Confidence**: number of correct predictions, as a proportion of all instances to the rule applies 
Example: 4 cool days with normal humidity
	Support = 4, confidence = 100% 
Normally: minimum support and confidence prespecified (e.g., 58 rules with $support \geq 2$ and $confidence \geq 95\%$ for weather data)

# Rules with exceptions 
Allows rules to have exceptions (e.g., `... THEN Class A EXCEPT if condition THEN Class B`).
## Advantages of Using Exception
- Rules can be updated incrementally:
	- Easy to incorporate new data 
	- Easy to incorporate domain knowledge 
- People often think in terms of exceptions 
- Each conclusion can be considered just in the context of the rules and exceptions that lead to it:
	- Locality property is important for understanding large rule sets
	- **Normal** rule sets don’t offer this advantage
# More expressive rules 
- But exceptions offer a psychological advantage 
	- Assumption: defaults and tests early on apply more widely than exceptions further down
	- Exceptions reflect special cases
## Rules Involving Relations
- So far: all rules involved comparing an attribute-value to a constant (e.g., temperature < 45)
- These rules are called “propositional” because they have the same expressive power as propositional logic
- What if the problem involves relationships between attributes 
	- It can’t be expressed with propositional rules 
	- More expressive representation required
## A relational solution
Comparing attributes with each other 
Generalizes better to new data 
Standard relations: =, <, > 
But: learning relational rules is costly 
Simple solution: add extra attributes (e.g., a binary attribute is width < height?)
# Instance-based representation 
- Simplest form of learning: rote learning 
	- *Training instances are searched for an instance that most closely resembles the new instance*
	- The instances themselves represent the knowledge 
	- Also called instance-based learning 
- Similarity function defines what’s “learned” 
- Instance-based learning is **lazy learning**.
- Methods: nearest-neighbor, k-nearest-neighbor, …
## The Distance Function
- Simplest case: one numeric attribute:
	- Distance is the difference between the two attribute values involved (or a function thereof) 
- Several numeric attributes: normally, Euclidean distance is used, and attributes are normalized 
- Nominal attributes: distance is set to 1 if values are different, 0 if they are equal
- Are all attributes equally important? *Weighting* the attributes might be necessary
## Learning Prototypes
- Only those instances involved in a decision need to be stored 
- Noisy instances should be filtered out 
- Idea: only use prototypical examples
## Rectangular generalizations
- Nearest-neighbor rule is used outside rectangles 
- Rectangles are rules! (But they can be more conservative than “normal” rules.) 
- Nested rectangles are rules with exceptions
# Clusters
- Partition the data set into clusters based on **similarity**.
- Store cluster representation (e.g., centroid and diameter).
- **Representing Clusters I**: Simple 2-D representation vs. Venn diagram.
- **Representing Clusters II**: Probabilistic assignment vs. Dendrogram (hierarchical clustering structure)
___
# Chapter 5 - Evaluating what’s been learned
# Evaluation: the key to success 
> How predictive is the model we learned? 
- Error on training data **isn’t a good indicator** of performance on future data.
	- Otherwise, 1-NN would be the optimum classifier! 
- **Simple solution (if labeled data is abundant)**: Split data into training and test sets.
- **Limitation**: Labeled data is usually limited, necessitating more sophisticated techniques
---
# Issues: training and testing 
- Statistical *reliability* of estimated differences in performance (→  significance tests) 
- Choice of performance measure: 
	- Number of correct classifications 
	- Accuracy of probability estimates 
	- Error in numeric predictions 
- Costs assigned to different types of errors 
	- Many practical applications involve costs.
## Training and testing
- Natural performance measure for classification problems: error rate 
	- **Success:** instance’s class is predicted correctly 
	- **Error:** instance’s class is predicted incorrectly 
	- **Error rate:** proportion of errors made over the whole set of instances 
	- **Resubstitution error**: Error rate obtained from the *training* data.
- Test set: independent instances that have *played no part in the formation of the classifier*
	- Assumption: both training data and test data are representative samples of the underlying problem
- Training set: 
	- Must cover the cases in the data.
- Test and training data may differ in nature
	- Example: classifiers built using customer data from two different towns, A and B 
		- To estimate the performance of the classifier from town A in a completely new town, test it on data from
## Making the most of the data
- Once the evaluation is complete (choosing the best model), all the data can be used to build the final classifier. 
- Generally, the larger the training data, the better the classifier 
- The larger the test data, the more accurate the error estimate 
- Holdout procedure: a method of splitting the original data into a training and a test set 
	- Dilemma: ideally, both the training set and test set should be large!
# Predicting performance: confidence limits 
___
- Assume the estimated error rate is 25%. How close is this to the true error rate? 
	- Depends on the amount of test data 
- Prediction is just like tossing a (biased!) coin.
	- “Head” is a “success”, “tail” is an “error” 
- In statistics, a succession of independent events like this is called a **Bernoulli process**.
	- Statistical theory provides us with **confidence intervals** for the true underlying proportion.
## Confidence intervals
- We can say: $p$ lies within a certain specified interval with a certain specified confidence.
	- Example: $S=750$ successes in $N=1000$ trials 
		- Estimated success rate: $75\%$
		- How close is this to the true success rate p? 
			- Answer: with $80\%$ confidence $p$ in $[73.2,76.7]$ 
	- Another example: $S=75$ and $N=100$ 
		- Estimated success rate: $75\%$
		- With $80\%$ confidence $p$ in $[69.1,80.1]$
## Mean and Variance
- Mean and variance for a Bernoulli trial: $p, p (1–p)$ 
- Expected success rate $f=\dfrac{S}{N}$ 
- Mean and variance for f : $p, p (1–p)/N$ 
- For large enough $N, f$ follows a Normal distribution 
- $c\%$ confidence interval $[–z \leq X \leq z]$ for random variable with 0 mean is given by: 
$$Pr[–z \leq X \leq z]=c$$
- With a symmetric distribution:
$$Pr[–z \leq X \leq z]=1 - 2 *Pr[x \geq z]$$
## Confidents limits
Confidence limits for the normal distribution with 0 mean and a variance of 1:
## Transforming f
Transformed value for f : $\Pr\left[ -z < \frac{f - p}{\sqrt{p(1 - p)/N}} < z \right] = c$

(i.e., subtract the mean and divide by the standard deviation) 
Resulting equation: 
Solving for p : $p = \left( f + \frac{z^2}{2N} \pm z \sqrt{ \frac{f}{N} - \frac{f^2}{N} + \frac{z^2}{4N^2} } \right) \Big/ \left( 1 + \frac{z^2}{N} \right)$

___
# Holdout, cross-validation, bootstrap 
## Holdout
### Holdout estimation
> What to do if the amount of data is limited? 
- The holdout method reserves a certain amount for testing and uses the remainder for training (typically 1/3 test, 2/3 train).
- Problem: the samples might not be representative 
	- Example: class might be missing in the test data 
- Advanced version uses *stratification*
	- Ensures that each class is represented with approximately equal proportions in both subsets
### Repeated holdout method
- Holdout estimate can be made more reliable by repeating the process with different subsamples 
	- In each iteration, a certain proportion is randomly selected for training (possibly with stratification) 
	- The error rates on the different iterations are averaged to yield an overall error rate
- This is called the repeated holdout method 
- Still not optimum: the different test sets overlap. Can we prevent overlapping?
## Cross Validation
- Cross-validation avoids overlapping test sets 
	- First step: split data into k subsets of equal size 
	- Second step: use each subset in turn for testing, the remainder for training
- Called *k-fold cross-validation*  = divide into `k` part using `1` part for testing, rest for training
	- Normally, People use $k=5$
- Often, the subsets are stratified before the cross-validation is performed 
- The error estimates are averaged to yield an overall error estimate
### Leave-One-Out Cross-Validation
- Leave-One-Out: a particular form of cross-validation: 
	- Set the number of folds to the number of training instances 
	- I.e., for n training instances, build a classifier n times
- Makes the best use of data, involves no random subsampling, but is **very computationally expensive** (except for NN).
- **Cons**: Stratification is not possible as the test set contains only one instance.(exception: NN)
## Bootstrap
- CV uses sampling without replacement 
	- The same instance, once selected, can't be selected again for a particular training/test set 
- The bootstrap uses sampling with replacement to form the training set 
	- Sample a dataset of `n` instances replace `n` times  to form a new dataset of `n` instances 
	- Use this data as the training set 
	- Use the instances from original dataset that don’t occur in the new training set for testing
### The 0.632 bootstrap
- Also called the 0.632 bootstrap 
	- A particular instance has a probability of $1– \dfrac{1}{n}$ of not being picked 
	- Probability of being in the test set is $1 - (1 - 1/n)^n \approx 1 - e^{-1} \approx 0.368$.
	- Training data contains approximately $63.2\%$ of the instances.
	- **Estimated Error**: $\text{err} = 0.632 \times e_{\text{test}} + 0.368 \times e_{\text{training}}$. 
	- This means the training data will contain approximately $63.2\%$ of the instances
#### More on the Bootstrap
- Probably the best way to estimate performance for **very small datasets**.
- **Problem**: A perfect memorizer yields $0\%$ resubstitution error but $\sim 50\%$ error on the test set, leading to a bootstrap estimate of $31.6\%$ error (when true expected error is $50\%$).
___
# Comparing schemes: the t-test 
- Frequent question: which of two learning schemes performs better? 
- Note: this is domain dependent! 
- Obvious way: compare 10-fold CV estimates
- Generally sufficient in applications (we don't loose if the chosen method is not truly better)
- However, what about machine learning research? 
	- Need to show convincingly that a particular method works better
- Want to show that scheme A is better than scheme B in a particular domain 
	- For a given amount of training data 
	- On average, across all possible training sets 
- Let's assume we have an infinite amount of data from the domain:
	- Sample infinitely many dataset of specified size 
	- Obtain cross-validation estimate on each dataset for each scheme 
	- Check if mean accuracy for scheme A is better than mean accuracy for scheme B
## Summary of Some Measures
| Domain | Plot | Explanation |
| :--- | :--- | :--- |
| Lift chart | Marketing | TP Subset size vs TP (fraction of relevant records found) |
| ROC curve | Communications | TP rate vs FP rate |
| Recall-precision curve | Information retrieval | Recall vs Precision |
## Evaluating Numeric Prediction
- Same strategies apply: independent test set, cross-validation, significance tests.
- **Difference**: Error measures.
- Actual targets: $a_1, a_2, \ldots, a_n$. Predicted targets: $p_1, p_2, \ldots, p_n$. 
- Most popular measure: **Mean-squared error (MSE)**.
$$\text{MSE} = \frac{\sum_{i=1}^{n} (p_i - a_i)^2}{n}$$
- Easy to manipulate mathematically.
### Other Measures (Numeric)
- **Root mean-squared error (RMSE)**. $\text{RMSE} = \sqrt{\frac{(p_1 - a_1)^2 + (p_2 - a_2)^2 + \ldots + (p_n - a_n)^2}{n}}$
- **Mean absolute error (MAE)**: $\text{MAE} = \frac{|p_1 - a_1| + |p_2 - a_2| + \ldots + |p_n - a_n|}{n}$
	- Less sensitive to outliers than MSE.
- **Relative error values** (e.g., $10\%$ error when predicting $500$).
### Improvement on the Mean
Measures how much the scheme improves compared to simply predicting the average ($\bar{a}$).
- **Relative squared error**: $\frac{\sum(p_i - a_i)^2}{\sum(\bar{a} - a_i)^2}$
- **Relative absolute error**: $\frac{\sum|p_i - a_i|}{\sum|\bar{a} - a_i|}$
### Correlation Coefficient (Numeric Prediction)
Measures statistical correlation ($r_{PA}$) between predicted ($p$) and actual ($a$) values. Performance leads to large positive values.

___
# Predicting probabilities: loss functions 
- Performance measure so far: success rate 
- Also called 0-1 loss function: 
- Most classifiers produces class probabilities 
- Depending on the application, we might want to check the accuracy of the probability estimates 
- 0-1 loss is not the right thing to use in those cases
## Quadratic Loss Function
$$ \text{Quadratic loss} = \sum_j (p_j - a_j)^2 = 1 - 2p_c + \sum_j p_j^2 $$
Minimized when $p_j = p_j^*$ (the true probabilities).
## Informational Loss Function
$$-\log(p_c)$$
- Where $p_c$ is the probability of the true class. Represents the number of bits required to communicate the class.
- Minimized when $p_j = p_j^*$.
- **Difficulty**: Zero-frequency problem.
## Discussion on Loss Functions
- Quadratic loss accounts for all class estimates; Informational loss focuses only on the actual class probability.
- Quadratic loss is bounded (never exceeds 2).
- Informational loss can be infinite.
- Informational loss is related to the **MDL principle**.
---
# Cost-sensitive measures 
- In practice, different types of classification errors often incur different costs
- Examples: 
	- Loan decisions
	- Oil-slick detection 
	- Fault diagnosis 
	- Promotional mailing
- The confusion matrix:

|                  | **Yes** | **No**  | **Predicted Class** |
| ---------------- | --- | --- | --------------- |
| **Yes**          | TP  | FP  |                 |
| **No**           | FN  | TN  |                 |
| **Actual Class** |     |     |                 |
- Can take costs into account when making predictions, especially when errors have different impacts. 
- **Basic Idea**: Only predict a high-cost class when very confident. 
- **Expected Cost**: Calculated by the dot product of the vector of class probabilities and the appropriate column in the cost matrix. 
- **Goal**: Choose the column (class) that minimizes the expected cost.
## Summary of some measures

| **Measure**                | **Domain**            | **Plot**          | **Explanation**                            |
| -------------------------- | --------------------- | ----------------- | ------------------------------------------ |
| **Lift chart**             | Marketing             | TP, Subset size   | $\frac{TP}{(TP + FP)/(TP + TN + FN)}$      |
| **ROC curve**              | Communications        | TP rate, FP rate  | $\frac{TP}{TP + FN}$, $\frac{FP}{FP + TN}$ |
| **Recall–precision curve** | Information retrieval | Recall, Precision | $\frac{TP}{TP + FN}$, $\frac{TP}{TP + FP}$ |
## Kappa Statistic
The Kappa statistic ($\kappa$) is used to measure the agreement between two classifications (or prediction schemes) relative to agreement achieved by random chance.
**Application**: Comparing two confusion matrices for a $k$-class problem: one showing actual vs. predicted by the learning scheme ($D_{\text{observed}}$), and one showing prediction by a random classifier ($D_{\text{random}}$).
### Calculation Steps (For $k$ classes)
1.  **Calculate $D_{\text{observed}}$ (Sum of entries on the diagonal of the observed matrix):**
    $$D_{\text{observed}} = \sum_{i} \text{Count}(C_i, C_i)$$
    (Where $C_i$ is the actual class matching the predicted class $i$).
2.  **Calculate $D_{\text{random}}$ (Sum of entries expected by chance):**
    This is calculated by multiplying the row totals by the column totals for each cell and summing these products, divided by the total number of instances.
3.  **Calculate $D_{\text{perfect}}$ (Maximum possible sum of diagonal entries):**
    This is the sum of the minimum of the row total and the column total for each class.
4.  **Kappa Statistic Formula:**
$$\kappa = \frac{D_{\text{observed}} - D_{\text{random}}}{D_{\text{perfect}} - D_{\text{random}}}$$

**Interpretation**: Kappa measures the relative improvement over a random predictor. A value of 1 indicates perfect agreement, 0 indicates agreement no better than random chance.


---
# The Minimum Description Length principle
MDL stands for **minimum description length**.
Description length ($L$):
$$L = \text{space required to describe a theory} + \text{space required to describe the theory's mistakes}$$
- Aim: Seek a classifier with minimal DL.
- MDL principle is a **model selection criterion**.
## Model Selection Criteria
- Attempt to find a compromise between model complexity and prediction accuracy on the training data.
- Also known as **Occam's Razor**: the best theory is the smallest one that describes all the facts.
## MDL and Compression
- MDL principle relates to data compression: the best theory compresses the data the most.
- We need to compute: (a) size of the model, and (b) space needed to encode the errors (using informational loss function for this).
## MDL and MAP
- **MAP** (maximum a posteriori probability) finding the best theory corresponds to finding the MDL theory.
- The difficult part of MAP is determining the prior probability $\text{Pr}[T]$, which corresponds to the coding scheme for the theory in MDL.
___
# Chapter 6&7 - Mining Algorithms - Classification

# Supervised vs. Unsupervised Learning

## Supervised learning (classification)
- **Supervision**: The training data, such as observations or measurements, are accompanied by **labels** indicating the classes to which they belong.
- New data is classified based on the models built from the training set.
(See image on page 2 for an example of Training $\rightarrow$ Model Learning $\rightarrow$ Prediction)
## Unsupervised learning (clustering)
- The class labels of the training data are **unknown**.
- Given a set of observations or measurements, establish the possible existence of classes or clusters in the data.
___
# Prediction Problems: Classification vs. Numeric Prediction

## Classification
- Predict **categorical** class labels (discrete or nominal).
- Construct a model based on the training set and the class labels (the values in a classifying attribute) and use it in classifying new data.
## Numeric prediction
- Model **continuous-valued functions** (i.e., predict unknown or missing values).
___
# Classification—Model Construction, Validation, and Testing
## Model Construction and Training
- **Model**: Represented as decision trees, rules, mathematical formulas, or other forms.
- **Assumption**: Each sample belongs to a predefined class/class label.
- **Training Set**: The set of samples used for model construction.
## Model Validation and Testing
- **Test**: Estimate the accuracy of the model.
    - The known label of the test sample versus the classified result from the model.
    - **Accuracy**: $\%$ oO test set samples that are correctly classified by the model.
    - The test set is **independent** of the training set.
- **Validation**: If the test set is used to select or refine models, it is called a validation (or development) test) set.
- **Model Deployment**: If the accuracy is acceptable, use the model to classify new data.
___
# Decision Tree Induction: An Example
- Training data set: `Buys_computer`
- Resulting tree structure. (See image on page 5 for the full decision tree diagram.)
## Algorithm for Decision Tree Induction
- Basic algorithm (a **greedy algorithm**).
	- The tree is constructed in a **top-down recursive divide-and-conquer manner**.
		- Divide into many subsets.
		- Recursive do it until all instances belong to one class.
	- At the **start**, all the training examples are at the **root**. (Best attribute is using as root - It splits the dataset into many subsets, which is as pure as possible).
	- Attributes are categorical (if continuous-valued, they are discretized in advance).
	- Examples are partitioned recursively based on the selected attributes.
	- Test attributes are selected on the basis of a heuristic or statistical measure (e.g., **information gain, Gini index**).
### Conditions for stopping partitioning
- All samples for a given node belong to the same class.
- There are no remaining attributes for further partitioning $\rightarrow$ **Majority voting** is employed for classifying the leaf.
- There are no samples left.
### Prediction:
Majority voting is employed for classifying the leaf.
## How to Handle Continuous-Valued Attributes?
1. **Method 1**: Discretize continuous values and treat them as categorical values (e.g., age bins).
2. **Method 2**: Determine the **best split point** for a continuous-valued attribute $A$.
    - Sort the value $A$ in increasing order.
    - Possible split point: $\frac{a_i + a_{i+1}}{2}$ (midpoint).
    - The point with the **minimum expected information requirement** for $A$ is selected as the split-point for $A$.
    - **Split**: Based on split point $P$: tuples in $D$ satisfying $A \le P$ vs. those with $A > P$.
## Pro's and Con's of Decision Trees

### Pro's
- Easy to explain (even for non-expert).
- Easy to implement (many software).
- Efficient.
- Can tolerant missing data.
- **White box**.
- No need to normalize data.
- **Non-parametric**: No assumption on data distribution, no assumption on attribute independency.
- Can work on various attribute types.
### Con's
- **Unstable**: Sensitive to noise.
	- If the data has too much noisy, you should preprocess (clean up) dataset.
- Accuracy may be not good enough (depending on your data).
- The optimal splitting is NP. Greedy algorithms are used.
- **Overfitting**.
## Brief Review of Entropy
- **Entropy (Information Theory):** A measure of uncertainty associated with a random variable.
	- *Calculation:* A discrete random variable Y taking `m` distinct values `{y_1, ..., y_m}`:$\text{The} \log \text{is base} \ 2$. $$H(Y) = -\sum_{i=1}^{m} p_i \log(p_i) \ \text{where } p_i = P(Y=y_i)$$
	- *Interpretation:* 
		- Higher entropy $\geq$ higher uncertainty. 
		- Lower entropy $\geq$ lower uncertainty. 
- **Conditional Entropy:** $$ H(Y|X) = \sum_{x} p(x) H(Y|X=x) $$
## Attribute Selection Measure: Information Gain (ID3/C4.5)
- Select the **attribute with the highest information gain**.
- Let $p_i$ be the probability that arbitrary tuple in $D$ belongs to class $C_i$ estimated by $\frac{|C_{i,D}|}{|D|}$ 
- Expected information (entropy) needed to classify a tuple in $D$: $\text{The} \log \text{is base} \ 2$. 
$$
Info(D) = - \sum_{i=1}^{m} p_i \log_2(p_i)
$$
- Information needed (after using attribute $A$ to split $D$ into $\nu$ partitions): $info(D_j)$ is using the previous formula - but only one subset that means remove the sums.
$$
Info_A(D) = \sum_{j=1}^{\nu} \frac{|D_j|}{|D|} \times Info(D_j)
$$
- Information gained by branching on attribute $A$:
	- If the value is the largest, that is the bets to become the split point
$$
Gain(A) = Info(D) – Info_A(D)
$$
(See image on page 10 for an example calculation of Gain(age)).
## Computing Information-Gain for Continuous-Valued Attributes
- Let attribute A be a continuous-valued attribute:
- Must determine the _best split point_ for A.
	- Sort the value A in increasing order
	- Typically, the midpoint between each pair of adjacent values is considered as a possible _split point_: $(a_i+a_{i+1}):2$ is the midpoint between the values of $a_i$ and $a_{i+1}$.
	- The point with the _minimum expected information_ _requirement_ for A is selected as the split-point for A
- Split:
	- D1 is the set of tuples in D satisfying A ≤ split-point, and D2 is the set of tuples in D satisfying A > split-point
## Gain Ratio for Attribute Selection (C4.5)
- Information gain measure is biased towards attributes with a large number of values. C4.5 uses **gain ratio** to overcome the problem.
	- $v$ is the number of value in $D$.
$$
SplitInfo_A(D) = - \sum_{j=1}^{\nu} \frac{|D_j|}{|D|} \times \log_2\left(\frac{|D_j|}{|D|}\right)
$$
$$
GainRatio(A) = Gain(A) / SplitInfo(A)
$$
- The attribute with the maximum gain ratio is selected as the splitting attribute.
## Gini Index (CART, IBM IntelligentMiner)
- Gini index for a data set $D$:
$$
gini(D) = 1 - \sum_{j=1}^{n} p_j^2
$$
- If $D$ is split on $A$ into $D_1$ and $D_2$:
$$
gini_A(D) = \frac{|D_1|}{|D|} gini(D_1) + \frac{|D_2|}{|D|} gini(D_2)
$$
- **Reduction in Impurity**: $\Delta gini(A) = gini(D) - gini_A(D)$.
- The attribute providing the **smallest $gini_{split}(D)$** (or the largest reduction in impurity) is chosen to split the node.
## Comparing Attribute Selection Measures

| Measure              | Bias/Tendency                                                                 |
| :------------------- | :---------------------------------------------------------------------------- |
| **Information gain** | Biased towards multivalued attributes.                                        |
| **Gain ratio**       | Tends to prefer unbalanced splits.                                            |
| **Gini index**       | Biased to multivalued attributes; has difficulty when \# of classes is large. |
## Overfitting and Tree Pruning
- **Overfitting**: An induced tree may overfit the training data (too many branches reflect anomalies due to noise/outliers).
	- Too many branches
	- Poor accuracy
- **Two approaches to avoid overfitting**:
    1. **Prepruning**: Halt tree construction early if the goodness measure falls below a threshold.
	    1. Hard to choose appropriate threshold.
    2. **Postpruning**: Remove branches from a "fully grown" tree (not necessary branches or tree), and progressively prune trees.
	    1. Use a set of data different from the training data to decide which is the best “purned tree”
## Enhancements to Basic Decision Tree Induction
- Allow for **continuous-valued attributes**: Define new discrete value.
- **Handle missing attribute values**: Assign the most common value or assign a probability. (some models can not handle this part).
- **Attribute construction**: Create new attributes based on existing ones, reducing fragmentation, repetition, ...
## Hoeffding tree (incremental learning)
- **Very Fast Decision Tree (VFDT)** for streaming data - update the tree with the new data input (does not need to retrain all the data).
- Uses a **confidence interval** ($\epsilon$) for entropy estimation at a node:
	- $R$ is the range of the random variable,
	- $\delta$ is the desired probability of the estimate not being within $\epsilon$ of its expected value
	- $n$ is the number of examples collected at the node.
	- The entropy is in the range $[0,…,\log_nc]$ for $n_c$ class values.
$$
\epsilon = \sqrt{\frac{R^2 \ln 1/\delta}{2n}}
$$
___
# Bayes Classification Methods

## Bayes' Theorem: Basics
- **Total probability Theorem**:
$$
p(B) = \sum_{i=1}^{k} p(B|A_i)p(A_i)
$$
- **Bayes' Theorem**:
$$
p(H|X) = \frac{p(X|H)P(H)}{p(X)} \propto p(X|H)P(H)
$$

    - $P(H|X)$: **posteriori probability** (What we should choose)
    - $P(X|H)$: **likelihood** (What we just see)
    - $P(H)$: **prior probability** (What we knew previously)
    - $\propto$: Tỉ lệ thuận 
Classification: Derive the *maximum posteriori*.
## Naive Bayes Classifier
- **Simplified assumption**: Attributes are **conditionally independent** given the class.
$$
P(X|C_i) = \prod_{k=1}^{n} P(x_k|C_i)
$$
- This greatly reduces the computation cost. (only work for nominal or discrete value)
### Handling Continuous Attributes in Naive Bayes
- If attribute $A_k$ is **continuous-valued**, $P(x_k|C_i)$ is usually computed based on **Gaussian distribution** with mean $\mu$ and standard deviation $\sigma$.
$$
g(x, \mu, \sigma) = \frac{1}{\sqrt{2\pi}\sigma} e^{-\frac{(x-\mu)^2}{2\sigma^2}}
$$
### Avoiding the Zero-Probability Problem
- Naïve Bayesian prediction requires each conditional prob. be **non-zero**.
- Use **Laplacian correction (or Laplacian estimator)**:

$$

P(w_k|c) = \frac{count(w_k, c) + 1}{\sum_{w \in V} (count(w, c) + 1)} = \frac{count(w_k, c) + 1}{count(c) + |V|}

$$

where $|V|$ is the number of possible values for the attribute.
## Pros and Cons
***Strength:***
- Performance: A _naïve Bayesian classifier_, has comparable performance with decision tree and selected neural network classifiers
- Incremental: Each training example can incrementally increase/decrease the probability that a hypothesis is correct—prior knowledge can be combined with observed data
***Weakness:***
- Assumption: attributes conditional independence, therefore loss of accuracy.
	- E.g., Patient’s Profile: (age, family history),
	- Patient’s Symptoms: (fever, cough),
	- Patient’s Disease: (lung cancer, diabetes).
	- Dependencies among these cannot be modeled by Naïve Bayes Classifier
____
# Rule-based Classification
## Using IF-THEN Rules for Classification
- Knowledge represented as: **IF (antecedent/precondition) THEN (rule consequent)**.
- Assessment of a rule $R$:
    - **coverage**$(R) = n_{covers} / |D|$
    - **accuracy**$(R) = n_{correct} / n_{covers}$
- **Conflict Resolution** (if multiple rules trigger):
    - **Size ordering**: Highest priority to rules with the "toughest" requirement.
    - **Class-based ordering**: Rules for the most prevalent class come first.
    - **Rule-based ordering** (decision list): Long priority list.
## Rule Extraction from a Decision Tree
- One rule is created for each path from the root to a leaf.
- Rules are easier to understand than large trees.
- Each attribute-value pair along a path forms a conjunction: the leaf holds the class prediction.
## Rule Induction: Sequential Covering Method
- Extracts rules directly from training data.
- **Steps**: Rules are learned one at a time; covered tuples are removed; repeat until termination condition.
## How to Learn-One-Rule?
- Start with the most general rule (condition = empty).
- Use a **greedy depth-first strategy**, picking the one that most improves the rule quality.
- **Rule-Quality measures**: FOIL-gain and FOIL-Prune.
____
# Model Evaluation and Selection
## Evaluation Metrics
- Use **validation test set** of class-labeled tuples instead of training set when assessing accuracy.
- Methods for estimating accuracy: Holdout, Random Subsampling, Cross-validation, Bootstrap.
### Classifier Evaluation Metrics: Confusion Matrix
The matrix shows: Actual Class vs. Predicted Class.

| Actual class/Predicted class | $C_1$                | $\sim C_1$           |     |
| :--------------------------- | :------------------- | :------------------- | --- |
| $C_1$                        | True Positives (TP)  | False Negatives (FN) | P   |
| $\sim C_1$                   | False Positives (FP) | True Negatives (TN)  | N   |
### Accuracy, Error Rate, Sensitivity and Specificity
- **Accuracy** $= (\text{TP} + \text{TN}) / \text{All}$
- **Error rate** $= 1 - \text{Accuracy} = (\text{FP} + \text{FN}) / \text{All}$
- **Sensitivity** (True Positive recognition rate) $= \text{TP} / P$ (where $P$ is total actual positives)
- **Specificity** (True Negative recognition rate) $= \text{TN} / N$ (where $N$ is total actual negatives)
### Class Imbalance Problem
- Occurs when one class is rare (minority class). Sensitivity and Specificity become important.
### Precision and Recall, and F-measures
- **Precision** (Exactness): $\text{Precision} = \frac{\text{TP}}{\text{TP} + \text{FP}}$
- **Recall** (Completeness): $\text{Recall} = \frac{\text{TP}}{\text{TP} + \text{FN}}$
- **F measure** ($F_\beta$ score): Harmonic mean of precision and recall.
$$
F = \frac{2 \times \text{precision} \times \text{recall}}{ \text{precision} + \text{recall}}
$$
$$
F_\beta = \frac{(1+\beta^2) \times \text{precision} \times \text{recall}}{(\beta^2 \times \text{precision}) + \text{recall}}
$$
## Classifier Evaluation Techniques
### Holdout Method
- Data randomly partitioned into **Training Set** (e.g., 2/3) and **Test Set** (e.g., 1/3).
- **Repeated random sub-sampling validation**: Repeat holdout $k$ times; accuracy is the average.
### Cross-Validation
- **$k$-fold** (k=10 is popular): Data partitioned into $k$ subsets; each subset is used once as the test set, others as training set.
- **Leave-one-out**: $k$ equals the number of tuples.
- ***Stratified cross-validation***: Folds are stratified to maintain class distribution.
### Model Selection: ROC Curves
- **ROC Curve**: Shows the trade-off between the **True Positive Rate (TP/P)** (Y-axis) and the **False Positive Rate (FP/N)** (X-axis).
- **AUC (Area Under Curve)**: A measure of accuracy. Closer to 1.0 is better; closer to 0.5 (diagonal line) means less accurate.
### Evaluating Classifier Accuracy: Bootstrap
- Works well with **small data sets**.
- Samples training tuples **uniformly with replacement**.
- **0.632 bootstrap**: Uses 63.2% of data as training and the remaining 36.8% as the test set.
## Issues Affecting Model Selection
- **Accuracy**: Predicting class label.
- **Speed**: Training time, prediction time.
- **Robustness**: Handling noise and missing values.
- **Scalability**: Efficiency in disk-resident databases.
- **Interpretability**: Understanding provided by the model. 
___
# Review

|Color|Fur|Size|Class|
|:--|:--|:--|:--|
|brown|ragged|small|well-behaved|
|black|ragged|big|dangerous|
|black|smooth|big|dangerous|
|black|curly|small|well-behaved|
|white|curly|small|well-behaved|
|white|smooth|small|dangerous|
|red|ragged|big|well-behaved|
**Task:**  
Use the **ID3 algorithm** to determine a decision tree, where the attributes are to be chosen with the maximum average information gain.