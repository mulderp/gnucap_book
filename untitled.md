# Circuit basics

Several tutorials to learn gnucap are available on the internet. A good overview is provided from the [gnucap-examples](http://gnucap.org/dokuwiki/doku.php/gnucap:manual:examples:hello_world) wiki page.


## Interactive mode in Gnucap

Before you can run a simulation you must enter a netlist into the simulator. There a several ways to load a netlist, depending how big the netlist for simulation is. For small calculations you can run gnucap in "interactive mode". For this, start gnucap from the command line with:

    $ gnucap

For a small circuit you can enter the netlist with the "build" command in gnucap itself:

    gnucap> build

You can directly enter the nodes of the netlist. For example a simple voltage divider:

    * voltage divider
    vi 1 0 1.0
    r1 1 2 10K
    r2 2 0 10K
 
To check that the netlist is loaded run:

    gnucap> list
    
You should see the netlist:

    gnucap> list
    * voltage divider
    vi ( 1 0 )  DC  1.
    r1 ( 1 2 )  10.K
    r2 ( 2 0 )  10.K

Then calculate the DC operating points:

    * run DC
    .print op v(1) v(2)
    .op
    
And sweep the input voltage for example:

    * run DC sweep
    .width out=80
    
You can plot the results with:

    .plot dc v(1)(0,1) v(2)(0,1)
    .dc vi 0.0 1.0 .1
    .end

