---
tags:
  - data_mining
---
----
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

# Holdout, cross-validation, bootstrap 
___
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
- Still not optimum: the different test sets overlap 
	- Can we prevent overlapping?
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
- **Disadvantage**: Stratification is not possible as the test set contains only one instance. (exception: NN)
## Bootstrap
- CV uses sampling without replacement 
	- The same instance, once selected, cannot be selected again for a particular training/test set 
- The bootstrap uses sampling with replacement to form the training set 
	- Sample a dataset of n instances n times with replacement to form a new dataset of n instances 
	- Use this data as the training set 
	- Use the instances from the original dataset that don’t occur in the new training set for testing
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
# Comparing schemes: the t-test 
___
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
- Most popular measure: **Mean-squared error (MSE)**.
$$\text{MSE} = \frac{\sum_{i=1}^{n} (p_i - a_i)^2}{n}$$
- Easy to manipulate mathematically.
### Other Measures (Numeric)
- **Root mean-squared error (RMSE)**.
- **Mean absolute error (MAE)**: Less sensitive to outliers than MSE.
- **Relative error values** (e.g., $10\%$ error when predicting $500$).
### Improvement on the Mean
Measures how much the scheme improves compared to simply predicting the average ($\bar{a}$).
- **Relative squared error**: $\frac{\sum(p_i - a_i)^2}{\sum(\bar{a} - a_i)^2}$
- **Relative absolute error**: $\frac{\sum|p_i - a_i|}{\sum|\bar{a} - a_i|}$
### Correlation Coefficient (Numeric Prediction)
Measures statistical correlation ($r_{PA}$) between predicted ($p$) and actual ($a$) values. Performance leads to large positive values.

# Predicting probabilities: loss functions 
___
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

|              | Yes | NO  | Predicted Class |
| ------------ | --- | --- | --------------- |
| Yes          | TP  | FP  |                 |
| No           | FN  | TN  |                 |
| Actual Class |     |     |                 |
- Can take costs into account when making predictions, especially when errors have different impacts. 
- **Basic Idea**: Only predict a high-cost class when very confident. 
- **Expected Cost**: Calculated by the dot product of the vector of class probabilities and the appropriate column in the cost matrix. 
- **Goal**: Choose the column (class) that minimizes the expected cost.
Here is the definition and formula for the Kappa statistic as presented in the slides:

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
# Evaluating numeric prediction 
- **Same strategies** apply: independent test sets, cross-validation, significance tests. - **Difference**: Error measures used. 
- Actual targets: $a_1, a_2, \ldots, a_n$. Predicted targets: $p_1, p_2, \ldots, p_n$. 
- Most popular measure: **Mean-squared error (MSE)**. $$\text{MSE} = \frac{\sum_{i=1}^{n} (p_i - a_i)^2}{n}$$ - Other measures: Root Mean-Squared Error (RMSE), **Mean Absolute Error (MAE)** (less sensitive to outliers). 
- **Relative Error Measures** (Squared or Absolute) compare performance against simply predicting the average ($\bar{a}$).

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
