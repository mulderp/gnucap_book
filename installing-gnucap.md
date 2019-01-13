# Installing Gnucap

There are multiple ways to get Gnucap running. To use the latest features, it is best to install Gnucap from source. Building Gnucap is best on a Linux operating system such as Debian or Ubuntu. To build Gnucap on ohter operataing systems see the last section of this chapter.

## Prerequisites

To build Gnucap from source you need to install a number of buildtools: 

* g++
* the [readline](https://tiswww.case.edu/php/chet/readline/rltop.html) library or debian package `libreadline-dev`
* auto tools
* ...

## Building Gnucap on Linux

You can download gnucap from the [Gnu savannah repo](git://git.savannah.gnu.org/gnucap.git):

```text
git clone git://git.savannah.gnu.org/gnucap.git
```

or


```text
git clone https://git.savannah.gnu.org/r/gnucap
```

This will give you the basic gnucap directory structure:

```text
├── apps
├── include
├── lib
├── main
├── modelgen
└── tests
```

Next, you need to move a recent tag or branch of the project. You can do this with:

    git checkout -b ....
    

The project includes a gnucap shared library gnucap.so, some executables and a number of plugins.

To build of these, you can run the default build commands:

```text
./configure
./make
```

It might be necessary to reload the shared libraries with:

```text
 ldconfig
 ./configure
```

## Other operating systems

To build gnucap on MacOS, a good reference is the gnucap build recipe [https://github.com/guitorri/homebrew-tap/blob/master/gnucap.rb](https://github.com/guitorri/homebrew-tap/blob/master/gnucap.rb)

## Run gnucap

After a successfull build and installation, you should be able to run gnucap like this:

```
~$ gnucap
Gnucap : The Gnu Circuit Analysis Package
Never trust any version less than 1.0
Copyright 1982-2013, Albert Davis
Gnucap comes with ABSOLUTELY NO WARRANTY
This is free software, and you are welcome
to redistribute it under the terms of 
the GNU General Public License, version 3 or later.
See the file "COPYING" for details.
main version: master 2017.10.03
core-lib version: master 2017.10.03
default plugins: master 2017.10.03
```
