---
title: "Deploying a Python/C++ package"
layout: single
author_profile: true
---

I have written a C++ library for [non-parametric regression](https://github.com/gpldecha/non-parametric-regression).
Now C++ is great if you want to write efficient code, however it is less than ideal when it comes to plotting
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

## How to deploy a C++ shared library package

I first created a source tar ball for release on [github](https://github.com/gpldecha/non-parametric-regression/releases)
which I downloaded and extracted to my debian packaging work director:

```bash
$ pwd
$ /home/username/ubuntu_packaging/npregression_package
$ ls
$ non-parametric-regression-1.0 non-parametric-regression-1.0.tar.gz
```
I followed the same steps as in my previous post. When I run the command:

```bash
bzr dh-make libnpregression 1.0 non-parametric-regression-1.0.tar.gz
```

I made sure to choose the (l)ibrary option when prompted which type debian
package I wanted. I proceed to build the library,

```bash
./libnpregression$ bzr builddeb -- -us -uc
```
however I encountered the following error:

```bash

dh_install
dh_install: libnpregression-dev missing files (usr/lib/lib*.a), aborting
make: *** [binary] Error 255
dpkg-buildpackage: error: fakeroot debian/rules binary gave error exit status 2
debuild: fatal error at line 1364:
dpkg-buildpackage -rfakeroot -D -us -uc failed
bzr: ERROR: The build failed.

```
There are two important files to edit:

* libnpregression1.install

  usr/lib/npr/lib*.so


* libnpregression-dev.install

usr/include/*


All builds until the next error occurs:

```bash

dh_shlibdeps
dpkg-shlibdeps: error: no dependency information found for /usr/local/lib/libarmadillo.so.5 (used by debian/libnpregression1/usr/lib/npr/liblwr.so)
dh_shlibdeps: dpkg-shlibdeps -Tdebian/libnpregression1.substvars debian/libnpregression1/usr/lib/npr/liblwr.so returned exit code 2
make: *** [binary] Error 2
dpkg-buildpackage: error: fakeroot debian/rules binary gave error exit status 2
debuild: fatal error at line 1364:
dpkg-buildpackage -rfakeroot -D -us -uc failed
bzr: ERROR: The build failed.

```




### C++ shared library

* The libraries themselves are put into a binary package named libfoo1 where foo is the name of the library and 1 is the version from the SONAME.

* Development files from the package, such as header files, needed to compile programs against the library are put into a package called libfoo-dev.


## How to deploy a Python wrapper of a C++ library

## Your project is deployed


When a python package when deployed will typically reside on the [Python Package Index](https://pypi.python.org/pypi).



## resources

[Debian Library Packaging guide](https://www.netfort.gr.jp/~dancer/column/libpkg-guide/libpkg-guide.pdf)

[Tutorial on creating a distributable Python package using Setuptools with Boost-Python](http://robotics.usc.edu/~ampereir/wordpress/?p=202)
