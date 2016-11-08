---
title: "Deploying a Python/C++ package"
layout: single
author_profile: true
---

I have written a C++ library for [non-parametric regression](https://github.com/gpldecha/non-parametric-regression). Now C++ is great if you
want to write efficient code, however it is less than ideal when it comes to plotting
and visualising data. For this either Python or Matlab are perfect candidates.

So I have written a Python wrapper to my C++ library with Boost.Python and I want to
deploy it for the world to use.

Here are some use cases which I want my deployed package to fulfill:

* A user can either use the c++ interface or the python interface.
* It should be easy to install (of course):

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

In my mind a deployed package should be easy to install. As I am predominantly
using Ubuntu I would like to create an Ubuntu package.

* [Getting setup](http://packaging.ubuntu.com/html/getting-set-up.html)

* [Packaging New Software](http://packaging.ubuntu.com/html/packaging-new-software.html)

I encountered problems with dh_install

```bash
$ dh_install: npregression-dev missing files (usr/lib/lib*.so), aborting

```

So I used:

[dh-helper](http://help.ubuntu-it.org/6.06/ubuntu/packagingguide/it/basic-debhelper.html)

### C++ shared library

* The libraries themselves are put into a binary package named libfoo1 where foo is the name of the library and 1 is the version from the SONAME.

* Development files from the package, such as header files, needed to compile programs against the library are put into a package called libfoo-dev.


## How to deploy a Python wrapper of a C++ library

## Your project is deployed


When a python package when deployed will typically reside on the [Python Package Index](https://pypi.python.org/pypi).



## resources

* [Tutorial on creating a distributable Python package using Setuptools with Boost-Python](http://robotics.usc.edu/~ampereir/wordpress/?p=202)
