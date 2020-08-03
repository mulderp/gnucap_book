
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

Note that there are different syntax forms for netlist, e.g. Spice, Spectre, ... Also, Verilog simulations can be run with Gnucap.



There is no built-in help. A number of Gnucap commands can be seen in "c__cmd.cc" :

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
