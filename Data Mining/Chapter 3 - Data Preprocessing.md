#data_mining 
___
# Data Preprocessing: An Overview
- The first phase of the pipeline: how to correct and explore the data
___
## Data Quality: Why Preprocess the Data?
*Measures for data quality*: A multidimensional view
- Accuracy: correct or wrong, accurate or not
- Completeness: not recorded, unavailable, …
- Consistency: some modified but some not, dangling, ...
	- One variable can be defined in many ways; you need to make in the same meaning.
- Timeliness: timely update?
- Believability: How trustworthy is the data are correct? Is the survey correct, reliable?
- Interpretability: how easily can the data be understood?
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
# Data Cleaning
___
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
	- Noise: random error or variance in a measured variable
	- Incorrect attribute values may be due to
		- faulty data collection instruments
		- data entry problems
		- data transmission problems
		- technology limitation
		- Inconsistency in naming convention
	- Other data problems which require data cleaning
		- duplicate records
		- incomplete data
		- inconsistent data
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
	- *The most probable value: inference-based, such as a Bayesian formula or a decision tree* - predict technique.
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
# Data Integration
___
**Data integration**: Combines data from multiple sources into a coherent store
**Schema integration**: e.g., A.cust-id $=$ B.cust-#
- Integrate metadata (the data describes that data) from different sources
**Entity identification problem**:
- Identify real-world entities from multiple data sources, e.g., Bill Clinton = William Clinton.
Detecting and resolving data value conflicts
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
$\mathcal{X}^2$ (chi-square) test
$$
\mathcal{X}^2 = \sum \dfrac{(Obeserved - Expected)^2}{Expected}
$$The larger the $\mathcal{X}^2$ value, the more likely the variables are related
The cells that contribute the most to the $\mathcal{X}^2$ value are those whose actual count is very different from the expected count
Correlation does not imply causality
- \# of hospitals and \# of car thefts in a city are correlated
- Both are causally linked to the third variable: population

## Correlation Analysis (Nominal Data)

Correlation coefficient (also called **Pearson's product moment coefficient**).
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
\begin{aligned}
a'_k=\frac{a_k -\text{mean}(A)}{\text{std(A)}}\\
b'_k=\frac{b_k -\text{mean}(B)}{\text{std(B)}}
\end{aligned}
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
# Data Reduction
___
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
Redundant attributes:
- Duplicate much or all of the information contained in one or more other attributes
- E.g., the purchase price of a product and the amount of sales tax paid
Irrelevant attributes:
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
	- Combining features (see: discriminative frequent patterns in the Chapter on “Advanced Classification”)
	- Data discretization
### Data Reduction 2: Numerosity Reduction
Reduce data volume by choosing alternative, _smaller forms_ of data representation
**Parametric methods** (e.g., regression):
- Assume the data fits some model, estimate the model parameters, store only the parameters, and discard the data (except possible outliers)
- Ex.: Log-linear models—obtain value at a point in _m_-D space as the product of the appropriate marginal subspaces
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