<a id="SECTION000460000000000000000"></a>
# Interface with Wannier90

<a id="3250"></a>
<a id="3251"></a>
OpenMX is interfaced with Wannier90 [[145](bibliography.md#wf90)] which constructs maximally localized Wannier functions,
and calculates physical properties such as Wannier projected DOS and bandstructure, Fermi surface,
Berry phase related properties (anomalous Hall conductivity and optical conductivity),
and thermoelectric properties.
For the calculations, you need to set two keywords as follows:

```text

  Wannier.Func.Calc        on    # on|off, default=off 
  Wannier90.fileout        on    # on|off, default=off
```

Once you run a job by an input file with the parameter settings shown above, you will see that
the job will finish with the following message:

```text

  The input files for Wannier90,

  System.Name.amn
  System.Name.mmn
  System.Name.eig
  System.Name.win

  are successfully generated.
```

After finishing the calculation, you will obtain the four files listed above.
The first three files will be read by 'wannier90.x' of Wannier90, and the last file 'System.Name.win' is
an input file to handle the calculation of 'wannier90.x'.
The schematic computational flow is shown in Fig. [48](interface-with-wannier90.md#fig:OpenMX_Wannier90).
With the overlap matrix 'System.Name.mmn', the projection matrix 'System.Name.amn',
and eigenvalues 'System.Name.eig', maximally localized Wannier functions are calculated
by using 'wannier90.x'.
After getting the maximally localized Wannier functions, by using 'postw90.x' of Wannier90
you can calculate a variety of physical properties
such as Berry phase related properties (anomalous Hall conductivity and optical conductivity)
and thermoelectric properties.
In the file 'System.Name.win' the default setting is for the calculation of optical conductivity as

```text

  berry_task   kubo
```

By changing the option for the keyword 'berry_task' properly, you may be able to calculate other physical quantities.
Some of the options for the keyword are listed below:

```text

  berry_task   kubo     #  optical conductivity 
  berry_task   ahc      #  anomalous Hall conductivity
```

As for the more details of Wannier90, please refer to the website of Wannier90 [[145](bibliography.md#wf90)].

As examples, Figures [49](interface-with-wannier90.md#fig:OpenMX_Wannier90-Seebeck) and [50](interface-with-wannier90.md#fig:OpenMX_Wannier90-SrVO3) show
Seebeck coefficient of silicon in the diamond structure and optical conductivity of SrVO$_3$, respectively,
calculated by interfacing OpenMX with Wannier90 with the above mentioned scheme.
The input files 'Si-Wannier90.dat' and 'SrVO3-Wannier90.dat' can be found in the directory 'work'.

<a id="fig:OpenMX_Wannier90"></a>
<a id="3273"></a>
| ![\includegraphics[width=16.5cm]{OpenMX_Wannier90.epsi}](assets/img367.png) |
| --- |

<a id="fig:OpenMX_Wannier90-Seebeck"></a>
<a id="3280"></a>
| ![\includegraphics[width=17.0cm]{OpenMX_Wannier90-Seebeck.epsi}](assets/img368.png) |
| --- |

<a id="fig:OpenMX_Wannier90-SrVO3"></a>
<a id="6359"></a>
| ![\includegraphics[width=17.0cm]{OpenMX_Wannier90-SrVO3.epsi}](assets/img369.png) |
| --- |
