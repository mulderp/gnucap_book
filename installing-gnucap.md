# Installing Gnucap


There are multiple ways to get Gnucap running.
To use the latest features, it is best to install Gnucap from source.
Building Gnucap is best on a Linux operating system such as Debian or Ubuntu. To build Gnucap on ohter operataing systems see the last section of this chapter.

## Prerequisites


## Building Gnucap on Linux

You can download gnucap from the [Gnu savannah repo](git://git.savannah.gnu.org/gnucap.git):

```text
git clone git://git.savannah.gnu.org/gnucap.git
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


