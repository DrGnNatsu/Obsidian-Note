#data_mining  
___
# Evaluation: the key to success 
___
> How predictive is the model we learned? 
- Error on the training data is **not** a good indicator of performance on future data. 
	- Otherwise, 1-NN would be the optimum classifier! 
- Simple solution that can be used if lots of (labeled) data is available: 
	- Split the data into a *training set* and a *test set*.
- However, (labeled) data is usually limited:
	- More sophisticated techniques need to be used.
# Issues: training and testing 
___
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
- Resubstitution error: error rate obtained from training data
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
- In statistics, a succession of independent events like this is called a Bernoulli process.
	- Statistical theory provides us with confidence intervals for the true underlying proportion.
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
- The holdout method reserves a certain amount for testing and uses the remainder for training
	- Usually: one third for testing, the rest for training 
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
- Often the subsets are stratified before the crossvalidation is performed 
- The error estimates are averaged to yield an overall error estimate
### Leave-One-Out Cross-Validation
- Leave-One-Out: a particular form of cross-validation: 
	- Set number of folds to number of training instances 
	- I.e., for n training instances, build classifier n times
- Makes best use of the data 
- Involves no random subsampling 
- Very computationally expensive
	- (exception: NN)
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
	- Thus, its probability of ending up in the test data is: 
	- This means the training data will contain approximately $63.2\%$ of the instances

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
# Predicting probabilities: loss functions 
___
- Performance measure so far: success rate 
- Also called 0-1 loss function: 
- Most classifiers produces class probabilities 
- Depending on the application, we might want to check the accuracy of the probability estimates 
- 0-1 loss is not the right thing to use in those cases
## Quadratic loss function
## Informational loss function

# Cost-sensitive measures 
___
- In practice, different types of classification errors often incur different costs
- Examples: 
	- Loan decisions
	- Oil-slick detection 
	- Fault diagnosis 
	- Promotional mailing
- The confusion matrix:
# Evaluating numeric prediction 
___
# The Minimum Description Length principle
___

