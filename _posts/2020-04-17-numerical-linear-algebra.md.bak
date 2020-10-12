---
layout: post
title: Numerical linear algebra crib
description: A review of numerical linear algebra for machine learning.
published: true
future: true
mathjax: true
categories: [Maths, Data Science]
---

This crib sheet is based on material from Part 2 of [LALFD](https://math.mit.edu/~gs/learningfromdata/). 


# Solving Least Squares:

Many applications lead to unsolvable linear equations $Ax=b$. The best solution to these equations is $\hat{x}$. 

Least squares chooses $\hat{x}$ to minimise the error $\lvert \lvert b - A \hat{x} \rvert \rvert^2$

Minimising the error means that the derivatives are zero, this leads to the normal equations: $A^T A \hat{x} = A^T b$

There are four ways to calculate $\hat{x}$ as an approximate solution:

1. The singular value decomposition of $A$ leads to its pseudoinverse $A^+$. Then $\hat{x}=A^+b$
1. $A^TA\hat{x} = A^Tb$ can be solved directly when $A$ has independent columns.
1. The Gram-Schmidt idea produces orthogonal columns in $Q$. Then $A=QR$.
1. Minimise $\lvert \lvert b - A \hat{x} \rvert \rvert^2 + \delta^2 \lvert \lvert x \rvert \rvert^2$. The penalty alters the normal equations to $(A_TA + \delta^2 I)x_{\delta} = A^T b$.


# Some useful links for Least squares

- [Normal equations](http://mlwiki.org/index.php/Normal_Equation#Linear_Algebra_Point_of_View)
- [Projections onto vectors](https://en.wikibooks.org/wiki/Linear_Algebra/Orthogonal_Projection_Onto_a_Line)
- [Projections](https://textbooks.math.gatech.edu/ila/projections.html)
