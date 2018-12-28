# Gnucap overview

## Building Gnucap from source

You can download gnucap from the Gnu savannah repos:

```text
origin    git://git.savannah.gnu.org/gnucap.git 
```

After running the default build commands:

```text
./configure
./make
```

It might be necessary to reload the shared libraries with:

```text
 ldconfig
 ./configure
```

A good reference is the gnucap build recipe [https://github.com/guitorri/homebrew-tap/blob/master/gnucap.rb](https://github.com/guitorri/homebrew-tap/blob/master/gnucap.rb)

