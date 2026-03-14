<a id="SECTION000350000000000000000"></a>
<a id="sec:Non-collinear_DFT"></a>
# Non-collinear DFT

<a id="1845"></a>
A fully unconstrained non-collinear density functional theory (DFT)
is supported including
the spin-orbit coupling (SOC) [[8](bibliography.md#Barth),[9](bibliography.md#Kubler),[10](bibliography.md#Sticht),[11](bibliography.md#Oda),[16](bibliography.md#Theurich)].
When the non-collinear DFT is performed, the following option
for the keyword 'scf.SpinPolarization' is available.

```text

   scf.SpinPolarization        NC        # On|Off|NC
```

When the option 'NC' is specified, wave functions are expressed by
a two component spinor. An initial spin orientation of each site
is given by

```text

  <Atoms.SpeciesAndCoordinates           # Unit=Ang
    1  Mn    0.00000   0.00000   0.00000   8.0  5.0  45.0 0.0 45.0 0.0  1 on
    2  O     1.70000   0.00000   0.00000   3.0  3.0  45.0 0.0 45.0 0.0  1 on
  Atoms.SpeciesAndCoordinates>
```

```text

   1:    sequential serial number
   2:    species name
   3:    x-coordinate
   4:    y-coordinate
   5:    z-coordinate
   6:    initial occupation for up spin
   7:    initial occupation for down spin
   8:    Euler angle, theta, of the magnetic field for spin magnetic moment
   9:    Euler angle, phi, of the magnetic field for spin magnetic moment
         Also, the 8th and 9th are used to generate the initial non-collinear 
         spin charge distribution
  10:    the Euler angle, theta, of the magnetic field for orbital magnetic moment
  11:    the Euler angle, phi, of the magnetic field for orbital magnetic moment
  12:    switch for the constraint schemes specified by the keywords 
         'scf.Constraint.NC.Spin', 'scf.NC.Zeeman.Orbital' and 'scf.NC.Zeeman.Orbital'.
         '1' means that the constraint is applied, and '0' no constraint.
  13:    switch for enhancement of orbital polarization in the LDA+U method, 
         'on' means that the enhancement is made, 'off' no enhancement.
```

The initial Euler angles, $\theta$ and $\phi$, for orientation of the spin and orbital
magnetic moment are given by the 8th and 9th columns, and 10th and 11th columns, respectively.
The 12th column is a switch for a constraint scheme that a constraint (penalty or Zeeman)
functional to the spin and orbital orientation is added on each site, where '1' means that
the constraint functional is added, and '0' means no constraint.
For the details of the constraint DFT for the spin orientation, see Sec. [38](constraint-dft-for-non-collinear-spin-orientation.md#sec:Constraint_DFT_for_non-collinear_spin_orientation)
'Constraint DFT for non-collinear spin orientation'.
The final 13th column is a switch for enhancement of orbital polarization in the LDA+U method,
'on' means that the enhancement is made, 'off' no enhancement.
Figure [32](non-collinear-dft.md#fig:NonCol) shows the spin orientation in a MnO molecule calculated
by the non-collinear DFT.
You can follow the calculation using an input file 'Mol_MnO_NC.dat'
in the directory 'work'.
To visualize the spin orientation in real space,
two files are generated:

```text

   System.Name.nc.xsf
   System.Name.ncsden.xsf
```

where *System.Name* means 'System.Name' you specified.
Two files '*System.Name*.nc.xsf' and '*System.Name*.ncsden.xsf' store a projected spin orientation
to each atom by Mulliken analysis and the spin orientation on real space
grids in a vector file format (XSF) supported by XCrySDen.
Both the files can be visualized using 'Display$\to $ Forces' in XCrySDen
as shown in Fig. [32](non-collinear-dft.md#fig:NonCol).

The spin moment and Euler angles of each atom, which are calculated
by Mulliken analysis, are found in the file '*System.Name*.out' as follows:

```text

***********************************************************
***********************************************************
                   Mulliken populations
***********************************************************
***********************************************************

   Total spin moment (muB)   4.998503442   Angles (Deg) 44.991211196   0.000000000

               Up       Down      Sum      Diff        theta      phi
    1   Mn   9.59803  4.76902  14.36705   4.82901    44.99208    0.00000
    2    O   3.40122  3.23173   6.63295   0.16949    44.96650   -0.00000
```

Also it should be noted that it is difficult to achieve a self consistent
field in the non-collinear DFT more than the collinear DFT calculation,
since there are many minima, having almost comparable energy, in the
spin orientation space, while the constraint DFT is useful for such a case.

In the non-collinear DFT, the inclusion of spin-orbit coupling is supported,
while it is not supported for the collinear DFT.
See also the Section 'Relativistic effects' for the issue.

<a id="fig:NonCol"></a>
<a id="1871"></a>
| ![\includegraphics[width=11.0cm]{NonCol.eps}](assets/img193.png) |
| --- |
