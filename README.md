This is a work in progress; better README to come soon. Meanwhile:

**Untested hardware and software — Do not assume anything works!**

# Multiples

This is a buffered multiple module in Kosmo format. It provides two buffered multiple circuits each with one input and four outputs; the input to the second is normalized to the input of the first, so it can function as a 1-in, 8-out multiple.

It is intended to be V/oct-safe. Voltage follower stages are used to guarantee unity gain. Input impedance is 1M instead of the common 100k, resulting in attenuation (of a signal from a source with 1k output impedance) by 0.1% rather than 1% — corresponding to 1.2 cents per octave instead of 12. Output current limiting resistors are in the loop, so there will be no attenuation at the downstream input.

Two things to watch out for:

* There are no stabilization capacitors in the design. With the in-the-loop resistor, the potential exists for op amp instability when driving a capacitive load. In practice this probably means don't use 20 meter long patch cords on the outputs. In more normal usage there is not likely to be a problem.
* Use of JFET op amps (TL074) in voltage followers rather than paired inverting stages means there can be phase reversal if the input signal is less than 4 V from the negative rail, giving incorrect outputs. If your inputs might go more negative than -8 V, use a different multiple. There also is no protection against overvoltage outside the ±12 V range, so exercise care not to connect anything that might give such large voltages.

## Current draw
?? mA +12 V, ?? mA -12 V


## Photos

![]()

![]()

## Documentation

* [Schematic](Docs/multiples.pdf)
* PCB layout: [front](Docs/multiples_layout_front.pdf), [back](Docs/multiples_layout_back.pdf)
* [BOM](Docs/multiples_bom.md)
* [Build notes](Docs/build.md)
* [How it works](Docs/howitworks.md)
* [Blog post]()

## GitHub repository

* [https://github.com/holmesrichards/multiples](https://github.com/holmesrichards/multiples)

## Submodules

This repo uses submodules aoKicad and Kosmo_panel, which provide needed libaries for KiCad. To clone:

```
git clone git@github.com:holmesrichards/multiples.git
git submodule init
git submodule update
```


Alternatively do

```
git clone --recurse-submodules git@github.com:holmesrichards/multiples.git
```

Or if you download the repository as a zip file, you must also click on the "aoKicad" and "Kosmo\_panel" links on the GitHub page (they'll be in the Libraries folder and will have "@ something" after them) and download them as separate zip files which you can unzip into this repo's aoKicad and Kosmo\_panel directories (in the Libraries folder).

If desired, copy the files from aoKicad and Kosmo\_panel to wherever you prefer. 

Then in KiCad, go into Edit Symbols and add symbol libraries 

```
aoKicad/AO_symbols
Kosmo_panel/Kosmo
```
and go into Edit Footprints and add footprint libraries 
```
aoKicad/AO_tht
Kosmo_panel/Kosmo_panel.
```
