# Circuit basics

Now that you have a feeling on how to interact with Gnucap, let's look at some examples for circuit analysis.



## A basic voltage divider

Before you can run a simulation you must enter a netlist into the simulator. There a several ways to load a netlist, depending how big the netlist for simulation is. For small calculations you can run gnucap in "interactive mode". For this, start gnucap from the command line with:

    $ gnucap

For a small circuit you can enter the netlist with the "build" command in gnucap itself:

    gnucap> build

You can directly enter the nodes of the netlist. For example a simple voltage divider:

    * voltage divider
    vi 1 0 1.0
    r1 1 2 10K
    r2 2 0 10K
    *an empty line is needed after this one
 
To check that the netlist is loaded run:

    gnucap> list
    
You should see the netlist:

    gnucap> list
    * voltage divider
    vi ( 1 0 )  DC  1.
    r1 ( 1 2 )  10.K
    r2 ( 2 0 )  10.K

Then calculate the DC operating points:

```
gnucap> probe op V(nodes)
gnucap> op
#           V(1)       V(2)      
 27.        1.         0.5  
```

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

## Simulate a diode

to be discussed

## Simulate transistor

work in progress

### Igs

```
** simulation of pn junction
Vds 1 0 DC +10V
Vgs 2 0 DC +3V
M1 1 2 0 0 nmos_enhance L=10u W=400u

* model statement (Level 1 by default)
.MODEL nmos_enhance nmos (kp=20u Vto=+2 lambda=0)

** output
.print DC V(1) I(Vds)

** analysis
.DC Vds 0V 3V 100mV
``` 

## References

Several tutorials to learn gnucap are available on the internet. A good overview is provided from the [gnucap-examples](http://gnucap.org/dokuwiki/doku.php/gnucap:manual:examples:hello_world) wiki page.
