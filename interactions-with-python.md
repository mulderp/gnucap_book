# Simulations with Python

It is possible to run GnuCAP simulations from Python.

For this, you need to install the Gnucap Python package from Felix Saalfelder. This package can be obtained from: [The Gitlab project](https://gitlab.com/gnucap/gnucap-pytho)

The main project package is located at: [http://gnucap.org/dokuwiki/doku.php/gnucap:user:gnucap\_python](http://gnucap.org/dokuwiki/doku.php/gnucap:user:gnucap_python)

## Build the Python extension

First you need to clone the repo:

    git clone https://gitlab.com/gnucap/gnucap-python

To build the Gnucap Python extension you might to build a new version of gnucap. You can see a list of recent versions with:

    git tag -l
    git checkout 20171003
    
And repeat the build cycle from Chapter 1.

The Python extension is based on SWIG and the autotools build system

    
    
To build and use the Gnucap module, you should install a number of other Python package:

* numpy
* matplotlib

