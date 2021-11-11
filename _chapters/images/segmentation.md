---
title: Segmentation
keywords: Gestalt Theory, Agglomerative Clustering, Graph-Based Segmentation
order: 9 # Lecture number for 2020
---
# 13.1 Introduction
The goal of image segmentation is to identify groups of pixels that go together. 

# 13.2 Gestalt Theory
# 13.3 Agglomerative Clustering
# 13.4 Graph-Based Segmentation


![](https://i.imgur.com/ZHtHFXg.jpg)
![](https://i.imgur.com/Ahv5xsA.jpg)
_The end result of segmentation allows us to group and differentiate distinct clusters of pixels in an image._

### Problem Formulation
We start with a Graph $G = (V, E)$, where $V$ is a set of nodes and $E$ is a set of undirected edges between pairs of pixels. Let's define $w(v_i, v_j)$ as the weight of the edge btween nodes $v_i$ and $v_j$.

$S$ is a segmentation of graph G such that $G' = (V, E')$ where $S$ divides $G$ into G such that it contains distinct clusters $C$. 
![](https://i.imgur.com/UibIc12.png =x250)
In this case, we have 3 distinct clusters.



### Predicate for Segmentation
We will define two functions that we will use for merging clusters (dif and in):


* ![](https://i.imgur.com/Lg3xQ8R.png =x50)is the minimum difference between a node $v_i$ in cluster $C_1$ and a node $v_j$ in cluster $C_2$.

* ![](https://i.imgur.com/zgASFB1.png =x50) is maximum internal difference that connects two nodes within each cluster ($C_1$ and $C_2$).
    
Now that we have our two functions, we will use them to determine whether we want to merge two clusters. This is done by the following equation:
![](https://i.imgur.com/mjI0jlC.png =x75)

If $dif(C1,C2)$ is less than $in(C1, C2)$, we will merge. Practically speaking, this means that the clusters are very close to each other such that the minimum weighted edge between clusters $C1$ and $C2$ is less than both clusters' max internal weighted edges. 

![](https://i.imgur.com/WfawsdA.png =x200)


**Notes on Constant $k$**

* $\dfrac{k}{|C|}$ sets a threshold by which components need to be different from internal nodes.
* If k is large, it causes preference of larger objects since the clusters are more likely to merge.

![](https://i.imgur.com/xXBPMGU.png =x160)![](https://i.imgur.com/kUgUg6H.png =x160)

### Features and Weights
To put this algorithm to work, we can now project every pixel into feature space defined by $(x, y, r, g, b)$. Then, we build out a graph where each pixel is connected to its 8 neighboring pixels.

![](https://i.imgur.com/Q3ONMgP.png =x100)

Edge weights are determined by difference in intensities by using using L2 norm (Euclidian distance) in the feature space. 

![](https://i.imgur.com/x27iFBO.png)

Edges are chosen for only top ten nearest neighbors in feature space to ensure run time of $O(n \log n)$ where $n$ is number of pixels.




