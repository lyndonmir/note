# First Normal Form
## Definition
### Atomic
- no composite attributes
- no Mult attributes
- no complex data type--such as object oriented
### 1NF
- A relational schema R is in the first normal form if the domains of all attributes of R are atomic
- For the relational database, it's required that all relations are in 1NF
## Non-atonmic Values
### Deal With
- For composite attributes, use a number of attributes
- For multi-value attributes: use multi fields; use a separatet table or use a single field
### Drawbacks of non-atomic strategy
- complicate storage
- encourage redundant storage of data
- complicated to query
## Rule
- Atomicity is actually a property of how the elements of the domain are used, so judging on the application
# Pitfalls in Relational Database Design
## Pitfalls or Bad Design
- Redundant Storage
- insert/Delete/Update Anomalies
## Theory
- decompose a bad design into a set of relations
- each relation is in good form
- the decomposition is a lossless-join decomposition
- based on functional dependencies and multivalued dependencies
# Functional Dependencies
## Definition
## Use
- judge schema normalization
- sugget refinements
- test relations to see if they are legal under a given set of functional dependencies F
- Specify constraints(F) on the set of legal relatioins- schema
## Functional dependency vs key
- A functional dependency is a generalization of the notion of a key
- K is a superkey for the relation schema R iff K->R, K is a candidate key for R iff(K->R and No $\alpha \subset K, \alpha->R$)
- Fuctional dependencies can express constraints that cannot be expressed using keys
## Definition of Trivial and Non-Trivial Dependency
- trivial: $\alpha->\beta, if\beta \subseteq \alpha$
- non-trival: $\alpha->\beta, if\beta \not\subseteq \alpha$
## Closure of a Set of Functional Dependencies
### Definition
- The set of all functionial dependencies logically implied by F, $F^{+}$
### Armstrong's Axioms
- reflexive--trival
- augmentation
- transitive
### Supplemet of Armstrong's Axioms
- union
- decomposition
- pseudotransitivity
### Procedure for computing $F^{+}$
- steps
- The maximum number of Functional dependencies(FDs) is $2^{n} * 2^{n}$
## Closure of Attributes Sets
### Superkey test
- Method1, Find $F^{+}$, then find all $\alpha->\beta$, see whether{$\beta _{1}, \beta _{2}...$}=R
- Method2, Find the closure of $\alpha$
### Definition
- $\alpha^{+}$ is the set of attributes that are functionally determined by $\alpha$ under F
### Procedure for get $\alpha^{+}$
- steps
### Use
- Testing for a superkey
- Testing functional dependencies
- Computing the closure of F: use trival/reflexive
## Canoniacal Cover
### Definition
- a canonical cover of F, denoted by $F^{c}$, is a minimal set of FDs equivalent to F
- not redundant: no functional dependency in $F_{c}$ contains an extraneous attribute
- left side is unique
### How to get
- delete extraneous attributes
### Extraneous attributes
- redundant dependencies that can be inferred from the others: e.g. transitive
- Left side may be redundant
- right side may be redundant
# Decomposition
## Requestments of Decomposition
### Lossless-join decompostion
- divide R into R1 and R2, R1 and R2 have a mutual attribute which is either R1's key or R2's key: 
- represent by sttribute's closure: if $a^{+}\supseteq R_{1}/R_{2}$ 
### Dependency preservation
- represented by function dependencies' closure
- $(F_{1} \cup F_{2})^{+}=F^{+}$  
- $F_{i}$ is the set of dependencies in $F^{+}$ that include only attributes in $R_{i}$ 
- Testing for dependency preservation
### No redundancy
- in Boyce-codd Normal Form or Third Normal Form
- Good form- BCNF or 3NF
# Boyce-Codd Normal Form
## Definition
- example
## Testing for BCNF
- It suffices to check only the dependencies in the given set F for violation of BCNF
- To test decomposition a BCNF or not, under $F^{+}$ not only F, see the example
## BCNF Decomposition Algorithn
- steps
- example
## BCNF and Dependency Preservation
- It's not always possible to get a BCNF decompostion that is dependency preserving
# Third Normal Form
## Definition
- $\alpha \to \beta$ is trival
- $\alpha$ is a superkey for R
- Each attribute A in$\beta-\alpha$ is contained in a candidate key for R
## BCNF and 3NF
- 3NF is a minimal relaxation of BCNF to ensure dependency preservation
## Redundancy of 3NF
- repetition of information
- null values
## Testing for 3NF
- check only FDs in F
- check $\alpha$ is superkey or not by closure
- check the third condition, NP hard
## 3NF Decompostion Algorithm
- steps
## Comparision of BCNF and 3NF
- It's always possible to decompose a relation into relations in 3NF and lossless ,dependencies preserved
- It's always possible to decomose a relation into relations in BCNF and lossless
## Design Goals
# Multivalued Dependencies
## Definition
- 4-tuple definition
- another one: 3-tuple definition
## Notion
- Y$\to \to$ Z iff $(y_{1},z_{1},w_{1})\in r$ and $(y_{1},z_{2},w_{2})\in r$ then $(y_{1},z_{1},w_{2})\in r$ and $(y_{1},z{2},w{1})\in r$ 
- Since behavior of z and w are identical, it follows that $Y\to \to Z$ if $Y\to\to W$
## Theory of MVDs
- every functional dependency is also a multivalued dependency
- The closure $D^{+}$ of D is the set of all functional and multivalued dependecies logically implied by D
# Fourth Normal Form
## Definition
- A relation schma R is in 4NF with respect to a set D of functional and multivalued dependencies if for all multivalued dependencies in $D_{+}$ of the form $\alpha \to\to \beta$ where $\alpha \subseteq R$ and $\beta \subseteq R$ ,at least one of the following hold
1. it's trivial ($\beta \subseteq \alpha$ or $\alpha \cup \beta =R$)  
2. $\alpha$ is a superkey for schema
3. if a relation is in 4NF, it's in BCNF
## Requirement for decomposition
- All functioinal dependencies in $D^{+}$ that include only attributes of $R_{i}$
- All mutivalued dependencies of the form $\alpha \to]to (\beta \cap R_{i})$ 
## Denormalization for Performance
- steps
## Other Design Issues

