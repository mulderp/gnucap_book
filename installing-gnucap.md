# Installing Gnucap

There are pre-built binaries of Gnucap availabe if you search for them. However, to use the latest features, it is best to install Gnucap from source. Many EDA software tools have been written on a Linux operating system. So is Gnucap. It is easy to build Gnucap on system such as Debian or Ubuntu. To build Gnucap on other operating systems (for example MacOS or Windows) see the last section of this chapter.

## Prerequisites

To build Gnucap from source you need to install a number of buildtools and libraries: 

* A modern g++ compiler
* Auto tools or CMake build tools
* The [readline](https://tiswww.case.edu/php/chet/readline/rltop.html) library or debian package `libreadline-dev`
* termcap library to interact with rendering characters to a terminal

If you want to build Gnucap with CMake, you need:
* CMake 3.12 (or later)
* A build system generator such as Make or [Ninja](https://ninja-build.org/)

## Building Gnucap on Linux

You can build Gnucap with help of autotools or CMake build tools.
A short overview can be seen in the [Gnucap wiki](http://gnucap.org/dokuwiki/doku.php/gnucap:manual:autotools)

If you are on a new system, you should install the dependencies first:

An example on OpenSuse would like as:


```
# zypper install readline-dev
# zypper install termcap
```

Then for Gnucap, you can download its source from the [Gnu savannah repo](git://git.savannah.gnu.org/gnucap.git):

```text
git clone git://git.savannah.gnu.org/gnucap.git
```

or from the URL with https if your network does support that better:


```text
git clone https://git.savannah.gnu.org/r/gnucap
```

This will give you the basic Gnucap directory structure:

```text
        ./apps
        ./include
        ./lib
        ./main
        ./modelgen
        ./tests
```

As you will learn later, the architecture of Gnucap is based heavily on plugins. The apps and libs folder include a set of plugins. 
Gnucap consists of a set of models for simulations, simulation algorithms and a user interface. The main user interface is in the main folder. Modelgen is a utility to translate electrical components into models for simulation with Gnucap.

To build Gnucap, you should move to a recent tag or branch of the project. You can do this with:

    git checkout -b <tag_or_branch>

You can see a list of tags with:
  
    git tag -l

Or you can see the branches with:

    git branch -a

For example, you can build the version "20171003" tag or cmake-4 branch.
    
The build process of gnucap will give some executables and some shared libraries such as gnucap.so (or .dll on Windows).

To build of these, you can run the default build commands:

```text
./configure
./make
./make install

For a CMake based build look below.
```

Before you can start Gnucap, it might be necessary to reload the shared libraries with:

```text
 ldconfig
 ./configure
```

And set the Gnucap plugin path to your path that has gnucap-default-plugins.so 

For example:

```
export GNUCAP_PLUGPATH=/usr/local/lib64/gnucap/

```


## Other operating systems

To build gnucap on MacOS, a good reference is the gnucap build recipe [https://github.com/guitorri/homebrew-tap/blob/master/gnucap.rb](https://github.com/guitorri/homebrew-tap/blob/master/gnucap.rb)

## Building with CMake

It is possible to build GnuCap with CMake. This approach can also be used on Windows with Cygwin and MinGW for example:

```
mkdir build
cd build
cmake -G Ninja ..
ninja all
```

In this case, the [Ninja](https://ninja-build.org/) build tool is selected. You can also select Make if you prefer.

One example configuration run is shown below

```
-- The CXX compiler identification is GNU 9.1.0
-- Check for working C compiler: C:/msys64/mingw64/bin/cc.exe
-- Check for working C compiler: C:/msys64/mingw64/bin/cc.exe -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: C:/msys64/mingw64/bin/c++.exe
-- Check for working CXX compiler: C:/msys64/mingw64/bin/c++.exe -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Found Git: C:/Program Files/Git/bin/git.exe (found version "2.21.0.windows.1")
CMake Warning (dev) at CMakeLists.txt:33 (if):
  Policy CMP0064 is not set: Support new TEST if() operator.  Run "cmake
  --help-policy CMP0064" for policy details.  Use the cmake_policy command to
  set the policy and suppress this warning.

  TEST will be interpreted as an operator when the policy is set to NEW.
  Since the policy is not set the OLD behavior will be used.
This warning is for project developers.  Use -Wno-dev to suppress it.

-- Looking for readline in readline
-- Looking for readline in readline - found
-- Looking for tgetent in termcap
-- Looking for tgetent in termcap - found
-- Looking for dlopen
-- Looking for dlopen - not found
...
```

Now the build starts and you will get a library: libgnucap.dll and two main files:

* modelgen
* gnucap executables

However, when you start gnucap you might see an error such as:

```
gnucap
plugpath: PLUGPATH=/usr/local/lib/gnucap
Gnucap : The Gnu Circuit Analysis Package
...
main version: cmake-2 2017.10.18
core-lib version: cmake-2 2017.10.18
/usr/local/lib/gnucap
gnucap-default-plugins.dll
load gnucap-default-plugins.dll
     ^ ? plugin debug (gnucap-default-plugins.dll ) not found in /usr/local/lib/gnucap
```

You need to provide a path the gnucap plugin dll.
Also, you need to set the environment variable:

```env
set GNUCAP_PLUGPATH=C:\Users\pm\git\gnucap\build\main
```

Sometimes you also must have the dll and executable in the same directories.

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


