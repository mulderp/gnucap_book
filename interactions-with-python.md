# Simulate from Python

It is possible to run GnuCAP simulations from Python.

For this, you need to install the Gnucap Python package from Felix Saalfelder. This package can be obtained from: [The Gitlab project](https://gitlab.com/gnucap/gnucap-pytho)

The main project package is located at: [http://gnucap.org/dokuwiki/doku.php/gnucap:user:gnucap\_python](http://gnucap.org/dokuwiki/doku.php/gnucap:user:gnucap_python)

## Build the Python extension

First you need to clone the repo:

    git clone https://gitlab.com/gnucap/gnucap-python

To build the Gnucap Python extension you might to build a recent version of gnucap. You can see a list of recent versions with:

    git tag -l
    git checkout 20171003
    
And repeat the build cycle from Chapter 1.

The Python extension is based on SWIG and the autotools build system

    
    
To build and use the Gnucap module, you should install a at least the numpy package with development headers. In Linux you can simply put a link to these headers in the /usr/include folder as follows:

    # cd /usr/local/include && ln -sf /usr/local/lib/python3.5/dist-packages/numpy/core/include/numpy .
    
Also you might want to install matplotlib package to plot simulation results.


## Simple pulse simulation

```
$ cat > pulse.ckt
spice
v1 (1 0) pulse (0 1)

.print tran v(1)
.tran 0 1 .1
.tran trace all

.end
```

Then run the Python based simulation script:


```
$ cat > sim_pulse.py
import gnucap
from gnucap import command as cmd

cmd("get stuff.sp")
print("listing circuit")
cmd("list")
cmd("store tran v(nodes)")
cmd("transient 1 trace=none > /dev/null") # spice aliases don't work

# bug: does not throw if "v(1)" doesnt exist, (but returns None).
w = gnucap.CKT_BASE_find_wave("v(1)")

for i in w:
        print (i)
```



