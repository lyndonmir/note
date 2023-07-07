# 6.1 The Basic of Counting
## 1. Basic Counting Principles
- The Sum Rule
- The Product Rule
## 2. The Inclusion-Exclusion Principle(Subtraction Rule)
## 3. Tree Diagrams
# 6.2 The Pigeonhole Principle
## 1. Introduction
- definition
- direct applications
## 2. The Generalized Pigeonhode Principle
- definition
## 3. Some elegant applications
- find pigeons
- find pigeonholes
- find ways to divide
- or used in sufficient or necessary condition as tools
# 6.3 Permutations and Combinations
## 1. Permutations
- Definition
- Notation
## 2. Combinations
- Definition
- Notation
## 3. Combination Proof
- Bijective Proof
- Double Counting Proof
# 6.4. Binomial Coefficients
## Theorem1
- $$(x+y)^{n}=\sum_{j=0}^{n}\begin{pmatrix}n\\j\\\end{pmatrix}x^{n-j}y^{j}$$
### Corollary 1
$$\sum_{k=0}^{n}\begin{pmatrix}n\\k\\\end{pmatrix}=2^{n}$$
### Corollary 2
$$\sum_{k=0}^{n}(-1)^{k}\begin{pmatrix}n\\k\\\end{pmatrix}=0$$
### Corollary 3
$$\sum_{k=0}^{n}2^{k}\begin{pmatrix}n\\k\\\end{pmatrix}=3^{n}$$
## Theorem2
- Pascal's identity$$\begin{pmatrix}n+1\\k\\\end{pmatrix}=\begin{pmatrix}n\\k-1\\\end{pmatrix}+\begin{pmatrix}n\\k\\\end{pmatrix}$$
## Theorem3
- Vandermonde's Identity$$\begin{pmatrix}m+n\\r\\\end{pmatrix}=\sum_{k=0}^{r} \begin{pmatrix}m\\r-k\\\end{pmatrix}\begin{pmatrix}n\\k\\\end{pmatrix}$$
### Corollary 4
$$\begin{pmatrix}2n\\n\\\end{pmatrix}=\sum_{k=0}^{n}\begin{pmatrix}n\\k\\\end{pmatrix}^{2}$$
## Theorem4
- $$\begin{pmatrix}n+1\\r+1\\\end{pmatrix}=\sum_{k=r}^{n}{\begin{pmatrix}k\\r\\\end{pmatrix} }$$
# 6.5 Generalized Permutations and Combinations
## Permutations
### Permutations with Repetition
- $n^{r}$
### Permutations with Indistinguishable Objects
- $n!/(n_{1}!n_{2}!.....n_{k}!)$
- first assume all are different  boxes, then find indistinguished ones
### r-Circle Permutation
- P(n,r)/r
## Combinations
### Combinations With Repetition
- C(n-1+r,r)
- n undistinguished elements divided into r groups, each group include zero or more;to use combination, we should guarantee each group exists at least one, then add the same amount elements as number of groups, then it comes to be n+r elements, we abstract such question into bars questions, n+r elements hav n+r-1 gap. Because we divide them into r groups, so we need r-1 bars, so we use combination to find bars' positions, that is C(n+r-1,r-1);
## Distributing objects into boxes
### Distinguishable objects and distinguishable boxes
- Permutations with indistinguished objects
### Distinguishable objects and indistinguishable boxes
- use Stirling numbers of the second kind
- ways to divide objects+objects are distinguishable
### Indistinguishable objects and distinguished boxes
- Combinations With Repetition
### Indistinguishable objects and indistinguished boxes
- ways to divide objects
