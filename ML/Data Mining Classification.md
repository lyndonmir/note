# General Approach for Building Classification Model
- Training set->Induction:"learn model" ->Model->Deduction"apply model"->Test Set
# Hunt's Algorithm
## General Procedure
- If $D_{t}$ contains records that belong the same class $y_{t}$, then t is a leaf node labeled as $y_{t}$, where $y_{t}$ is an attribute that includes many values.
- If $D_{t}$ contains records that belong to more than one class, use an attribute test to split the data into smaller subsets. Recursively apply the procedure to each subset.
  ![[Pasted image 20230320222718.png]]
# Methods for Expressing Test Conditions
## Binary
## Nominal
- Muti-way split
- Binary split
## Ordinal
- Multi-way
- Binary split
## Continous
- Discretization
- Binary Decision
#  Ways to determine the Best Split
## Measures of Node Imputity
- Gini Index
 $$Gini\quad Index = 1 - \sum_{i=0}^{c-1}{p_{i}(t)^{2}}$$
 - Entropy
 $$Entropy\quad = -\sum_{i=0}^{c-1}{p_{i}(t)log_{2}p_{i}(t)}$$
 - Misclassification error
 - $$ Classification\quad error = 1-max[p_{i}(t)]$$
 - Gain
	 $$Gain\quad = P-M$$
	 where P is impurity before splitting, M is impurity after splitting(Compute impurity of each child and weighted sum up)
##  GINI Index
### Maximum and Minimum
- Maximum:
	Maximum of 1-1/c when records are equally distributed, worst
- Minimum:
	Minimum of 0 when are records belong to one class
### Single Node
![[Pasted image 20230320230141.png]]
### A collection of nodes
![[Pasted image 20230320230235.png]]
### Binary Attributes
### Categorical Attributes
![[Pasted image 20230320230327.png]]
### Continuous Attributes
![[Pasted image 20230320230451.png]]
- Sort the attribute on values
- Linearly scan these values, each time updating the count matrix and computing gini index
- Choose the split position that has the least gini index
## Entropy
### Maximum and Minimum
- Maximum:
	Maximum of $log_{2}c$ when records are equally distributed, worst
- Minimum:
	Minimum of 0 when are records belong to one class
### Single Node
![[Pasted image 20230320230656.png]]
### Gain Ration
$$Gain\quad Ratio = \frac{Gain_{split}}{Split\quad Info}$$
$$Split\quad Info = \sum_{i=1}^{k}\frac{n_{i}}{n}log_{2}\frac{n_{i}}{n}$$
## Classification Error
### Maximum and Minimum
- Maximum:
	Maximum of 1-1/c when records are equally distributed, worst
- Minimum:
	Minimum of 0 when are records belong to one class
### Single Node
![[Pasted image 20230320231144.png]]
## Comparison among Impurity Measures
- For a 2-class problem
![[Pasted image 20230320231311.png]]
- Misclassification Error vs Gini Index
![[Pasted image 20230320231350.png]]
# Decision Tree Based Classification
## Advantages
- Relatively inexpensive to construct
- Extremely fast at classifying unknow records
- Easy to interpret for small-sized trees
- Robust to noise(especially when methods to avoid overfitting are employed)
- Can easily handle redundant attributes
- can easily handle irrelevant attributes(unless the attributes are interacting)
## Disadvantages
- Greedy nature of splitting criterion, interacting attributes may be passed over in favor of other attributed that are less discriminating
- Each decision boundary involves only a single attribute