
# Interactive Gnucap

After a successfull build and installation, you should be able to run gnucap like this:

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
