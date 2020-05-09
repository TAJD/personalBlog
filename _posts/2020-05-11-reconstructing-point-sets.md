---
layout: post
title: Reconstruct point set from Euclidean Distance Matrix
description: Solving a simple problem using code because I doubted myself.
published: true
future: true
mathjax: true
---


This post is motivated by my desire to understand how to recover point locations given a Euclidean Distance Matrix. I took some time to understand the explanation in [Linear Algebra and Learning from Data](https://math.mit.edu/~gs/learningfromdata/) and [this paper](https://arxiv.org/pdf/1502.07541.pdf) so I decided to write up the solution of a problem. The desire to reconstruct point sets from EDMs occurs in areas such as ultrasound tomography and others which involve attempting to reconstruct the location of recording devices given the recorded signals. I have no doubt there are many others.

The general question can be phrased as: __How to reconstruct the locations of the original vectors given the Euclidean distance matrix, $D$?__ 

The key assumption is that the distances in $D$ satisfy the triangle inequality, which means that there will always be a position matrix $X$. $X$ has $d$ rows when the points are in $d$-dimensional space. Once the point set has been identified it is possible to align the point set with known locations using Procrustes analysis - also known as the Orthogonal Procrustes problem.

# Theory

This procedure is summarised from [this paper](https://arxiv.org/pdf/1502.07541.pdf). This method is known as _classical MDS_ and can be developed to consider real world problems, for example, those with noise.

Consider a collection of $n$ points in a $d$-dimensional Euclidean space. The squared distance between points $x_i$ and $x_j$ is $d_{ij}$ and is calculated using:

$$ d_{ij}= \lvert\lvert x_i - x_j \rvert\rvert^2$$

Expanding this norm yields:

$$d_{ij}=(x_i - x_j)^T(x_i - x_j) = x_i^T x_i - 2x_i^T x_j + x_j^T x_j$$

The matrix equation for the distance matrix $D=[d_ij]$ is calculated using:

$$edm(X)=\mathit{1} \text{diag}(X^TX)^T - 2X^TX + \text{diag}(X^T X)\mathit{1}^T$$

$\mathit{1}$ is the column vector of all ones and $diag(A)$ is a column vector of the diagonal entries of $A$.

The operator $\kappa (G)$ is defined which is equivalent to $edm(X)$ that operates directly on the Gram matrix $G=X^T X$. This now gives the equation below:

$$\kappa (G) = diag(G)\mathit{1}^T - 2G + \mathit{1} diag(G)^T$$

Let the first point $x_1$ be the origin, then the first column of $D$ contains the squared norms of the point vectors,

$$d_{i1} = \lvert\lvert x_i - x_1 \rvert\rvert^2= \lvert\lvert x_i - 0 \rvert\rvert^2 == \lvert\lvert x_i \rvert\rvert^2$$

It is now possible to construct the term $diag(G)\mathit{1}^T$ and its transpose in the equation to calculate $\kappa (G)$.

The Gram matrix $G$ can now be found from $\kappa (G)$ like so:

$$X^T X=G=-\frac{1}{2}\big(D-\mathit{1}d_1^T-d_1\mathit{1}\big)$$

The final stage is to identify the point set using Eigenvalue Decomposition (EVD), for example:

$$G =U\Lambda U^T$$

Remember that $\Lambda = diag(\lambda_1, ...,\lambda_n)$


```python
import numpy as np; import matplotlib.pyplot as plt
from scipy.spatial import distance_matrix
from scipy.spatial.distance import cdist
```



## Example problem

This problem is Q5 from Problem Set $VII.1$ from the [Linear Algebra and Learning from Data](https://math.mit.edu/~gs/learningfromdata/) textbook. Given a Euclidean distance matrix, $D$, find the locations of the points:

$D = \begin{bmatrix}0 & 9 & 25 \\\9 & 0 & 16 \\\25 & 16 & 0\end{bmatrix}$

```python
D = np.array([[0, 9, 25], [9, 0, 16], [25, 16, 0]])
```

Calculate the Gram matrix (I hope that it is positive semidefinite but it is possible to check this: J. C. Gower, “Euclidean Distance Geometry,” Math. Sci., vol. 7, pp. 1–14, 1982.)


```python
G = -0.5*(D-np.outer(np.ones(3), D[1, :])-np.outer(D[:, 1], np.ones(3)))
G
```




    array([[ 9., -0., -0.],
           [-0., -0., -0.],
           [-0., -0., 16.]])



$$G=U\Lambda U^T$$

Use ```np.linalg.svd``` to find out what happens next!


```python
Q, Lambda, _ = np.linalg.svd(G)
print(Q)
print(Lambda)
```

    [[0. 1. 0.]
     [0. 0. 1.]
     [1. 0. 0.]]
    [16.  9. -0.]


Return the original point set: $\hat{X}=\Lambda^{1/2}U^T$


```python
np.power(Lambda, 0.5) * Q.T
```




    array([[0., 0., 0.],
           [4., 0., 0.],
           [0., 3., 0.]])



This makes sense.

There was no need to code this example up - I was just interested in how I would do it in case I needed to do so in anger!

