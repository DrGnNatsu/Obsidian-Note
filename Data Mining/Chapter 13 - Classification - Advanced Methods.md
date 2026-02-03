---
tags:
  - data_mining
---
# Feature Selection and Engineering
Feature selection methods aim to select a subset of relevant features for use in model construction. There are three main types:
## Filter Methods
- Selects "good" features based on a goodness measure of the input features, independent of the classification model.
- Often used as a preprocessing step.
- Suppose we have `p` initial features and we with to select `k` features (`k` < `p`) if we have a goodness score for each futures we can simply select `k` features with highest goodness scores 
- **Example**: Using a measure like Chi-square to find the correlation between a feature and the class label, then selecting the features with the highest scores.
## Wrapper Methods
- Combines the feature selection step and classifier training step together in an iterative process.
- It "wraps" the feature selection process around the classifier.
- At each iteration, it builds a classifier with the current feature subset and updates the subset (e.g., add, remove, swap features) based on the classifier's performance.
- While this can find the optimal subset, it is computationally expensive as it may need to evaluate all $2^p - 1$ possible subsets. In practice, heuristic search strategies are used.
- This method uses to find the best subset presenting the dataset
## Embedded Methods
- Aims to combine the advantages of both filter and wrapper methods.
- Performs feature selection and classification model construction simultaneously, allowing them to mutually benefit.
- Tries to avoid the expensive, iterative search process of wrapper methods.
- **Example**: Decision trees naturally select features at each node, embedding the selection process into the model building.
# Bayesian Belief Networks
![[Bayesian Belief Networks.png|400]]
- A **Bayesian belief network** (or Bayesian network) is a probabilistic graphical model that allows for representing class conditional independencies between subsets of variables.
- It consists of two components:
    1.  A **directed acyclic graph (DAG)** representing the dependency structure.
    2.  A set of **conditional probability tables (CPTs)** for each variable.
- It provides a specification of a joint probability distribution.
    - **Nodes**: Random variables.
    - **Links**: Causal influence/dependency.
    - The probability of a combination of values is the product of the conditional probabilities: $P(x_1, \ldots, x_n) = \prod_{i=1}^{n} P(x_i | \text{Parents}(x_i))$.
## Joint Probability of a Bayesian Network 
If U = {A₁, ..., Aₙ} is the universe of variables in a Bayesian network, and pa(Aᵢ) are the parents of Aᵢ, then the joint probability distribution P(U) is the product of all the probability distributions in the network. $$P(x_1, \ldots, x_n) = \prod_{i=1}^{n} P(x_i | \text{Parents}(x_i))$$This allows for inference, such as calculating the probability of a set of query variables X given evidence e: $$P(X, e) = \sum_{U \setminus X} P(U, e) = \sum_{U \setminus X} \prod_i P(U_i | \text{parents}(U_i))e$$
## How Are Bayesian Networks Constructed?
- **Subjective construction**: Based on expert knowledge to identify direct causal structures.
	- Hidden Markdov Model (HMM): 
	- `n`-order MM: Based on `n` steps previous of the states to get more precise and concise about the probability of this states
- **Synthesis from other specifications**: Derived from formal system designs like block diagrams.
- **Learning from data**:
    - Learn parameters (CPTs) given a known structure.
    - Learn both structure and parameters from data.
    - The **Maximum Likelihood Principle** favors networks that maximize the probability of observing the given data.
# Classification by Backpropagation (Neural Networks)
- **Backpropagation** is a neural network learning algorithm.
- A **neural network** is a set of connected input/output units where each connection has a weight.
- During learning, the network adjusts these weights to predict the correct class label.
- This is also known as **connectionist learning**.
## Neuron: A Hidden/Output Layer Unit
- An input vector **x** is mapped to a variable **y** through a scalar product and a nonlinear activation function.
- The weighted sum of inputs is added to a **bias** ($\mu_k$), and then an activation function is applied.
## How a Multi-Layer Neural Network Works
1.  Inputs are fed into the **input layer**.
2.  They are weighted and fed into one or more **hidden layers**.
3.  The weighted outputs of the last hidden layer are fed to the **output layer**, which emits the prediction.
4.  The network is **feed-forward**: weights do not cycle back.
## Backpropagation Algorithm
- **Goal**: Minimize the mean squared error between the network's prediction and the actual target value.
- **Steps**:
    1.  Initialize weights to small random numbers.
    2.  Propagate inputs forward through the network.
    3.  **Backpropagate the error** from the output layer back to the input layer, updating weights and biases.
    4.  Terminate when the error is very small.
## Neural Network as a Classifier
- **Weakness**:
    - Long training time.
    - Requires empirical determination of parameters (e.g., topology).
    - Poor interpretability of learned weights and hidden units.
- **Strength**:
    - High tolerance to noisy data.
    - Ability to classify untrained patterns.
    - Well-suited for continuous-valued inputs and outputs.
    - Inherently parallel.
# Support Vector Machines (SVM)
- **Classification** is a mathematical mapping problem: find a function $f: X \rightarrow Y$.
- SVM is a classification method for both **linear and nonlinear data**.
- It uses a nonlinear mapping to transform the original data into a higher dimension where a linear optimal separating hyperplane (decision boundary) can be found.
## SVM General Philosophy
- SVM finds the hyperplane using **support vectors** (essential training tuples closest to the boundary) and **margins** (the space between the classes).
- The goal is to find the hyperplane with the **largest margin**, known as the **maximum marginal hyperplane (MMH)**.
## SVM for Linearly Separable and Inseparable Data
- **Linearly Separable**: A separating hyperplane can be written as $W \cdot X + b = 0$. The support vectors lie on the margin hyperplanes $W \cdot X + b = \pm 1$. This is solved as a constrained quadratic optimisation problem.
- **Linearly Inseparable**: The original input data is transformed into a higher-dimensional space where it becomes linearly separable.
## Kernel Functions for Nonlinear Classification
- The **kernel trick** allows SVM to operate in a high-dimensional feature space without explicitly computing the transformations.
- It applies a **kernel function** $K(X_i, X_j) = \Phi(X_i) \cdot \Phi(X_j)$ to the original data.
- **Typical Kernel Functions**:
    - Polynomial: $K(X_i, X_j) = (X_i \cdot X_j + 1)^h$
    - Gaussian radial basis function (RBF): $K(X_i, X_j) = e^{-\|X_i - X_j\|^2 / (2\sigma^2)}$
    - Sigmoid: $K(X_i, X_j) = \tanh(\kappa X_i \cdot X_j - \delta)$

| Feature | SVM | Neural Network |
| :--- | :--- | :--- |
| Algorithm Type | Deterministic | Nondeterministic |
| Generalization | Nice properties | Generalizes well but lacks strong mathematical foundation |
| Learning Mode | Batch mode (quadratic programming) | Incremental fashion |
| Complexity | Using kernels can learn very complex functions | Requires multilayer perceptron (nontrivial) |
# Lazy Learners (or Learning from Your Neighbors)
- **Lazy learning** (e.g., instance-based learning) simply stores training data and waits until it is given a test tuple.
- **Eager learning** (e.g., decision trees, SVMs) constructs a classification model before receiving new data.
- **Lazy**: Less time in training, more time in predicting.
- **Eager**: Must commit to a single hypothesis.
## The k-Nearest Neighbor (k-NN) Algorithm
- All instances correspond to points in an n-D space.
- The nearest neighbors are defined in terms of Euclidean distance.
- For a discrete-valued target, k-NN returns the most common value among the $k$ nearest training examples.
- For a real-valued target, it returns the mean value of the $k$ nearest neighbors.
## Case-Based Reasoning (CBR)
- Uses a database of problem solutions (cases) to solve new problems.
- Stores rich symbolic descriptions, not just points.
- **Four step process**: Retrieve, Reuse, Revise, Retain.
# Other Classification Methods
## Genetic Algorithms (GA)
- Based on an analogy to biological evolution.
- An initial population of rules (represented as bit strings) is randomly generated.
- Offspring are generated by **crossover** and **mutation**.
- The **fitness** of a rule is its classification accuracy.
- The process continues until a population of high-fitness rules evolves.
## Rough Set Approach
- Used to "roughly" define equivalent classes.
- Approximates a class C with a **lower approximation** (certain to be in C) and an **upper approximation** (cannot be described as not belonging to C).
# Additional Topics Regarding Classification
- **Multiclass Classification**:
    - **One-vs.-all (OVA)**: Train m classifiers, one for each class vs. all others.
    - **All-vs.-all (AVA)**: Train $m(m-1)/2$ binary classifiers for each pair of classes. Tends to be superior.
- **Semi-Supervised Classification**: Uses both labeled and unlabeled data (e.g., Self-training, Co-training).
- **Active Learning**: The learner queries a human "oracle" for labels on carefully selected unlabeled data.
- **Transfer Learning**: Extracts knowledge from source tasks to apply to a target task, useful when data is outdated or distribution changes.