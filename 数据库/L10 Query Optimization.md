# Introduction
## Steps in cost-based query optimization
1. Generate logically equivalent expressions using equivalence rules
2. Annotate resultant expressions to get alternative query planes
3. Choose the cheapest plan based on estimated cost
## Estimation of plan cost based on
- Statistical information about  relations
- Statistics estimation for intermediate results
- Cost formulae for algorithms, computed using statistics
# Transformation of Relational Expressions
## Equivalence Rules
1. Conjunctive selection
2. Selection operations are commutative
3. Combine projection operations
4. Selections can be combined with Cartesian products and theta joins
5. Theta-join operations (and natural joins) are commutative
6. a) Natural join operations are associative
6. b) Theta joins are associaive in the following manner
7. The selection operation distributes over the theta join operation under the following two conditions
7. a) 
7. b)
8. The projection operation distributes over the theta join operatioin as follows
9. The set operations union and intersection are commutative
10. Set union and intersection are associative
11. The selection operation distributes over union/intersection/divide
12. The projection operation distributes over union\
### Strategy
- Performing the selectioin as early as possible 
- Performing the projection as early as possible
- do small join first
## Enumeration of Equivalent Expression
## brute-force
- Apply all applicable equivalence rules on every subexpression of every equivalent expression found so far
## Optimize
- based on transformation rules
- special case approach for queries with only selections, projections and joins
## Implementing Tranformation Based Optimization
- Space requirements reduced by sharing common sub-expressions
- Time requirements are reduced by not generating all expressions
## Cost Estimation
# Statistics for Cost Estimation
## Notations
## Histograms
## Selection Size Estimation
- $\sigma _{A=v}(r)$
- $\sigma _{A\leq v}(r)$
## Size Estimation of Complex Selections
- Selectivity
- Conjunction
- Disjunction
- Negation_
## Estimation of the Size of Joins
- several conditions
- examples
## Size Estimation for Other Operations
- Projection
- Aggregation
- Outer join
- Set Operations
- Selections
## Estimation of Number of Distinct Values
- Selections
- Joins
- use "no more than" to understand the fomulaes provided
## Choice of Evaluation Plans
### Must consider the interaction of evaluation techniques whenchoosing evaluation plans
- Merge join may be costlier than hash join, but may provide a sorted output which reduces the cost for an outer level aggregation.
- Nested loop join may provide opportunity for pipelining
## Cost-Based Optimization

