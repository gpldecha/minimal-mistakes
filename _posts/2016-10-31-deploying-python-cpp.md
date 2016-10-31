---
title: "Deploying a Python/C++ package"
layout: single
author_profile: true
---

I have written a C++ library for [non-parametric regression](https://github.com/gpldecha/non-parametric-regression). Now C++ is great if you
want to write efficient code, however it is less than ideal when it comes to plotting
and visualising data. For this either Python or Matlab are perfect candidates.

So I have written a Python wrapper to my C++ library with Boost.Python and I want to
deploy.

Here are some use cases which I want my deployed package to fulfill:

* A user can either use the c++ interface or the python interface.
* Easy to install:

```bash
$  pip install npregression
```

or

```bash
$ sudo apt-get install npregression
```

## Approach

Since the C++ library should be completely independent of the wrapper it should
be able to be installed/deployed without the wrapper.

If the wrapper is installed via pip it should first install the C++ library which
is a dependency and then proceed to install the Python wrapper using standard
pip.

## How to deploy a C++ package

## How to deploy a Python wrapper of a C++ library

## Your project is deployed


When a python package when deployed will typically reside on the [Python Package Index](https://pypi.python.org/pypi).



## resources

* [Tutorial on creating a distributable Python package using Setuptools with Boost-Python](http://robotics.usc.edu/~ampereir/wordpress/?p=202)
