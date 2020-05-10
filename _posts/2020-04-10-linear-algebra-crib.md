---
layout: post
title: Linear algebra crib
description: Linear algebra for data science
published: true
future: true
mathjax: true
---

These are my crib notes for the key linear algebra topics for the [MIT Opencourseware course Matrix Methods in Data Analysis, Signal Processing, and Machine Learning.](https://ocw.mit.edu/courses/mathematics/18-065-matrix-methods-in-data-analysis-signal-processing-and-machine-learning-spring-2018/) The accompanying text for this course is [Linear algebra and learning from Data](https://math.mit.edu/~gs/learningfromdata/) which I think is a rather good breeze through all the things one needs to know to do data science. I take no responsibility for the ideas on this page, they are all the fault of the sources that I've linked to.

# Summary

Linear algebra has many different matrices, but positive definite symmetric matrices $ S $ are the best ones as they have positive eigenvalues $ \lambda $ and orthogonal eigenvectors $ q $. $ S $ matrices are combinations $ S = \lambda_1 q_1 q_1^T + \lambda_2 q_2 q_2^T ... $ of simple rank-one projections $qq^T$ onto those eigenvectors.

If $\lambda_1 \geq \lambda_2 \geq \lambda_2 ... $ then $ \lambda_1 q_1 q_1^T$ is the most informative part of $S$. For a sample covariance matrix this part has the greatest variation.

These ideas are extended from symmetric matrices to all matrices using the singular value decomposition (SVD). The matrix $A$ is decomposed into two sets of singular vectors $u$s and $v$s and singular values $\sigma$ replace eigenvalues $\lambda$.

$$ A = \sigma_1 u_1 v_1^T + \sigma_2 u_2 v_2^T + ... $$

$$ A = U \Sigma V^T $$

With decreasing $ \sigma $'s those rank-one pieces of $A$ still come in order of importance. The "Eckart-Young Theorem" about $A$ complements what we know about the symmetric matrix $A^T A$: for rank $k$, stop at $ \sigma_k u_k v_k^T$.

# Topics covered in P1 of LADA

1. Multiplication $Ax$ using columns of $A$
1. Matrix-Matrix multiplication $ \boldsymbol{AB}$
1. The four fundamental subspaces
1. Elimination and $ \boldsymbol{A = LU} $
1. Orthogonal matrices and subspaces
1. Eigenvalues and eigenvalues
1. Symmetric positive definite matrices
1. Singular values and singular vectors in the SVD
1. Principal components and the best low rank matrix
1. Norms of vectors and functions and matrices