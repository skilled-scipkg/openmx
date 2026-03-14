<a id="SECTION000490000000000000000"></a>
# Calculations of work functions

Using cube files of either *System.Name*.v0.cube or *System.Name*.v1.cube,
one can calculate work functions of metals. The work function is defined by

<a id="eq:WorkFunc1"></a>
| $\displaystyle \Phi$ | $\textstyle =$ | $\displaystyle \left(\phi_{\infty} + E[N-1]\right) - E[N],$ |  |
| --- | --- | --- | --- |
|  | $\textstyle =$ | $\displaystyle \phi_{\infty} - \mu,$ | (11) |

where $E[N]$ and $E[N-1]$ are the total energies of the $N$-electron and $(N-1)$-electron systems,
respectively, and $\phi_{\infty}$ and $\mu$ are the potential at the infinite distance from the surface
and the chemical potential, respectively. The second line of Eq. ([11](calculations-of-work-functions.md#eq:WorkFunc1)) can be obtained
by the Janak theorem [[89](bibliography.md#Janak1978)] as
$E[N-1]-E[N]=\int dn \partial E/\partial n = -\mu$,
where $n$ is an occupation number of an one-particle eigenstate on the Fermi surface, $dn= -ds/S$
defined with the area of the Fermi surface $S$ and an infinitesimal area $ds$, and the surface
integral is performed over the Fermi surface.
Since the work function is a quantity associated to a surface, we need to introduce a slab model
as shown in Fig. [54](calculations-of-work-functions.md#fig:WorkFunc-Fig1)(a). As an example, we consider an aluminum slab, where
the layer thickness is 5 and the vacuum of about 60 Å is taken into account along the $x$-axis
together with the effective screening medium (ESM) method in Sec. [47](effective-screening-medium-method.md#sec:ESM), where
'ESM.switch=on1' is used, to avoid the interaction between the periodic slabs.
The SCF calculation can be performed using an input file 'Al111_WorkFunc_0E.dat' as follows:

```text

   % mpirun -np 28 ./openmx Al111_WorkFunc_0E.dat
```

After the calculation is completed normally, you obtain a cube file of 'Al111_WorkFunc_0E.v0.cube'.
To analyze the cube file, you can utilize a post-processing code of 'gcube2oned.c' in the directory 'source',
which can be compiled as

```text

   % gcc gcube2oned.c -lm -o gcube2oned
```

After copying the executable code 'gcube2oned' to your working directory, you can transform
the data of 3D cube data to an 1D data along a chosen direction,
in this case '1' corresponding to the **a**-axis, by integrating over the remaining 2D (**bc**-plane)
as follows:

```text

   % gcube2oned Al111_WorkFunc_0E.v0.cube 1 > 1d_pot.txt
```

<a id="fig:WorkFunc-Fig1"></a>
<a id="3412"></a>
| ![\includegraphics[width=12.0cm]{WorkFunc-Fig1.eps}](assets/img394.png) |
| --- |

In the obtained file '1d_pot.txt', the first, second, and third columns correspond to
the serian number of grid, the position (Å) along the **a**-axis, and a 1D potential (Hartree)
averaged over the **bc**-plane. In case of the 1D potential along the **b** or **c**-axis,
you can specify '2' or '3' as an argument of 'gcube2oned'. In Fig. [55](calculations-of-work-functions.md#fig:WorkFunc-Fig2) we show
the 1D potentials for the Al(111) surface along the **a**-axis which is perpendicular to the surface.
The number of layers consisting of empty atoms is systematically changed from 0 to 7 for both the surfaces.
As shown in Fig. [54](calculations-of-work-functions.md#fig:WorkFunc-Fig1), the layers consisting of empty atoms are taken into account
so that the tail of wave function towards the vacuum region can be accurately described.
The input files used for the calculations are
'Al111_WorkFunc_%E.dat', where % varies from 0 to 7, which are all available
in the directory 'work'.
The potential $\phi_{\infty}$ in Eq. ([11](calculations-of-work-functions.md#eq:WorkFunc1)) can be obtained from that at around 70 Å,
while the chemical potential $\mu$ can be found from the out file. Since the potential at around
70 Å is almost zero, the work function is basically determined by the chemical potential in the cases.
Then, the calculated values using Eq. ([11](calculations-of-work-functions.md#eq:WorkFunc1)) are plotted as a function of the number of
empty layers in Fig. [56](calculations-of-work-functions.md#fig:WorkFunc-Fig3).
One can see that the work function of the Al(111) surface reaches to the convergence
at the 2 empty layers, implying adding the 2 empty layers is sufficient to obtain the convergent result.

<a id="fig:WorkFunc-Fig2"></a>
<a id="6361"></a>
| ![\includegraphics[width=15.9cm]{WorkFunc-Fig2.eps}](assets/img395.png) |
| --- |

<a id="fig:WorkFunc-Fig3"></a>
<a id="6362"></a>
| ![\includegraphics[width=13.0cm]{WorkFunc-Fig3.eps}](assets/img396.png) |
| --- |

In Table [11](calculations-of-work-functions.md#table:WorkFunction) we show the calculated results of work function for five metals and
the corresponding experimental values. In all the calculations the 7 empty layers were introduced.
It is found that the calculated values are well compared to the experimental values.
The input files used for the calculations are 'Al111_WorkFunc_7E.dat', 'Cu111_WorkFunc_7E.dat',
'Ag111_WorkFunc_7E.dat', 'Au111_WorkFunc_7E.dat', and 'Pd111_WorkFunc_7E.dat', which are all
available in the directory 'work'.

As for gapped systems Eq. ([11](calculations-of-work-functions.md#eq:WorkFunc1)) may not be valid in a rigorous sense.
However, you may be able to use Eq. ([11](calculations-of-work-functions.md#eq:WorkFunc1)) as an approximate treatment.
Especially for gapped systems with polar surfaces, you need to use the ESM method
in Sec. [47](effective-screening-medium-method.md#sec:ESM) to avoid the interaction between the periodic slabs.

<a id="table:WorkFunction"></a>

<a id="3450"></a>
|  | OpenMX | Expt. |
| --- | --- | --- |
| Al(111) | 4.19 | 4.26$\pm$0.03 [[129](bibliography.md#Al111-WF)] |
| Cu(111) | 4.74 | 4.94$\pm$0.03 [[130](bibliography.md#Cu111-WF)] |
| Ag(111) | 4.51 | 4.46$\pm$0.02 [[131](bibliography.md#Ag111-WF)] |
| Au(111) | 5.33 | 5.26$\pm$0.04 [[132](bibliography.md#Au111-WF)] |
| Pd(111) | 5.40 | 5.55$\pm$0.01 [[133](bibliography.md#Pd111-WF)] |
