# Flush Attacks

Cache side channel attacks that mainly use time of
execution of some operations to gather information
about other processes in the system.

# Flush-Cli

Simple command line interface to perform Flush+Flush
or Flush+Reload side channel attacks.

## Build

In the `flush-cli/` folder you can use `make` to build
the program.

## Use

```
./flush-cli fr /usr/lib/x86_64-linux-gnu/gnome-calculator/libcalculator.so 0x27550 1.0
```

Will notify you in the terminal every time the `math_equation_get_variables` function
is called. This function is called by the `gnome-calculator` application everytime
we launch it or hit a button. This will be done using the Flush+Reload attack, hence
the `fr` argument.

```
./flush-cli ff /usr/lib/x86_64-linux-gnu/libkdeinit5_kcalc.so 0x456f0 1.0
```

Will notify you in the terminal every time the `kdemain` function is called. This
function is called by the `kcalc` calculator everytime it is launched.
It uses the Flush+Flush attack, hence the `ff` argument.

```
./flush-cli ff /lib/x86_64-linux-gnu/libQt5Gui.so.5 0x1229c0 1.0
```

Will notify you in the terminal every time the `processKeyEvent` function
from the `QGuiApplicationPrivate` class is called. This
function is called everytime the calculator is launched.
It uses the Flush+Flush attack, hence the `ff` argument.


### Arguments

```
./flush-cli <attack type> <file> <offset> <sensibility>
```

* **Attack Type** - `ff` for Flush+Flush or `fr` for Flush+Reload.

* **File** - The binary you want to monitor.

* **Offset** - The offset in the binary you want to monitor.

* **Sensibility** - A number between 0 and 1. The higher the sensibility
the less false hits you will get, at the cost of possibly having
less true hits.

### Threshold

The program finds a timestamp range in which hits occur during the
pre-attack phase (calibration).
