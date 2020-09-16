# Components

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
