<a id="SECTION000174000000000000000"></a>
## Optimization of enthalpy

It is possible to perform the variable cell optimization under an applied pressure.
This is done by minimizing the enthalpy $H$ defined with

| $\displaystyle H = E + pV,$ |  |  | (1) |
| --- | --- | --- | --- |

where $E$ is the total energy of system per unit cell, $p$ is the applied pressure, and $V$ is the
volume of the unit cell. To perform the optimization of enthalpy, you only have to include the following
keyword in your input file:

```text

   MD.applied.pressure         10.0       # in GPa, default=0
```

The positive pressure corresponds to the compression of cell.
The functionality is compatible with 'OptC1', 'OptC2', 'OptC3', 'OptC4', 'OptC5', 'OptC6', 'OptC7',
and 'RFC5', 'RFC6', and 'RFC7' which can be specified by the keyword 'MD.Type'.
As an example, one can perform the enthalpy optimization using an input file 'Si8-pV.dat' stored
in the directory 'work', which is for the optimization of Si crystal under 10 GPa.
After the calculation, you may find the history of the optimization
in the out file 'si8-pV.out' as follows:

```text

***********************************************************
                History of cell optimization               
***********************************************************
***********************************************************

MD_iter   SD_scaling     |Maximum force|   Maximum step        Utot             Enpy           Volume
                         (Hartree/Bohr)        (Ang)         (Hartree)        (Hartree)        (Ang^3)

 1       1.25981732       0.07663140       0.05108760     -32.84057849     -32.47335956     160.10300700
 2       1.25981732       0.06717954       0.04478636     -32.84541333     -32.48138995     158.70978745
 3       1.25981732       0.05879663       0.03919775     -32.84853574     -32.48736913     157.46427382
 4       1.25981732       0.05131728       0.03421152     -32.85047522     -32.49182806     156.36581813
 5       3.14954331       0.04468030       0.07446716     -32.85159836     -32.49515060     155.40690918
 6       3.14954331       0.02956430       0.04927383     -32.85232293     -32.50062291     153.33695214
 7       3.14954331       0.01960389       0.03267316     -32.85158714     -32.50293764     152.00696345
 8       3.14954331       0.01318467       0.02197446     -32.85069024     -32.50392104     151.18717226
 9       7.87385828       0.00909382       0.03789092     -32.84998761     -32.50434789     150.69473500
10       7.87385828       0.00253118       0.00537839     -32.84867882     -32.50470324     149.96919000
11       7.87385828       0.00198428       0.03321825     -32.84877730     -32.50477155     149.98234416
12       7.87385828       0.00271856       0.01866538     -32.84922787     -32.50499775     150.08016284
13       7.87385828       0.00086782       0.00943670     -32.84942256     -32.50507226     150.13256385
14       7.87385828       0.00077020       0.00982293     -32.84949585     -32.50509162     150.15607426
15       7.87385828       0.00020223       0.00270074     -32.84950610     -32.50511244     150.15146767
16       7.87385828       0.00005544       0.00000000     -32.84950546     -32.50511390     150.15055140
```

It can be confirmed that the enthalpy is actually optimized with shrinking of the volume rather
than the total energy.

Also, one can apply the pressure to only designated axes in orthorhombic crystal systems
by the following keyword:

```text

   MD.applied.pressure.flag   1 1 1   # default=1 1 1
```

The default setting is '1 1 1' which means that the isotropic pressure is equally applied
along the **a**-, **b**-, and **c**-axes.
When you specify the keyword as '1 0 0', the pressure is applied along only the **a**-axis
which is the direction perpendicular to the **bc**-plane in orthorhombic crystal systems.
The functionality is valid for
orthorhombic crystal systems, and in this case you need to provide the unit vectors such as

```text

    <Atoms.UnitVectors
     10.000   0.000   0.000
      0.000   8.000   0.000
      0.000   0.000  11.000
    Atoms.UnitVectors>
```

so that the non-zero elements can be diagonal.
Apart from the orthorhombic crystal systems, one may apply the anisotropic pressure along
an lattice vector perpendicular to the plane defined by the other lattice vectors.
The case can be found in cases such as hexagonal crystal systems, and you may specifiy these keywords
as follows

```text

   MD.applied.pressure.flag   0 0 1   # default=1 1 1
```

```text

    <Atoms.UnitVectors
      6.000   0.000   0.000
     -3.000   5.196   0.000
      0.000   0.000  10.000
    Atoms.UnitVectors>
```
