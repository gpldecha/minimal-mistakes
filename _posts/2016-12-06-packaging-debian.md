---
title: "Ubuntu/Debian packaging"
layout: single
author_profile: true
---

**How to package a C++ program into a debian package**

First do all all the steps in:

* [Getting setup](http://packaging.ubuntu.com/html/getting-set-up.html)

I will be doing a walk through of the example given in the  [Packaging New Software](http://packaging.ubuntu.com/html/packaging-new-software.html)
in which you will be deploying a simple hello world program.

I first created a directory hello_package, in my ubuntu package deployment workspace,
and downloaded the hello world program as outlined in [Packaging New Software](http://packaging.ubuntu.com/html/packaging-new-software.html):


```bash
$ pwd
$ /home/username/ubuntu_packaging/hello_package
$ ls
$ hello-2.7  hello-2.7.tar.gz
```
After building hello-2.7 and installing it, I run bzr dh-make

```bash
$ bzr dh-make hello 2.7 hello-2.7.tar.gz
```

which takes the following options:

bzr dh-make PACKAGE_NAME VERSION TARBALL (see [builddeb-plugin](http://doc.bazaar.canonical.com/plugins/en/builddeb-plugin.html))

and creates an additional directory (hello) and new tarball (hello_2.7.orig.tar.gz):

```bash
$ pwd
$ /home/username/ubuntu_packaging/hello_package
$ ls
$ hello  hello-2.7  hello_2.7.orig.tar.gz  hello-2.7.tar.gz
```

After laboriously changing all files in hello/debian as prescribed and building the
debian package more directories are created:

```bash
$ pwd
$ /home/username/ubuntu_packaging/hello_package
$ ls
$ build-area  hello  hello-2.7  hello_2.7-0ubuntu1_amd64.changes  hello_2.7-0ubuntu1_amd64.deb  hello_2.7-0ubuntu1.debian.tar.gz  hello_2.7-0ubuntu1.dsc  hello_2.7.orig.tar.gz  hello-2.7.tar.gz
```
* hello_2.7-0ubuntu1_amd64.changes
* hello_2.7-0ubuntu1_amd64.deb
* hello_2.7-0ubuntu1.debian.tar.gz
* hello_2.7-0ubuntu1.dsc

On launchpad you have to create a new PPA for this project and upload your package to it, see [PPA-Uploading](https://help.launchpad.net/Packaging/PPA/Uploading).
Once this is down you are nearly ready to sudo apt-get install this package. Before this you have to add your ppa to your source packages. I
ran the following command:

```bash
sudo add-apt-repository ppa:gpldecha/ppa-hello
 A simple hello program which displays a greeting.
 More info: https://launchpad.net/~gpldecha/+archive/ubuntu/ppa-hello
Press [ENTER] to continue or ctrl-c to cancel adding it

Error: signing key fingerprint does not exist
```
However it did not work, I got: **Error: signing key fingerprint does not exist**.
This is because you frist have to added the public key of the PPA to your package sources, see [Added key for signed PPA](http://ia800203.us.archive.org/23/items/LaunchpadAddingAPpasKeyToYourUbuntuSystem/launchpad-adding-key-for-signed-ppa.ogv)

## Resources

* [Getting setup](http://packaging.ubuntu.com/html/getting-set-up.html)

* [Packaging New Software](http://packaging.ubuntu.com/html/packaging-new-software.html)

* [Debian dir overview](http://packaging.ubuntu.com/html/debian-dir-overview.html)

* [Packaging PPA](https://help.launchpad.net/Packaging/PPA?action=show&redirect=PPA#Adding%20a%20PPA%20to%20your%20Ubuntu%20repositories)
