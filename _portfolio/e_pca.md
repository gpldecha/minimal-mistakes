---
title: E-PCA
permalink: /projects/e-pca/
excerpt: A matlab (E)xponential-PCA package for non-linear dimensionality reduction. 
header:
  teaser:  /projects/e_pca/reconstructed_belief.gif
sidebar:
  nav: "docs"
---

E-PCA is a non-linear dimensionality reduction technique particularly suited
to probability distributions, see the paper [Exponential Family PCA for Belief Compression
in POMDPs](http://www.cs.cmu.edu/~ggordon/nickr-ggordon.nips02.pdf).

* [Matlab implementation of E-PCA](https://github.com/gpldecha/e-pca).

The left figure illustrates a filtered 2D probability distribution of an agent's location in a square world with a red block (goal state) at its center. The right figure is the result of the probability density function being reconstructed after a latent lower dimensional space was leaned via E-PCA.

{% include gif.html
           gif="/projects/e_pca/original_belief.gif"    
           title="Original beliefs"
%}

{% include gif.html
           gif="/projects/e_pca/reconstructed_belief.gif"    
           title="Reconstructed beliefs"
%}

In the above animation the original dimension of the probability distribution is 625 and the learned E-PCA latent space
has 8 dimensions. This is a very large compression, we went from 625 dimensions to 8 and as we can see the reconstructed probability distributions (right) are very similar to the original distributions (left).

The optimisation to find the latent space feature space is convex and can be solved though Newton's methods. The matalab implementation follows closely the aglorithm details given in the paper [Finding Approximate POMDP Solutions Through Belief
Compression](https://arxiv.org/pdf/1107.0053.pdf), see page 14.
