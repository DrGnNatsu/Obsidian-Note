---
tags:
  - data_mining
---
___
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