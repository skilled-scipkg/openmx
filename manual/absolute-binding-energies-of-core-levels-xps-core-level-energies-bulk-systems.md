<a id="SECTION000583000000000000000"></a>
## Bulk systems

Let us illustrate the calculation for the absolute binding energies of core levels in bulk by introducing
TiC bulk as an example.
The initial state calculation can be performed by

```text

    % mpirun -np 112 ./openmx TiC216.dat | tee TiC216.std
```

where any special keyword is not specified, but the spin-polarized calculation is performed with
'scf.SpinPolarization=on'. The input file 'TiC216.dat' is available in the directory 'work'.
The final state calculation can be performed by

```text

    % mpirun -np 112 ./openmx TiC216-CH3.dat | tee TiC216-CH3.std
```

The input file 'TiC216-CH3.dat' is available in the directory 'work'.
In the input file the atomic species are defined by

```text

   <Definition.of.Atomic.Species
     Ti  Ti7.0-s3p2d2        Ti_PBE13
     C   C6.0_1s-s3p2d1      C_PBE17_1s
     C1  C6.0_1s_CH-s3p2d1   C_PBE17_1s
   Definition.of.Atomic.Species>
```

and the species of 'C1' is allocated for atom 5 as

```text

   Atoms.Number         216
   Atoms.SpeciesAndCoordinates.Unit   Ang # Ang|AU
   <Atoms.SpeciesAndCoordinates           
      1  Ti   0.000000000000  0.000000000000  0.000000000000   6.0 6.0
      2  Ti   2.163500000000  2.163500000000  0.000000000000   6.0 6.0
      3  Ti   0.000000000000  2.163500000000  2.163500000000   6.0 6.0
      4  Ti   2.163500000000  0.000000000000  2.163500000000   6.0 6.0
      5  C1   2.163500000000  0.000000000000  0.000000000000   3.0 3.0
      6  C    0.000000000000  2.163500000000  0.000000000000   3.0 3.0
      7  C    0.000000000000  0.000000000000  2.163500000000   3.0 3.0
      8  C    2.163500000000  2.163500000000  2.163500000000   3.0 3.0
      ....
      ..
   Atoms.SpeciesAndCoordinates>
```

Then, a core hole is created for the $1s$-state on atom 5 by

```text

    scf.restart                 on
    scf.restart.filename        TiC216
    scf.coulomb.cutoff          on
    scf.core.hole               on
    scf.system.charge          0.0       # default=0.0

    <core.hole.state  
      5 s 1
    core.hole.state>
```

The Hartree potential $V_{H}$ in the final state calculation consists of two contributions [[88](bibliography.md#Ozaki_XPS2017)]:
periodic part
$V_{H}^{\rm (P)}$ and non-periodic part
$V_{H}^{\rm (NP)}$ as

| $\displaystyle V_{H}({\bf r}) = V_{H}^{\rm (P)}({\bf r}) + V_{H}^{\rm (NP)}({\bf r}),$ |  |  | (15) |
| --- | --- | --- | --- |

and the periodic part
$V_{H}^{\rm (P)}$ is calculated by the charge density obtained in the initial
state calculation via the Poisson equation with the periodic boundary condition.
One can specify the charge density obtained in the initial state calculation by
keywords 'scf.restart' and 'scf.restart.filename'.
The non-periodic part
$V_{H}^{\rm (NP)}$ is calculated by an exact Coulomb cutoff method [[91](bibliography.md#Jarvis1997)]
with the difference charge density
$\Delta \rho({\bf r}) = \rho_{\rm f}({\bf r}) - \rho_{\rm i}({\bf r})$,
where
$\rho_{\rm f}({\bf r})$ and
$\rho_{\rm i}({\bf r})$ are charge densities of final and initial states,
respectively, and the cutoff radius for the Coulomb interaction is set to the half of the lenght
of the shortest lattice vector.
You need to switch on the keyword 'scf.coulomb.cutoff' to enable the exact Coulomb cutoff method.
The core hole is created by the keywords 'scf.core.hole' and 'core.hole.state'.
In this case, a core hole for the 1s state on atom 5 is created.
It should be noted that the keyword 'scf.system.charge' is set to 0.0, since the TiC bulk is a metal.
When you treat a gapped system, 'scf.system.charge' has to be set to 1.0.

After finishing the calculations for the initial and final states, you may obtain the total energies
from the out files as

```text

     Initial state: -10499.900104007471 (Hartree)
     Final state:   -10489.553360141708 (Hartree)
```

Then, using Eq. ([14](absolute-binding-energies-of-core-levels-xps-core-level-energies-general.md#eq:XPS-Eq3)) the binding energy is found to be

| $\displaystyle E^{\rm (metal)}_{\rm b}$ | $\textstyle =$ | $\displaystyle E^{(0)}_{\rm f}(N-1) - E^{(0)}_{\rm i}(N),$ |  |
| --- | --- | --- | --- |
|  | $\textstyle =$ | $\displaystyle -10489.553360141708 - (-10499.900104007471) = 10.346743865763 ({\rm Hartree}),$ |  |
|  | $\textstyle \approx$ | $\displaystyle 281.55 ({\rm eV}).$ |  |

The obtained value of 281.55 eV is well compared to an experimental
value of 281.5 eV [[92](bibliography.md#Wagner1979)].

<a id="fig:XPS-Fig2"></a>
<a id="5109"></a>
| ![\includegraphics[width=16.0cm]{XPS-Fig2.eps}](assets/XPS-Fig2.png) |
| --- |

As an example of gapped systems, let us introduce calculations for bulk silicon.
One can perform the initial and final state calculations as

```text

    % mpirun -np 256 ./openmx Si-4-SOI.dat | tee Si-4-SOI.std
    % mpirun -np 256 ./openmx Si-4-CH-SOI1.dat | tee Si-4-CH-SOI1.std
    % mpirun -np 256 ./openmx Si-4-CH-SOI6.dat | tee Si-4-CH-SOI6.std
```

The input file of 'Si-4-SOI.dat' is for the initial state calculation, while
'Si-4-CH-SOI1.dat' and 'Si-4-CH-SOI6.dat' are for the final state calculations
with a core hole for the $2p$ state on Si atom specified by
$2p_{3/2} (J=3/2, M=3/2)$
and
$2p_{1/2} (J=1/2, M=-1/2)$, respectively.
To take account of the spin-orbit interaction in the $2p$ state on the Si atom
the non-collinear calculations are performed by specifying the following keywords:

```text

    scf.SpinPolarization        nc         # On|Off|NC
    scf.SpinOrbit.Coupling      on         # On|Off, default=off
```

After finishing the calculations for the initial and final states, you may obtain the total energies
from the out files as

```text

     Initial state:          -34820.483255130872 (Hartree)
     Final state for SOI1:   -34816.628201335407 (Hartree)
     Final state for SOI6:   -34816.601864921540 (Hartree)
```

and the chemical potential can be obtained from the initial state calculation.
Then, using Eq. ([13](absolute-binding-energies-of-core-levels-xps-core-level-energies-general.md#eq:XPS-Eq2)) the binding energies for SOI1 and SOI6 are found to be

| $\displaystyle {\rm For}~2p_{3/2}$ |  |  |  |
| --- | --- | --- | --- |
| $\displaystyle E^{\rm (bulk)}_{\rm b}$ | $\textstyle =$ | $\displaystyle E^{(0)}_{\rm f}(N-1) - E^{(0)}_{\rm i}(N-1) + \mu_0,$ |  |
|  | $\textstyle =$ | $\displaystyle -34816.628201335- (-34820.483255131) -0.201641583 = 3.65341221 ({\rm Hartree}),$ |  |
|  | $\textstyle \approx$ | $\displaystyle 99.41 ({\rm eV}),$ |  |
| $\displaystyle {\rm For}~2p_{1/2}$ |  |  |  |
| $\displaystyle E^{\rm (bulk)}_{\rm b}$ | $\textstyle =$ | $\displaystyle E^{(0)}_{\rm f}(N-1) - E^{(0)}_{\rm i}(N-1) + \mu_0,$ |  |
|  | $\textstyle =$ | $\displaystyle -34816.601864922 - (-34820.483255131) -0.201641583 = 3.6797486 ({\rm Hartree}),$ |  |
|  | $\textstyle \approx$ | $\displaystyle 100.13 ({\rm eV}).$ |  |

The obtained values of 99.41 and 100.13 eV are well compared to an experimental
value of 99.2 and 99.8 eV for $2p_{3/2}$ and $2p_{1/2}$, respectively [[92](bibliography.md#Wagner1979)], where
the degeneracies of $2p_{3/2}$ and $2p_{1/2}$ are 4 and 2, repectively, as can be seen from Table [12](absolute-binding-energies-of-core-levels-xps-core-level-energies-gaseous-systems.md#table:XPS-Col-orbitals).
It should be noted that for gapped systems the convergence of the absolute binding energies of core levels
is slow with repect to the cell size. In Figs. [79](absolute-binding-energies-of-core-levels-xps-core-level-energies-bulk-systems.md#fig:XPS-Fig2)(a) and (b), the relative binding energies
are shown as a function of inter-core hole distance for gapped systems and metals, respectively.
It is found that the convergence is slow for the gapped systems, implying that a large supercell needs to
be used to obtain the convergence result. On the other hand, we see that for metals the binding energies
quickly converges at a relatively small inter-core hole distance.
In Fig. [79](absolute-binding-energies-of-core-levels-xps-core-level-energies-bulk-systems.md#fig:XPS-Fig2)(c) we show difference charge density in silicon bulk, induced by
the creation of a core hole in the $2p$ state. To screen the potential produced by the core hole,
a charge redistribution takes place up to around $\sim 7$ Å from the core hole.
The slow convergence found in gapped systems is attributed to the charge redistribution.
On the other hand, in metals the charge redistribution is relatively short range, resulting in the fast convergence
as shown in Fig. [79](absolute-binding-energies-of-core-levels-xps-core-level-energies-bulk-systems.md#fig:XPS-Fig2)(b).

The other examples of calculations and input files used for the calculations
can be found in the website: https://t-ozaki.issp.u-tokyo.ac.jp/vps_pao_core2019/.
Also, applications of the method for silicene, borophene, and single Pt atoms dispersed on graphene
can be found in Refs. [[93](bibliography.md#Lee2017),[94](bibliography.md#Lee2018),[95](bibliography.md#Yamazaki2018)].
