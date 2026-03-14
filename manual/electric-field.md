<a id="SECTION000280000000000000000"></a>
# Electric field

<a id="1674"></a>
It is possible to apply a uniform external electric field given by
a sawtooth waveform during the SCF calculation and the geometry
optimization. For example, when an electric field of 1.0 GV/m (10$^9$ V/m)
is applied along the **a**-axis, please specify the keyword
'scf.Electric.Field' in your input file as follows:

```text

     scf.Electric.Field   1.0 0.0 0.0   # default=0.0 0.0 0.0 (GV/m)
```

The sign of electric field is taken as that applied to electrons.
If the uniform external electric field is applied to a periodic
bulk system without vacuum region, discontinuities of the potential
are introduced, which may cause numerical instability.
On the other hand, for molecular systems, the discontinuities
are located in the vacuum region, indicating that numerical instability
may not be induced.

As an illustration of the electric field, changes of total charge in
a nitrobenzene molecule induced by the electric field are shown in Fig. [28](electric-field.md#fig:nben_diff).
We can see that a large charge transfer takes place among oxygens
in -NO$_2$, para-carbon atom, and para-hydrogen atom.
The input file is 'Nitro_Benzene.dat' in the directory 'work'.
See also Section [63](analysis-of-difference-in-two-gaussian-cube-files.md#sec:Analysis_of_difference_in_two_Gaussian_cube_files)
'Analysis of difference in two Gaussian cube files'
as for the difference charge maps shown in Fig. [28](electric-field.md#fig:nben_diff).

<a id="fig:nben_diff"></a>
<a id="6283"></a>
| ![\includegraphics[width=18.0cm]{nben_diff.eps}](assets/img187.png) |
| --- |
