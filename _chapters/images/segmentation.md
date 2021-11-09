---
title: Segmentation
keywords: Gestalt Theory, Agglomerative Clustering, Graph-Based Segmentation
order: 9 # Lecture number for 2020
---
# 13.1 Introduction
This section

# 13.2 Gestalt Theory
# 13.3 Agglomerative Clustering
# 13.4 Graph-Based Segmentation
Introduced by Felzenszalb and Huttenlocher

**Problem Formulation**
Graph G = (V, E)
V is a set of nodes
E is a set of undirected edges between pairs of pixels
w(vi, vj) is the weight of the edge btween nodes vi and vj
S is a segmentation of graph G such that G' = (V, E') where 
S divides G into G such that it contains distinct clusters C

MInt

Dif(C1, C2) is difference between two clusters
in(C1, C2) is internal difference for 

Predicate D deermines whether there is a boundary for segmentation

If dif between two clusters is less than in(C1, C2), then merge

k / |C| sets threshold by which components need to be different from internal nodes

If k is large, it causes preference of larger objects. (since it is more likely to merge)

test: 
![\Large x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}](https://latex.codecogs.com/svg.latex?\Large&space;x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}) 

**Features and Weights**
Project every pixel into feature space defined by (x, y, r, g, b)
Each pixel is connected to its neighboring pixels and weights are determined by difference in intensities
Weights between pixels are determined using L2 (Euclidian distance) in feature space
Edges are chosen for only top ten nearest neighbors in feature sapce to ensure run time of O(n log n) where n is number of pixels.
