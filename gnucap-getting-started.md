
# Simulator modes

You can start Gnucap in interactive or batch mode. For small simulations and learning purposes the interactive mode can be helpful. It allows you to "build" a netlist manually with typine nodes and voltage/current sources.
For larger circuits and simulations the batch mode can be interesting.
Besides different modes for simulations, Gnucap also support different formats for defining netlists. This will be discussed below in the Verilog part of the chapter.


We first will look into the interactive mode.


## Interactive mode

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
gnucap>
```

The gnucap prompt allows you to enter different commands. Unfortunately, there is no built-in help. The best place to get information on Gnucap commands is the [documentation](https://www.gnu.org/software/gnucap/gnucap-man.pdf).

Also, a number of Gnucap commands can be seen in the source file "c__cmd.cc" :

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

The first command you want to learn are "build" and "list" to capture a netlist or the nodes of an electrical circuit.
See below a very basic example:

```
gnucap> build
Vsrc 1 0 5
Rload 1 0 1k
<empty line>
```

Now you can check the netlist was defined with "list":

```
gnucap> list
Vsrc ( 1 0 )  DC  5.
Rload ( 1 0 )  1.K
gnucap>
```

Next you need to think what to measure and how to measure voltages or currents in your circuit. For this, you need to take a look at the "print" command. The print command help is: "The ‘print’ command selects where to look at the circuit, or where to hook the voltmeter (ammeter, wattmeter, ohm meter, etc.) probe."

If you play with it in the Gnucap console you will see: 
```
gnucap> print
tran
ac
dc
op
fourier
gnucap> print op

gnucap> print op v(nodes)
gnucap> print
tran
ac
dc
op      v(1)
fourier
gnucap>
```

This means there will be one probe added to the node 1.


Now you can run an analysis such as "op" or "dc" to run different sweeps. 

```
gnucap> op
#           v(1)
 0.         5.
 1.         5.
```

Later we can look at "fourier" for getting frequency data.

## Batch mode

The same example can be run with batch mode. To start Gnucap in batch mode add a "-b" flag:

```
gnucap -b <mysim.ckt>
```

There are different extensions such as .ckt or .gc for Gnucap simulations. Gnucap uses .gc for "gnucap" files, to distinguish which ones need -b. A number of examples can be found in the test folder of gnucap gnucap/tests/*.{gc,ckt}. -b switches on a "spice" mode, so in principle you could run the same .ckt files in ngspice and gnucap.

Note that there are different syntax forms for netlist, e.g. Spice, Spectre, ... Also, Verilog simulations can be run with Gnucap.




## Verilog mode

Gnucap supports Verilog syntax. An overview on the Verilog can be found [in the wiki](http://gnucap.org/dokuwiki/doku.php/gnucap:manual:languages:verilog)

To switch to the verilog mode, type "verilog" in the first line or in the REPL.

```
param w=2

module m(1,2);
   resistor #(.r(w*5)) r(1,2);
endmodule

m #(.w(w)) m1(0, 1);

// sweep dc voltage
vin  1  0  dc 3

.dc vin 0 5 0.2
```
