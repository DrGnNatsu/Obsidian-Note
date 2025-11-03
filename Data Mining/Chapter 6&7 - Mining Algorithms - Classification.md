---
tags:
  - data_mining
---
___
# Supervised vs. Unsupervised Learning

## Supervised learning (classification)
- **Supervision**: The training data, such as observations or measurements, are accompanied by **labels** indicating the classes to which they belong.
- New data is classified based on the models built from the training set.
(See image on page 2 for an example of Training $\rightarrow$ Model Learning $\rightarrow$ Prediction)
![[Supervised Learning.png]]
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
(See image on page 3 showing a scatter plot with a regression line).
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
___
- Training data set: `Buys_computer`
- Resulting tree structure. (See image on page 5 for the full decision tree diagram.)
![[Decision Tree.png]]
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
(See image on page 14 for the formula and definition of terms).
___
# Bayes Classification Methods
___
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
____
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
___
## Evaluation Metrics
- Use **validation test set** of class-labeled tuples instead of training set when assessing accuracy.
- Methods for estimating accuracy: Holdout, Random Subsampling, Cross-validation, Bootstrap.
### Classifier Evaluation Metrics: Confusion Matrix
The matrix shows: Actual Class vs. Predicted Class.

| Actual class/Predicted class | $C_1$                | $\sim C_1$           |
| :--------------------------- | :------------------- | :------------------- |
| $C_1$                        | True Positives (TP)  | False Negatives (FN) |
| $\sim C_1$                   | False Positives (FP) | True Negatives (TN)  |
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