---
title: "Programming notes"
layout: single
author_profile: true
excerpt: "I note book of programming terminology, stuff I always forget"
header:
  overlay_color: "#333"
---

# Row-major

* (memory-layout-of-multi-dimensional-arrays)[http://eli.thegreenplace.net/2015/memory-layout-of-multi-dimensional-arrays/]


# Terminology

### name mangling

Adds meta-data to the name of a function. This process, in the case of C++, takes
place during the compilation. One reason for this is that the compilation process
first converts the C++ code to C and C only allows unique function names throughout
the program.

*resources*:

* [wiki name mangling](https://en.wikipedia.org/wiki/Name_mangling#C.2B.2B)

# C++

* [Example of gtest with travis](https://github.com/bast/gtest-demo)

# Python

## How to  structure a python project

[what-is-the-best-project-structure-for-a-python-application](http://stackoverflow.com/questions/193161/what-is-the-best-project-structure-for-a-python-application)

## How To Package Your Python Code

* [How To Package Your Python Code](https://python-packaging.readthedocs.io/en/latest/)
* [Uploading your project to pypi](https://packaging.python.org/distributing/#uploading-your-project-to-pypi)

## module path system

Important component which will frustrate most beginners if not understood
from the very beginning.

[python-import](https://docs.python.org/3/reference/import.html)

## importing a module into another whilst both are located in different folders

[python-modules-not-found](http://stackoverflow.com/questions/37233140/python-module-not-found)
[importing-modules-from-parent-folder](http://stackoverflow.com/questions/714063/importing-modules-from-parent-folder)
