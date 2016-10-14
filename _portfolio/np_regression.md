---
title: Non-parametric regression
permalink: /projects/np_regression/
excerpt: A set of regression methods written in C++ with a Python interface.

header:
  teaser:  /projects/np_regression/lwr-2D-th.png
sidebar:
  nav: "docs"
---

{% include image.html
           img="/projects/np_regression/lwr-2D.png"
           bbox="false"
%}

* github repository: [non-parametric-regression](https://github.com/gpldecha/non-parametric-regression)

This package provides a set of non-parametric methods for regression. The algorithmic implementation of the methods are in C++ whilst the interface
is in Python. Non-parametric regression methods typically retains all the training data. The value of a new test point is a function of the neighboring points in the input space. As a result it is essential to use a fast space partition method, such as FLANN. Current implemented method are:

* Locally Weighted Regression (LWR)
