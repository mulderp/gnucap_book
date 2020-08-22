
# Getting Started

To run a Gnucap analysis of an electrical circuit, you require a netlist. A netlist is a representation of a circuit and its different components such as voltage sources, resistors or transistors.

Entering a simple netlist and running an analysis is a good start to learn some basic Gnucap commands. Commands can be entered either in interactive or batch simulation mode. If you prefer a GUI to work with a netlist, there exist Gnucap plugins that allow you to capture a netlist and run an analysis with help of external programs such as [Qucs](http://qucs.sourceforge.net/) or [gEda](http://www.geda-project.org/).

The purpose of this chapter however is to look at the most important commands for electrical simulations. After having read this chapter, you should have a feeling on how to write a netlist (a schematic), add probes for an analysis, then run a simulation and capture its output.

Once you are able to load a netlist and start a simulation, the data from a simulation can be plotted with help of the plotting function or a plotting program. This will be discussed at the end of this chapter.


## Overview on Simulator Modes

The interactive mode is helpful for doing small simulations and learning purposes. The interactive mode allows you to "build" a netlist manually by defining nodes and voltage/current sources line by line.

For larger circuits and simulations, you can prepare your simulation in a ckt or spice file. In batch mode, you can load the netlist and run the simulation without manual interventions.

Besides different modes for simulations, Gnucap also supports different formats for defining netlists. This will be discussed below in the Verilog part of the chapter.

Let`s first look at the basics of the interactive mode.


## Interactive Mode

The interactive mode will be started if you run Gnucap without arguments:

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

Take a look below for a very basic build example:

```
gnucap> build
Vsrc 1 0 5
Rload 1 0 1k
<empty line>
```

Note the empty line to end "building" the netlist. You can later add new components with the "modify" command.

Once you have entered the netlist, you can inspect the netlist with "list":

```
gnucap> list
Vsrc ( 1 0 )  DC  5.
Rload ( 1 0 )  1.K
gnucap>
```

This is a very simple netlist with only 2 components. Let"s see how it can be analyzed.


### Adding probes

To do an analysis, you first need to think what to measure and how. In Gnucap, you need to take a look at the "print" command. In the documentation you will see: "The ‘print’ command selects where to look at the circuit, or where to hook the voltmeter (ammeter, wattmeter, ohm meter, etc.) probe."

If you play with "print" in the Gnucap console you will see:

```
gnucap> print
tran
ac
dc
op
fourier
gnucap> print op
```

The modes for analysis are:

* op: The "op" mode provides a way to get the operation points, or basic voltages and currents in a circuit.
* dc: A DC analysis is made to sweep the voltage or current (or some other parameter) in a circuit. It is basically a loop on "op" an analysis
* ac:  With an AC analysis you can do simulations in the frequency domain, e.g. for looking at filters.
* tran: This mode is for transient simulations. Transient simulations are made to study dynamic behavior of a circuit.
* fourier: TODO

Besides the operation mode, you need to add voltages and currents that you want to observe.
For example, you can add all voltages in the circuits as follows:

```
gnucap> print op v(nodes)
```

If you now type again "print" without arguments you will see a first probe:

```
gnucap> print
tran
ac
dc
op      v(1)
fourier
gnucap>
```

This means there will be one voltage probe on node 1. Similarly you can add probes for a current in the resistor component for example:

```
fourier
gnucap> print op v(nodes) i(rload)
gnucap> print
tran   
ac     
dc     
op      v(1) i(rload)
```

### Basic simulations

Now you can run an analysis such as "op" or "dc" to run different simulations. Operating points (or "op" simulations) are often helpful to get a first idea of where electrical charge moves inside a circuit.

For the basic netlist so far the result is not very surprising:


```
gnucap> op
#           v(1)       i(rload)  
 27.        5.         0.005  
```

Gnucap took 27 iterations to solve the voltage and currents in the circuit.


To see how charge moves with respect to changes in an electrical component (e.g. voltage of the voltage source), it is possible to do a DC sweep. First enter nodes for dc observation with:

 ```
gnucap> print dc i(rload)
 ```

Then start the sweep with:

 ```
gnucap> dc vsrc 0 3 0.5
#           i(Rload)
 0.         0.
 0.5        500.u
 1.         0.001
 1.5        0.0015
 2.         0.002
 2.5        0.0025
 3.         0.003
 ```

To capture outputs of an analysis you can use the ">" redirect:

```
gnucap> dc vsrc 0 3 0.5 > mydata.txt
```

Now data that would otherwise be printed will end up in a file. The file is not CSV format, but in a format that gnuplot and gwave can read.

## Plotting data

There are a number of ways to plot data from an analysis.
The fastes way to see a graphical result of a simulation is with the "plot" command.

### Gnucap plot command

```
plot dc v(1)(0,1) v(2)(0,1)
```
(todo discuss terminal output formatting)

However for higher resolution plots, it can help to install a waveform view or gnuplot.

### Gwave

A free waveform viewer is [gwave](http://gwave.sourceforge.net/)
(todo discuss installation of gwave)


### Gnuplot

you can plot the data with gnuplot for example:

```
$ gnuplot

        G N U P L O T
        Version 5.2 patchlevel 2    last modified 2017-11-15

        Copyright (C) 1986-1993, 1998, 2004, 2007-2017
        Thomas Williams, Colin Kelley and many others

        gnuplot home:     http://www.gnuplot.info
        faq, bugs, etc:   type "help FAQ"
        immediate help:   type "help"  (plot window: hit 'h')

Terminal type is now 'qt'
gnuplot> plot "mydata.txt" using 1:2
```

You now should see a simple resistor curve:

![Basic plot of a DC sweep](images/sim1.png =192x102)

## Batch Mode

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

Notes from Felix in mailing list:
the "set lang verilog" command hands over the input parsing to the verilog language plugin. as you might have found, the shipped version of this plugin essentially implements netlisting (some paramset and device instanciation), and running commands (not part of standard verilog). the wire, and register commands as well as the events in verilog are used in, or to describe, component models.

generating component models is more involved. a possible approach is to turn a model description into a plugin written in a programming language. another approach is to interpret the model or use some intermediate bytecode whatosoever. there is a tradeoff between speed and other things such as (maybe) flexibility.

we have a model compiler "modelgen" that reads models, in a language that predates verilog. it writes plugins written in C++ and it is limited to analog component models.  E.g. the built-in semiconductor models are partly implemented in modelgen langage. The intent and plan is to also support a sensible subset of verilog-a in a modelgen style compiler. and then possibly include the digital/mixed modelling features you mention. it is not there yet [1].

somewhat independently, i have started the logic device rewrite with the aim to support verilog-ams "connectmodule" semantics. this will provide custom mixed signal behavioural models -- limited to C++ (probably also Python) implementations at the moment ([2], there is something on the mailing list about it). it's all plugins. perhaps they should be standalone and/or part of gnucap-python...

```
 gnucap-spice>.dc vsrc 0 1 .1 | ./postprocess.sh
```


## Notes on storing data

Gnucap has some plugins under development that can improve how you can capture data. You could use a small class as in [dataparse.py](https://codeberg.org/gnucap/gnucap-python/src/branch/develop/examples/dataparse.py) to read it from within Python.  
Y
You could write a small program that converts to some other format, and
run it as in

```
gnucap> transient 1 2 3 | anyprogram
```

Be warned this is a work in progress feature -- passing arguments or redirecting further seems not implemented, ...

Some day, the output-pluggability will allow to do pretty much exactly what you are suggesting. there is a demo [hdf command](https://git.savannah.gnu.org/cgit/gnucap.git/log/?h=hdf-14) which shows the intended use. A demo command syntax is something like

```
gnucap> hdfprobe tran v(nodes)
gnucap> tran 1 2 3.
```

a similar plugin could then implement CSV.


