
# Interactive Gnucap

You can start Gnucap in interactive or batch mode. The default mode is interactive.

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

To start Gnucap in batch mode add a "-b" flag:

```
gnucap -b <mysim.ckt>
```

There are different extensions such as .ckt or .gc for Gnucap simulations. Gnucap uses .gc for "gnucap" files, to distinguish which ones need -b. A number of examples can be found in the test folder of gnucap gnucap/tests/*.{gc,ckt}. -b switches on a "spice" mode, so in principle you could run the same .ckt files in ngspice and gnucap.

Note that there are different syntax forms for netlist, e.g. Spice, Spectre, ... Also, Verilog simulations can be run with Gnucap.



There is no built-in help. The best place to get information on Gnucap commands is the [documentation](https://www.gnu.org/software/gnucap/gnucap-man.pdf). Also, a number of Gnucap commands can be seen in "c__cmd.cc" :

     build
     delete
     fourier
     generator
     include
     list
     modify
     options
     param
     print
     quit
     status
     temperature
     transient
     system
     <
     >

Commands can be abbreviated with their first letter, e.g. "b" for build.

The first command you want to learn are "build" and "list" to capture nodes of an electrical circuit. Then you can run analysis such as "fourier" for getting frequency data.

Important commands for simulations are "dc" and "probe" commands.
