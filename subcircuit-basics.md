# Subcircuits

When you look at different functions of an electrical circuit, they are easier to understand by hiding information in a block, or a subcircuit.

The main syntax for a subcircuit is "subckt myckt ... ends ckt".


## A basic example

To understand the syntax for a subcircuit take a look at voltage divider.

Enter the following lines in a file vdiv.ckt:

```
* voltage divider
subckt vdiv in out
vi in 0 1.0
r1 1 out 10K
r2 out 0 10K
ends vdiv
```
 
In Gnucap this subcircuit can be loaded with:

    gnucap> get vdiv.ckt

    
Now you can check that the netlist is loaded:

    gnucap> list
    .subckt vdiv ( in out )
    vi ( in 0 )  DC  1.
    r1 ( 1 out )  10.K
    r2 ( out 0 )  10.K
    .ends vdiv

Now enter a circuit that uses the subcircuit:

    gnucap> b
    >vsrc 1 0 5
    >x1 1 0 vdiv


Then calculate the DC operating points:

```
gnucap> probe op V(nodes)
gnucap> op
#           V(1)       V(2)      
 27.        1.         0.5  
```

### to be removed
As you can see, the voltage on node 2 is half of voltage on node 1. This calculation took 27 internal steps (Todo: check the meaning of # 27.)

And sweep the input voltage for example:

    * run DC sweep
    width out=80
    
You can plot the results with:

    plot dc v(1)(0,1) v(2)(0,1)
    dc vi 0.0 1.0 .1
    
If you would do the process by reading the content of a file where everything is written inside, you would append a dot before each command(except for build) and pass the name of the file with the -b option
    
    #gnucap -b test.ckt
    
the content of the file would be:
```    
    * voltage divider
    vi 1 0 1.0
    r1 1 2 10K
    r2 2 0 10K
    .probe op V(nodes)
    .op
    .width out=80
    .plot dc v(1)(0,1) v(2)(0,1)
    .dc vi 0.0 1.0 .1
    .end
```    
Note that a there's a end command. It simple tells the program that it have done his job.

