---
tags:
  - data_mining
---
___
# What is Cluster Analysis?
- **Cluster**: A collection of data objects that are:
    - **Similar** (or related) to one another within the same group.
    - **Dissimilar** (or unrelated) to objects in other groups.
- **Cluster analysis** (or clustering, data segmentation) involves finding similarities and grouping similar data objects into clusters.
- It is a form of **unsupervised learning** (no predefined classes - no class): learn by observations.
- **Typical applications**:
    - As a **stand-alone tool** to gain insight into data distribution.
    - As a **preprocessing** step for other algorithms.
## Applications of Cluster Analysis
- **Data reduction**: Summarisation, Compression (vector quantisation).
- **Hypothesis generation and testing**.
- **Prediction based on groups**.
- **Finding K-nearest Neighbours**: Localising search to a small number of clusters.
- **Outlier detection**: Outliers are often viewed as objects *"far away"* from any cluster (a very small cluster)
![[Cluster.jpeg]]
- **Application Examples**: Biology (taxonomy), Information retrieval (document clustering), Marketing (customer segmentation), City-planning, Earthquake studies, etc.
# Basic Steps to Develop a Clustering Task
1.  **Feature selection**: Select relevant information, Minimal information redundancy.
2.  **Proximity measure**: Define similarity/distance between feature vectors.
3.  **Clustering criterion**: Expressed via a cost function or rules.
4.  **Clustering algorithms**: Choice of algorithm.
5.  **Validation of the results**: Test the validity of the clusters.
6.  **Interpretation of the results**: Integrate with applications.
## Quality: What Is Good Clustering?
A good clustering method produces high-quality clusters with:
- High **intra-class similarity** (**cohesive** within clusters), the objects in the same cluster must be close enough.
- Low **inter-class similarity** (**distinctive** between clusters).
- Quality depends on the similarity measure (distance, cosine similarity), implementation, and ability to discover *hidden* patterns.
## Measure the Quality of Clustering 
- ***Dissimilarity/Similarity metric:*** 
	- Similarity is expressed in terms of a distance function, typically a metric: `d(i, j)`. 
	- The definitions of distance functions are usually different for interval-scaled, boolean, categorical, ordinal, and vector variables. Weights should be associated with different variables based on applications and data semantics (high means that attributes is important and reversely).
- ***Quality of clustering:*** 
	- There is usually a separate "quality" function that measures the "goodness" of a cluster. 
	- Hard to define "similar enough" or "good enough" as the answer is typically highly subjective (depends on the users).
## Considerations for Cluster Analysis
- **Partitioning criteria**: Single level vs. hierarchical partitioning.
- **Separation of clusters**: Exclusive (object belongs to one cluster) vs. non-exclusive.
- **Similarity measure**: Distance-based (Euclidean) vs. connectivity-based (density).
- **Clustering space**: Full space vs. subspaces (for high-dimensional data). How many dimensions does each object have?
## Requirements and Challenges 
- ***Scalability:*** Clustering all the data instead of only on samples. 
- ***Ability to deal with different types of attributes
- ***Constraint-based clustering:*** Using user-provided constraints or domain knowledge. 
- ***Interpretability and usability.*** 
- ***Others:*** 
	- Discovery of clusters with arbitrary shape. 
	- Ability to deal with noisy data. 
	- Incremental clustering (can update clustering) and insensitivity to input order. 
	- High dimensionality.
___
# Major Clustering Approaches

## Approaches (I)
- **Partitioning approach**: Construct various partitions and evaluate them by some criterion (e.g., minimising the sum of squared errors).
    - *Typical methods*: k-means, k-medoids, CLARANS.
- **Hierarchical approach**: Create a hierarchical decomposition of the data.
    - *Typical methods*: Diana, Agnes, BIRCH, CAMELEON.
- **Density-based approach**: Based on connectivity and density functions.
    - *Typical methods*: DBSCAN, OPTICS, DenClue.
- **Grid-based approach**: Based on a multiple-level granularity structure.
    - *Typical methods*: STING, WaveCluster, CLIQUE.
## Approaches (II)
- **Model-based**: Hypothesise a model for each cluster and find the best fit.
    - *Typical methods*: EM, SOM, COBWEB.
- **Frequent pattern-based**: Based on the analysis of frequent patterns.
    - *Typical methods*: p-Cluster.
- **User-guided or constraint-based**: Clustering with user-specified constraints.
    - *Typical methods*: COD, constrained clustering.
- **Link-based clustering**: Uses links between objects to cluster.
    - *Typical methods*: SimRank, LinkClus.
___
# Partitioning Methods
## Partitioning Algorithms: Basic Concept
- **Method**: Partition a database $D$ of $n$ objects into $k$ clusters to minimise the sum of squared distances (where $c_i$ is the centroid or medoid of the cluster $C_i$). If the value $E$ It’s small, that is a good cluster.
	- Centroid: is the centre of the cluster
	- Medoid: is the closest object to the centroid
$$E = \sum_{i=1}^{k} \sum_{p \in C_i} (d(p, c_i))^2$$
- **Heuristic methods**: k-means and k-medoids.
    - **k-means**: Each cluster is represented by its center (mean).
    - **k-medoids**: Each cluster is represented by one of its objects (medoid).
## The K-Means Clustering Method
1. Partition objects into $k$ nonempty subsets.
2. Compute seed points as centroids (mean point) of the current clusters.
3. Assign each object to the cluster with the nearest seed point.
4. Go back to Step 2; stop when the assignment does not change.
### Comments on the K-Means Method
- **Strength**: Efficient: $O(tkn)$, where $n$ is \# objects, $k$ is \# clusters, $t$ is \# iterations.
- **Weakness**:
    - Often terminates at a **local optimum**.
    - Applicable only to continuous n-dimensional space.
    - Need to specify $k$ in advance.
    - Sensitive to noisy data and **outliers**.
    - Not suitable for non-convex or different-sized clusters.
## The K-Medoid Clustering Method
- Finds representative objects (**medoids**) in clusters.
- **PAM (Partitioning Around Medoids)**: Iteratively replaces medoids with non-medoids if it improves total distance. Effective for small datasets, but does not scale well.
- Efficiency improvements: **CLARA** (PAM on samples), **CLARANS** (randomized re-sampling).
___
# Hierarchical Methods

## Hierarchical Clustering
- Uses a distance matrix as the clustering criterion. Does not require $k$ as input but needs a termination condition.
- **Agglomerative (AGNES)**: Bottom-up. Starts with each object as a separate cluster and merges them.
- **Divisive (DIANA)**: Top-down. Starts with all objects in one cluster and splits them.
## AGNES (Agglomerative Nesting)
- Use the **single-link** method and a dissimilarity matrix.
	- $L(R,S)=min(D(i,j)),i \in R,j\in S$
- Merge nodes that have the least dissimilarity in a non-descending fashion.
- Eventually, all nodes belong to the same cluster.
## DIANA (Divisive Analysis)
- Inverse order of AGNES.
- Eventually, each node forms a cluster on its own.
## Dendrogram
- A tree of clusters that shows how clusters are merged (or split).
- Cutting the dendrogram at a desired level yields a clustering.
## Distance between Clusters
- **Single link**: Smallest distance between an element in each cluster.
- **Complete link**: Largest distance between an element in each cluster.
- **Average**: Average distance between elements.
- **Centroid**: Distance between cluster centroids.
- **Medoid**: Distance between cluster medoids.
## Extensions to Hierarchical Clustering
- **Weakness of agglomerative methods**: Can never undo a merge (can not go back); does not scale well (at least $O(n^2)$).
- **BIRCH**: Uses CF-tree to incrementally adjust sub-clusters. Scales linearly but handles only numeric data.
- **CHAMELEON**: Uses dynamic modelling and a two-phase graph-based algorithm.
___
# Density-Based Methods 

## Density-Based Clustering
- Clusters based on density (local cluster criterion), such as density-connected points.
- **Major features**: Discovers clusters of arbitrary shape, handles noise, and often requires one scan.
- **Studies**: DBSCAN, OPTICS, DENCLUE.
## DBSCAN: Density-Based Spatial Clustering of Applications with Noise
- **Relies on a density-based notion of a cluster**: A cluster is a maximal set of density-connected points.
- **Basic Concepts**:
    - **Eps**: Maximum radius of the neighbourhood.
	    - $R_m$
    - **MinPts**: Minimum number of points in an Eps-neighbourhood.
    - **Core point**: A point with at least `MinPts` in its Eps-neighbourhood.
    - **Density-Reachable**: A point $p$ is directly density reachable from $q$ If there is a path of core points from $q$ to $p$ with respect to `Eps, MinPts`.
	    - The `q` is a core point.
	    - The `p` is re
    - **Density-Connected**: Two points are connected if they are reachable from a common core point.
	    - Merge all the clusters that is the density reachable
- **Algorithm**: Arbitrarily select a point, retrieve all density-reachable points. If it's a core point, a cluster is formed.
___
# Evaluation of Clustering
- How to determine the number of clusters?
    - **Empirical method**: $k \approx \sqrt{n/2}$.
    - **Elbow method**: Use the turning point in the curve of sum of within-cluster variance vs. # of clusters.
    - **Cross-validation method**.
- **Measuring Clustering Quality**: 3 kinds of measures:
    - **External**: Supervised, uses ground truth (e.g., purity, F-measure).
    - **Internal**: Unsupervised, criteria derived from data itself (e.g., cohesion, separation).
    - **Relative**: Directly compare different clusterings.