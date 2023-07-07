# Introduction
## Definition
- Given a set of objects, place them in groups such that the objects in a group are similar(or related) to one another and different from(or unrelated to) the objects in other groups
## Application
### Understanding
- browsing group related documents
### Summarization
- Reduce the size of large data sets


# Types of Clusterings
## General
- A clustering is a set of clusters
## Hierarchical Clustering
- A set of nested clusters organized as a hierarchical tree
- ![[Pasted image 20230323205051.png]]
## Partitional clustering
- A division of data objects into non-overlapping subsets(clusters)
- ![[Pasted image 20230323205001.png]]
## Fuzzy Clustering(one type of )
- In fuzzy clustering, a point belongs to every cluster with some weight between 0 and 1
- Weights must sum to 1
- Probabilistic clustering has similar characteristics
## Distinctions Between Sets of Clusters
### Exclusive versus non-exclusive
- In non-exclusive clusterings, points  may  belong  to multiple  clusters
- Can belong  to  multiple  classes  or could be 'border' points 
### Partial  versus complete
- In some cases, we only want to cluster some of the data

# Types of Clusters
## Well-separated clusters
## Prototype-based clusters
## Contiguity-based clusters
## Density-based clusters
## Described by an Objective Function
## Characteristics of Input Data Are Important
### Type of proximity or density measure
- Central to clustering
- Depends on data and application
### Data characteristics that affect proximity and density
- Dimensiionality(Sparseness)
- Attribute Type
- Special relationships in the data
- Distribution of the data
### Noise and Outliers
- Often interfere with the operation of the clustering algorithm
### Clusters of differing sizes, densities and shapes
# Clustering Algorithms
## K-means and its variants
### General
- Partitional clustering approach
- Number of clusters, K, must be specified
- Each cluster is associated with a centroid(center point)
- Each point is assigned to the cluster with the closest centroid
### Steps
1. Select K points as the initial centroids
2. repeat
3. Form K clusters by assigning all points to the closet centroid
4. Recompute the centroid of each cluseter
5. until the centroid don't change
### Example
![[Pasted image 20230323212824.png]]
### Detalis
### Objective Function(SSE a common one)
$$SSE\:=\:\sum_{i=1}^{K}{\sum_{x\in C_{i}}dist^{2}(m_{i},x)} $$
- x is a data point in cluster $C_{i}$ , $m_{i}$ is the centroid(mean) for cluster $C_{i}$
- SSE improves in each iteration of K-means until it reaches a local or global minima
### Choose Inittial Centroids
- Importance
![[Pasted image 20230323214537.png]]
- If clusters are the same size n, then $$ P\:=\: \frac{number\:of\:ways\:to\:select\:one\:centroid\:from\:each\:cluster}{number\:of\:ways\:to\:select\:K\:centroids}=\frac{K!n^{K}}{(Kn)^{K}}=\frac{K!}{K^{K}}$$
- solutions
1. Multiple runs
2. Use some strategy to select the k initial centroids and select among then
  1. Select most widely separated
  2. Use hierarchical clustering
3. Bisecting K-means
### K-means ++
1. select an initial point at random to be the first centroid, name as $C_{k},k=0$
2. For each of the N points,$x_{i},i\in [1,N]$, calculate $d_{i} = min{D_{i,j}}$
3. $P_{i}=\frac{d_{i}^{2}}{\sum_{i}d_{i}^{2}}$, which $P_{i}$ represent i's possibility to be the next centroids, select the max one
4. Then numbers of centroid increase by 1, repeat these steps until we get k centroids
### Bisecting K-means
## Hierarchical clustering
## Density-based clustering
