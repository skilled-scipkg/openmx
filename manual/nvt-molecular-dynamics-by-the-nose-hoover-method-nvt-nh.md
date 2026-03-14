<a id="SECTION000183000000000000000"></a>
## NVT molecular dynamics by the Nose-Hoover method (NVT_NH)

<a id="1153"></a>
The Nose-Hoover molecular dynamics [[31](bibliography.md#NH)]
is supported to perform NVT ensemble molecular dynamics simulations
by the following keyword:

```text

    MD.Type         NVT_NH     # NOMD|Opt|NVE|NVT_VS|NVT_NH
```

Then, in this NVT molecular dynamics
the temperature for nuclear motion can be controlled by

```text

   <MD.TempControl
     4
     1    1000.0
     100  1000.0
     400   700.0
     700   600.0
   MD.TempControl>
```

The beginning of the description must be '$<$MD.TempControl', and
the last of the description must be 'MD.TempControl$>$'.
The first number '4' gives the number of the following lines
to control the temperature. In this case you can see that
there are four lines. Following the number '4',
in the consecutive lines the first and second columns
give MD steps and a given temperature for nuclear motion.
The temperature between the MD steps is given by a linear interpolation.
Although the same keyword 'MD.TempControl' as used in the
velocity scaling MD is utilized in this specification, it is noted
that the format is different from each other.
In addition to the specification of 'MD.TempControl',
you must specify a mass of heat bath by the following keyword:

```text

    NH.Mass.HeatBath          30.0      # default = 20.0
```

The dimension is length$^2$ $\times $ mass.
In this specification we use the bohr radius for the length, and
the unified atomic mass unit, that the principal isotope of carbon atom is 12.0,
for the mass.
Calculated quantities at every MD step are stored in an output
file '*System.Name*.ene' as explained in 'NVT molecular dynamics by a velocity
scaling'.
As an example, we show a result for Nose-Hoover MD
of a glycine molecule in Fig. [12](nvt-molecular-dynamics-by-a-velocity-scaling-nvt-vs.md#fig:Gly_MD) (b).
We see that the temperature in the molecule oscillates
around the given temperature.
Also for visualization of molecular dynamics,
an output file '*System.Name*.md' can be easily animated using free software
such as OpenMX Viewer [[152](bibliography.md#YTL-OpenMX-Viewer),[151](bibliography.md#OpenMX-Viewer)] and XCrySDen [[105](bibliography.md#XCrySDen)] as well as NVT_VS.
