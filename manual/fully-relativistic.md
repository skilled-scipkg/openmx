<a id="SECTION000361000000000000000"></a>
## Fully relativistic

<a id="1880"></a>
The fully relativistic effects including the spin-orbit coupling
within the pseudopotential scheme can be included in the non-collinear
DFT calculations [[12](bibliography.md#MacDonald),[32](bibliography.md#BHS),[16](bibliography.md#Theurich)],
while the inclusion of the spin-orbit coupling is not supported in the collinear
DFT calculation. The inclusion of fully relativistic effects is made
by the following two steps:

**(1) Making of j-dependent pseudopotentials**

First, you are requested to generate j-dependent pseudopotentials
using ADPACK. For your convenience, the j-dependent pseudopotentials
are available for many elements in the database Ver. 2019 [[149](bibliography.md#DataBase)].
The details how to make the j-dependent pseudopotential are found in
the manual of ADPACK.

**(2) SCF calculation**

If you specify j-dependent pseudopotentials in the specification of
'$<$Definition.of.Atomic.Species',
it is possible to include spin-orbit
coupling by the following keyword 'scf.SpinOrbit.Coupling':

<a id="1881"></a>

```text

    scf.SpinOrbit.Coupling      on         # On|Off, default=off
```

Then, the spin-orbit coupling can be self-consistently incorporated
within the pseudopotential scheme rather than a perturbation scheme.
Due to the spin-orbit coupling, $\alpha $ and $\beta $ spin components
in the two component spinor can directly interact.
In order to determine the absolute spin orientation in the non-collinear
DFT calculations, you have to include the spin-orbit coupling, otherwise
the spin orientation is not uniquely determined in real space.
As an illustration of spin-orbit splitting, we show band structures of
a bulk GaAs calculated by the non-collinear DFT without and with spin-orbit
coupling in Fig. [33](fully-relativistic.md#fig:GaAs_SOC), where the input file is 'GaAs.dat' in the
directory 'work'.
In Fig. [33](fully-relativistic.md#fig:GaAs_SOC)(b) we can see that there are spin-orbit
splittings in the band dispersion, while no spin-orbit splitting is
observed in Fig. [33](fully-relativistic.md#fig:GaAs_SOC)(a). The spin-orbit splittings at two **k**-points,
$\Gamma $ and $L$, are listed together with the other calculations
and experimental values in Table [5](fully-relativistic.md#table:SOC-GaAs).
We see a good agreement in this table.

<a id="fig:GaAs_SOC"></a>
<a id="6288"></a>
<a id="1889"></a>
<a id="1890"></a>
<a id="1889"></a>
<a id="1890"></a>
| ![\includegraphics[width=15.0cm]{GaAs_SOC.eps}](assets/img194.png) |
| --- |

<a id="table:SOC-GaAs"></a>
<a id="table:SOC-GaAs"></a>
| Level
OpenMX
LMTO
PP
Expt.

$\Gamma _{15v}$
0.344
0.351
0.35
0.34

$L_{3v}$
0.213
0.213
0.22 |  |  |  |  |
| --- | --- | --- | --- | --- |
| Level | OpenMX | LMTO | PP | Expt. |
| $\Gamma _{15v}$ | 0.344 | 0.351 | 0.35 | 0.34 |
| $L_{3v}$ | 0.213 | 0.213 | 0.22 |  |
