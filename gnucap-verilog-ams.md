# Verilog-AMS mode

Gnucap supports Verilog-AMS syntax. An overview on the Verilog can be found [in the wiki](http://gnucap.org/dokuwiki/doku.php/gnucap:manual:languages:verilog). An overview on Verilog-AMS is [here](https://verilogams.com/) and on the [Accellera website](https://accellera.org/images/downloads/standards/v-ams/VAMS-LRM-2-4.pdf).

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

