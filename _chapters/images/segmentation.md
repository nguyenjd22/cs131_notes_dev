---
title: Segmentation
keywords: Gestalt Theory, Agglomerative Clustering, Graph-Based Segmentation
order: 9 # Lecture number for 2020
---
# 13.1 Introduction
The goal of image segmentation is to identify groups of pixels that go together, so that they represent coherent objects and regions. We often think of image segmentation as a "clustering" problem, where we create groups formed by similar, related points (in this case pixels). There are a few reasons to do this:
* #### Summarize data:
  It is often easier to think of an image as consisting of several macroscopic entities rather than a series of pixels. Representing each entity as a token rather than each pixel individually allows us to analyze large amounts of data more efficiently, as well as denoise data by separating actual entities from noise.
* #### Counting
  Clustering allows us to get characteristics of the segmented images, and count up/represent those summary characteristics e.g. size, color, etc.
* #### Segmentation
  As discussed earlier, we are able to separate images into different coherent regions using clustering.
* #### Prediction
  After clustering images, we are able to see similarities between the clusters- for instance, image labels determining what a specific clster depicts. We can use this to infer the classifications of unknown clusters, as they are likely to be similar.
  
In this unit, we will learn different ways through which images can be broken down into clusters and segmented, as well as the characteristics that delineate between clusters and allow us to group pixels and macroscopic components of images together.


# 13.2 Gestalt Theory
Gestalt Theory is a commonly used theory within the perception subfield psychology. In essence, Gestalt theory states that visual perception is more than merely identifying objects in an image; it posits that groupings, or relations of objects with each other, is also important to understanding. (The word "Gestalt" in German roughly represents an idea similar to "group" in English.)

Several types of Gestalt perception are displayed below:
* #### Subjective contours: 
    Illusory edges or borders perceived/inferred by an observer using gaps in an existing image. In the below image, observe the illusory rings perceived by deleting parts of the black circles.
    
    <img src="https://i.imgur.com/wTExxVS.png" alt="drawing" width="275"/>
    
* #### Occlusion: 

    The ability to perceive the original object despite deleted sections. This occurs often with regular shapes (see circle, below) as well as common objects which we can infer the remainder of (see panda from WWF logo, below), due to having a familiarity with the general shape.

    <img src="https://i.imgur.com/VKM7RNJ.png" alt="drawing" width="275"/>
    <img src="https://i.imgur.com/tDfRkVC.png" alt="drawing" width="275"/>

### Gestalt Factors
Scientists have identified several "factors"- similarities between objects that make them more likely to be clustered together by humans. Following are 8 of the main factors:


* #### Proximity
    Proximity states that objects closer to each other are likely to be grouped together. 
    
    <img src="https://i.imgur.com/Xxdw47x.png" alt="drawing" width="500"/> 
    
    Here, we observe on the left a normal grid of circles with 6 columns. However, on the right, because the columns are paired up and separated, we perceive it as 3 groups of 2 columns. 
    
* #### Similarity
  Similarity states that objects that appear similar are likely to be grouped together.
  
  <img src="https://i.imgur.com/ZdKtMv7.png" alt="drawing" width="250"/><img src="https://i.imgur.com/qetE0qK.png" alt="drawing" width="295"/>
  
  Here, we observe first the same 6x6 grid of squares, but this time in the second image the rows alternate colors. Because the circles within each row appear more visually similar to other rows of the same color, viewers are more likely to differentiate the grid into two groups of different colored circles.
  
* #### Common Fate
  Common fate states that objects with a "similar fate"- that is, they appear to be moving in the same direction- are more likely to be grouped together.
  
<img src="https://i.imgur.com/yrAkszy.png" alt="drawing" width="250"/>

    Here, we observe that the eight birds all appear to be moving up and towards the right; the common fate factor therefore argues that we tend to observe them as a single flock or unit.
    
* #### Common Region
  Common region states that objects drawn to lie within a single region, with a boundary separating them from other objects, are more likely to be grouped together.
  
<img src="https://i.imgur.com/gY9MgN4.png" alt="drawing" width="400"/>

    Here, in the top half there is no grouping (in fact, due to the proximity factor we consider the two middle dots to be grouped). However, we observe in the bottom half of the image that the dots are separated into two groups by the blue rectangular boundaries; the common region factor states that we will observe the four dots as two individual groups.
    
* #### Parallelism
    Parallelism states that objects that are "parallel"- that is, they are oriented in the same way- are likely to be grouped together.
    
    <img src="https://i.imgur.com/f6ccCpC.png" alt="drawing" width="400"/>
    
    Here, we can observe that there are three line segments that are parallel and facing the same general direction. According to the parallelism factor, these are more likely to be grouped together, while the three other lines that share no parallelism with each other do not belong to any group.
    
* #### Symmetry
  Symmetry states that objects that are symmetric across some axis will be more likely to be grouped together.
  
   <img src="https://i.imgur.com/xSfVNxi.png" alt="drawing" width="400"/>
   
    On the left, we can observe that the curly left brace and square right brace aren't symmetrical, while on the right, the curly left and right braces are symmetrical across a vertical axis. This leads to the sense that the two characters on the right are grouped, more so than the ones on the left.
    
* #### Continuity
    Continuity states that we perceive continuous, flowing lines as grouped, as opposed to sharp turns or discontinuities.
    
    On the left, we can observe the uncolored image. Gestalt's principle of continuity explains that we interpret image \(a) as two separate lines separated as shown in (b) with both lines remaining smooth, fluid, and intact. Continuity argues that we do not see the separation as shown in \(c\), which has the lines include jagged turns and non-fluid connections.
    
* #### Closure
  Closure states that humans tend to perceive objects in a complex pattern as belonging to a single pattern or object rather than a series of disconnected parts.
  
<img src="https://i.imgur.com/5Vssqc2.png" alt="drawing" width="400"/>

    In the IBM logo, we perceive the image as forming the characters I, B, and M, rather than a series of disconnected horizontal shapes. This is due to the closure factor, which states that that because the shapes form the pattern of letters, we fill in the empty space, and interpret the image as those letters rather than a random collection of shapes.
    
With that said, it's important to note that even though these concepts exist, to implement them in an algorithm is quite difficult. For instance, especially when dealing with real-world objects, it's not easy to determine if two objects share a grouping by the parallelism factor, because of the complexities of images and slight variations that make algorithmic determination of such factors difficult.

### Interpretative Cues
Interpretative cues aid our observational skills to allow us to interpret images more easily. There are several types of interpretative cues:

* #### Continuity through occlusion cues
  Sometimes, drawing lines that delineate occlusions or sometimes even occlude an image further can help with inferring an interpretation for the original image.
  
<img src="https://i.imgur.com/j8sACUe.png" alt="drawing" width="300"/>
<img src="https://i.imgur.com/6pDO6SN.png" alt="drawing" width="300"/>

In the first image, it's more difficult to construe the image as a single object, though with some imagination, it's still possible to view the different arrows as corners of a cube. This task becomes much easier when lines are drawn delineating the erased parts of the image; with the new lines, the structure of the cube is much more visible, despite the fact that that no lines were actually drawn to delineate the cube.

<img src="https://i.imgur.com/YUDOqwx.png" alt="drawing" width="350"/><img src="https://i.imgur.com/Ji1cOwQ.png" alt="drawing" width="300"/>

In this image, shading the occluded parts in grey once again helps to make the image as a series of drawn 9s clearer, though the actual image itself remains equally occluded.


* #### Figure-ground discrimination
  Differences between the foreground and the background, particualrly with sharp color contrasts, can aid in image interpretation.
  
<img src="https://i.imgur.com/z1VxxV9.png" alt="drawing" width="300"/>

In this image, the white figure of a lamppost starkly contrasts with the black surroundings, which forms a pair of symmetric faces; this color contrast allows us to interpret the image in two alternate ways depending on which color we treat as the foreground.

# 13.3 Agglomerative Clustering
The concept of the unsupervised learning method clustering is to group given elements $x_1, x_2, \dots, x_n$ into clusters. To do so, there needs to be a specific pairwise association function for the elements in question. When the data points are represented as feature vectors, the most common association functions used for clustering are: 
* #### Euclidean Distance
    Given two elements $x$ and $y$ from the possible elements in the universe, the Euclidean distance between them is defined as: 
        $$ dist(x, y) = \sqrt{\sum (x_i - y_i)^2}$$
        
* #### Cosine Similarity
    Given two elements $x$ and $y$ from the possible elements in the universe, the cosine similarity between them is defined as: 
        $$ sim(x, y) = \cos{\theta} = \frac{x^{\top}y}{\|x\| \cdot \|y\| },$$
        where for any element $a$, $\|a\| = \sqrt{a^{\top}a}$.

### Desirable Properties of clustering algorithms 

The properties desired for a good clustering algorithm include:
    
* Scalability with both time and space
* Adaptable to various data types
* Minimal requirements for domain knowledge to determine input parameters
* Interpretability and usability (should incorprate the user's desired constraints)

### Agglomerative Clustering 
**Workflow**

1.  Consider every point to be its own cluster.


<img src="https://i.imgur.com/Gfbgp7W.png" alt="drawing" width="300"/>

2.  Find the two clusters that have the most \"similarity\" between
    them.

<img src="https://i.imgur.com/BdFvXfb.png" alt="drawing" width="300"/>

3.  Merge the two chosen clusters into one new cluster.


<img src="https://i.imgur.com/9zJMqmo.png" alt="drawing" width="300"/>

4.  Repeat this process.

<img src="https://i.imgur.com/Xth5eno.png" alt="drawing" width="300"/>

5.  As we see here, the next iteration of this process would merge a
    separate point into the cluster made from our first merge.
    
<img src="https://i.imgur.com/xfMmtpH.png" alt="drawing" width="300"/>
    
**Analysis**

1.  How do we define similarity in our previous algorithm? We have
    several options, such as:

    1.  Average distance between points

    2.  Minimum distance

    3.  Maximum distance

    4.  Distance between means or medoids

2.  How many clusters do we have in this algorithm?

    1.  This clustering process creates a dendrogram (essentially, a
        tree diagram). Threshold is based on the maximum number of
        clusters OR based on the distance between merges (diagram shown)
        
        <img src="https://i.imgur.com/MQVpwaB.png" alt="drawing" width="300"/>

3.  The algorithm, officially:

<img src="https://i.imgur.com/OrdM8gy.png" alt="drawing" width="500"/>



### Different Measures of Clustering 
* #### Single Link
    This is equivalent to the minimum spanning tree algorithm. Usually produces long and skinny clusters. You can set a threshold and stop when the distance between clusters is above this threshold. 
        
    $$d(C_i, C_j) = \min_{x \in C_i, x' \in C_j} d(x, x')$$
    <img src="https://i.imgur.com/82aCTWs.png" alt="drawing" width="500"/>

        
        
* #### Complete Link
    Clusters with this type of measure tend to be compact and equal in diameter.
        $$d(C_i, C_j) = \max_{x \in C_i, x' \in C_j} d(x, x')$$
        <img src="https://i.imgur.com/TSyNIvy.png" alt="drawing" width="500"/>

        
        
* #### Average Link
    This is the average distance between elements (between single-linkage and complete-linkage). 
        $$d(C_i, C_j) = \frac{\sum x \in C_i, x' \in C_j d(x, x')}{|C_i| \cdot |C_j|}$$
        <img src="https://i.imgur.com/gjktfa3.png" alt="drawing" width="500"/>

        
| Advantages of agglomerative clustering      | Disadvantages |
| ----------- | ----------- |
| It is simple to implement, with widespread application   | It may have imbalanced clusters |
| The cluster shapes are adaptable | It does not scale well - has a runtime of O($n^3$)       |
| It provides a hierarchy of clusters | You still have to choose the number of clusters or threshold |
| There is no need to specify the number of clusters in advance.  | It can get stuck at a local optima. |



# 13.4 Graph-Based Segmentation

<img src="https://i.imgur.com/ZHtHFXg.jpg" alt="drawing" width="600"/>

<img src="https://i.imgur.com/Ahv5xsA.jpg" alt="drawing" width="600"/>

_The end result of segmentation allows us to group and differentiate distinct clusters of pixels in an image._

### Problem Formulation
We start with a Graph $G = (V, E)$, where $V$ is a set of nodes and $E$ is a set of undirected edges between pairs of pixels. Let's define $w(v_i, v_j)$ as the weight of the edge btween nodes $v_i$ and $v_j$.

$S$ is a segmentation of graph G such that $G' = (V, E')$ where $S$ divides $G$ into G such that it contains distinct clusters $C$. 

<img src="https://i.imgur.com/UibIc12.png" alt="drawing" width="600"/>

In this case, we have 3 distinct clusters.


### Predicate for Segmentation
We will define two functions that we will use for merging clusters (dif and in):



* <img src="https://i.imgur.com/Lg3xQ8R.png" alt="drawing" width=300/>is the minimum difference between a node $v_i$ in cluster $C_1$ and a node $v_j$ in cluster $C_2$.


* <img src="https://i.imgur.com/zgASFB1.png" alt="drawing" width=300/> is maximum internal difference that connects two nodes within each cluster ($C_1$ and $C_2$).
    
Now that we have our two functions, we will use them to determine whether we want to merge two clusters. This is done by the following equation:

<img src="https://i.imgur.com/mjI0jlC.png" alt="drawing" width=600/>


If $dif(C1,C2)$ is less than $in(C1, C2)$, we will merge. Practically speaking, this means that the clusters are very close to each other such that the minimum weighted edge between clusters $C1$ and $C2$ is less than both clusters' max internal weighted edges. 

<img src="https://i.imgur.com/WfawsdA.png" alt="drawing" width=300/>


**Notes on Constant $k$**

* $\dfrac{k}{|C|}$ sets a threshold by which components need to be different from internal nodes.
* If k is large, it causes preference of larger objects since the clusters are more likely to merge.

<img src="https://i.imgur.com/xXBPMGU.png" alt="drawing" width=300/>
<img src="https://i.imgur.com/kUgUg6H.png" alt="drawing" width=300/>


### Features and Weights
To put this algorithm to work, we can now project every pixel into feature space defined by $(x, y, r, g, b)$. Then, we build out a graph where each pixel is connected to its 8 neighboring pixels.

<img src="https://i.imgur.com/Q3ONMgP.png" alt="drawing" width=100/>

Edge weights are determined by difference in intensities by using using L2 norm (Euclidian distance) in the feature space. 

<img src="https://i.imgur.com/x27iFBO.png" alt="drawing"/>

Edges are chosen for only top ten nearest neighbors in feature space to ensure run time of $O(n \log n)$ where $n$ is number of pixels.








