<a id="SECTION000452000000000000000"></a>
## Analysis

**Plotting interpolated band structure**

<a id="3147"></a>
To plot the interpolated band structure, set
'Wannier.Interpolated.Bands'
to be 'on'.

```text

     Wannier.Interpolated.Bands             on    # on|off, default=off
```

Other necessary settings, like k-path and sampling
density along each path, are
borrowed from those for plotting band dispersion in OpenMX.
Therefore, the keyword 'Band.dispersion' should be set as 'on'
in order to draw interpolated band structure.
After convergence, interpolated band dispersion data will
be found in a file with the extension name '.Wannier_Band',
which has the same format as '.Band' file. As an example, the interpolated
band structure of Si in diamond structure is shown together with its
original band structure in Fig. [47](maximally-localized-wannier-function-analysis.md#fig:Wannier_Si)(a).

<a id="fig:Wannier_Si"></a>
<a id="3157"></a>
| ![\includegraphics[width=15.0cm]{Wannier_Si.eps}](assets/img348.png) |
| --- |

**Plotting MLWF**

<a id="3161"></a>
To plot the converged MLWFs, please change the keyword
'Wannier.Function.Plot'
to be 'on'. The default value of it is 'off'.

```text

   Wannier.Function.Plot                  on         # default off
   Wannier.Function.Plot.SuperCells      1 1 1       # default=0 0 0
```

If it is turned on, all the MLWFs will be plotted.
They are written in the Gaussian cube file format with the file extension
such as '.mlwf1_4_r.cube'. The file is named in the same
style as HOMO or LUMO molecular orbitals files.
The first number after '.mlwf' indicates the spin index and
the following one are index of MLWFs and the last
letter 'r' or 'i' means the real or imaginary part of the MLWF.
Users can set the supercell size for plotting MLWF.
It is defined by the keyword
'Wannier.Function.Plot.SuperCells'.
'1 1 1' in the above example means that the unit cell is extended
by one in both the plus and minus directions along the a-, b-, and c-axes
by putting the home unit cell at the center, and therefore the MLWFs
are plotted in an extended cell consisting of

$27 (=(1*2+1)*(1*2+1)*(1*2+1))$ cells in this case.
Figure [47](maximally-localized-wannier-function-analysis.md#fig:Wannier_Si)(b) shows one of the eight converged MLWFs from four valence
states and four conduction states near Fermi level of Si in diamond
structure.
