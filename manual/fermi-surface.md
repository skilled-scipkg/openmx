<a id="SECTION000630000000000000000"></a>
# Fermi surface

<a id="5610"></a>
<a id="5611"></a>
<a id="5612"></a>
<a id="5613"></a>
The Fermi surface is visualized by XCrySDen [[105](bibliography.md#XCrySDen)] and FermiSurfer [[143](bibliography.md#fermisurfer1),[144](bibliography.md#fermisurfer2)].
When you perform calculations of the density of states by the following keywords:

```text

  Dos.fileout                  on        # on|off, default=off
  Dos.Erange              -20.0  20.0    # default = -20 20 
  Dos.Kgrid                 61 61 61     # default = Kgrid1 Kgrid2 Kgrid3
  FermiSurfer.fileout         on         # default = off, on/off
```

you will obtain a file '*System.Name*.FermiSurf0.bxsf'
which is readable by XCrySDen [[105](bibliography.md#XCrySDen)] and a file '*System.Name*.FermiSurf_s0_a*A*.frmsf'
which is readable by FermiSurfer [[143](bibliography.md#fermisurfer1),[144](bibliography.md#fermisurfer2)],
where '*System.Name*' is 'System.Name', and *A* is the serial number of atoms.
To obtain the files readable by FermiSurfer, you need to switch on the keyword 'FermiSurfer.fileout'.
As well as 'Dos.Fileout', 'DosGauss.fileout' can also be used for the purpose, while the files readable by
FermiSurfer are not generated in the case of 'DosGauss.fileout'.
In case of spin-polarized calculations, for XCrySDen two files
'*System.Name*.FermiSurf0.bxsf' and '*System.Name*.FermiSurf1.bxsf'
are generated for spin-up and spin-down states, respectively, and for FermiSurfer two files
'*System.Name*.FermiSurf_s0_a*A*.frmsf' and '*System.Name*.FermiSurf_s1_a*A*.frmsf'
are generated for spin-up and spin-down states, respectively.
The data file for FermiSurfer can be used to display the color plot of the contribution
from each atoms.

<a id="fig:FermiSurface"></a>
<a id="6494"></a>
| ![\includegraphics[width=16.0cm]{FermiSurface.eps}](assets/img609.png) |
| --- |

For example, if we plot the character of atomic orbitals of the atom 1, we read
'*System.Name*.FermiSurf_s0_a1.frmsf'.
In case of non-collinear calculations, a file '*System.Name*.FermiSurf.bxs' and
'*System.Name*.FermiSurf_a*A*.frmsf' are generated.
It is noted that a large number of **k**-points should be used in order to obtain
a smooth Fermi surface.
As an example, Fermi surfaces of the fcc Ca bulk are shown in Fig. [89](fermi-surface.md#fig:FermiSurface).
The input file used for the calculation is available as 'Cafcc_FS.dat' in the directory 'work'.
