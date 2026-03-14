<a id="SECTION000582000000000000000"></a>
## Gaseous systems

Let us introduce a couple of examples to illustrate how the absolute binding energies of core levels
can be calculated below:

We try to calculate the binding energy for the 1s state of carbon atom in a C$_2$H$_2$ molecule.
The **initial state** calculation can be performed as

```text

   % mpirun -np 4 ./openmx C2H2.dat
```

where the input file 'C2H2.dat' is avalilable in the directory 'work'.
In the initial state calculation you need to specify the following keyword:

```text

    scf.coulomb.cutoff          on       # default = off
    scf.SpinPolarization        on or nc # default = off
```

In case of 'scf.coulomb.cutoff=on', the clasical Coulomb interaction between supercells is cut off
along all the three directions **a**-, **b**-, and **c**-axes using the exact Coulomb cutoff method [[91](bibliography.md#Jarvis1997)].
In the calculations for the initial and final state calculations, you need to specify either 'on' or 'nc'
for the keyword 'scf.SpinPolarization' and keep the same option in both the initial and final state calculations,
since the system is spin-polarized after the creation of a core hole in the final state calculation.
To calculate the absolute binding energies of core levels, we need to have pseudopotentials
including the relevant core state. In the input file 'C2H2.dat', the following pseudopotentials
are specified:

```text

    <Definition.of.Atomic.Species
      H   H7.0-s3p2           H_PBE19
      C   C7.0_1s-s4p3d2      C_PBE19_1s
      C1  C7.0_1s_CH-s4p3d2   C_PBE19_1s
    Definition.of.Atomic.Species>
```

The pseudopotential of 'C_PBE19_1s.vps' actually includes the 1s, 2s, and 2p states as
valence states. The basis sets of 'C7.0_1s.pao' and 'C7.0_1s_CH' are used for the initial
and final state calculations, respectively. In the final state calculation,
the radial wave functions are largely modified due to the core hole compared to the
the state without the core hole. Thus, the basis set optimized for the state with the core hole
has to be utilized to obtain a convergent result. The pseudopotential and basis sets for the
final state calculations are available at the following website:

```text

    https://t-ozaki.issp.u-tokyo.ac.jp/vps_pao_core2019/
```

The data for only seven elements: B, C, N, O, Si, S, Ge, Pt are now available on the website.
We have been planing to develop the pseudopotentials and basis sets of the other elements
for core level excitations in the near future.
The geometrical structure is specified as follows:

```text

   Atoms.Number         4
   Atoms.SpeciesAndCoordinates.Unit   Ang # Ang|AU
   <Atoms.SpeciesAndCoordinates           # Unit=Ang.
     1  C   0.6005  0.000  0.000  3.0 3.0
     2  C  -0.6005  0.000  0.000  3.0 3.0
     3  H   1.8015  0.000  0.000  0.5 0.5
     4  H  -1.8015  0.000  0.000  0.5 0.5
   Atoms.SpeciesAndCoordinates>
```

It should be noted that the species for atom 1 is 'C' for which we allocate 'C7.0_1s.pao' being the basis set
for the initial state, while we are going to create a core hole of 1s state for atom 1.

<a id="table:XPS-Col-orbitals"></a>
<a id="4947"></a>
<a id="4947"></a>
| Collinear case |  |  |  |  |  |  |  |  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| $s$ | 1: $s\uparrow$ | 2: $s\downarrow$ |  |  |  |  |  |  |
| $p$ | 1: $p_x\uparrow$ | 2: $p_y\uparrow$ | 3: $p_z\uparrow$ | 4: $p_x\downarrow$ | 5: $p_y\downarrow$ | 6: $p_z\downarrow$ |  |  |
| $d$ | 1:
$d_{3z^2-r^2}\uparrow$ | 2:
$d_{x^2-y^2}\uparrow$ | 3:
$d_{xy}\uparrow$ | 4:
$d_{xz}\uparrow$ | 5:
$d_{yz}\uparrow$ |  |  |  |
|  | 6:
$d_{3z^2-r^2}\downarrow$ | 7:
$d_{x^2-y^2}\downarrow$ | 8:
$d_{xy}\downarrow$ | 9:
$d_{xz}\downarrow$ | 10:
$d_{yz}\downarrow$ |  |  |  |
| $f$ | 1:
$f_{5z^2-3r^2}\uparrow$ | 2:
$f_{5xz^2-xr^2}\uparrow$ | 3:
$f_{5yz^2-yr^2}\uparrow$ | 4:
$f_{zx^2-zy^2}\uparrow$ | 5:
$f_{xyz}\uparrow$ | 6:
$f_{x^3-3xy^2}\uparrow$ | 7:
$f_{3yx^2-y^3}\uparrow$ |  |
|  | 8:
$f_{5z^2-3r^2}\downarrow$ | 9:
$f_{5xz^2-xr^2}\downarrow$ | 10:
$f_{5yz^2-yr^2}\downarrow$ | 11:
$f_{zx^2-zy^2}\downarrow$ | 12:
$f_{xyz}\downarrow$ | 13:
$f_{x^3-3xy^2}\downarrow$ | 14:
$f_{3yx^2-y^3}\downarrow$ |  |
| Non-collinear case |  |  |  |  |  |  |  |  |
| $s$ | 1:
$J=1/2$
$M=1/2$ | 2:
$J=1/2$
$M=$-1/2 |  |  |  |  |  |  |
| $p$ | 1:
$J=3/2$
$M=3/2$ | 2:
$J=3/2$
$M=1/2$ | 3:
$J=3/2$
$M=$-1/2 | 4:
$J=3/2$
$M=$-3/2 | 5:
$J=1/2$
$M=1/2$ | 6:
$J=1/2$
$M=$-1/2 |  |  |
| $d$ | 1:
$J=5/2$
$M=5/2$ | 2:
$J=5/2$
$M=3/2$ | 3:
$J=5/2$
$M=1/2$ | 4:
$J=5/2$
$M=$-1/2 | 5:
$J=5/2$
$M=$-3/2 | 6:
$J=5/2$
$M=$-5/2 |  |  |
|  | 7:
$J=3/2$
$M=3/2$ | 8:
$J=3/2$
$M=1/2$ | 9:
$J=3/2$
$M=$-1/2 | 10:
$J=3/2$
$M=$-3/2 |  |  |  |  |
| $f$ | 1:
$J=7/2$
$M=7/2$ | 2:
$J=7/2$
$M=5/2$ | 3:
$J=7/2$
$M=3/2$ | 4:
$J=7/2$
$M=1/2$ | 5:
$J=7/2$
$M=$-1/2 | 6:
$J=7/2$
$M=$-3/2 | 7:
$J=7/2$
$M=$-5/2 | 8:
$J=7/2$
$M=$-7/2 |
|  | 9:
$J=5/2$
$M=5/2$ | 10:
$J=5/2$
$M=3/2$ | 11:
$J=5/2$
$M=1/2$ | 12:
$J=5/2$
$M=$-1/2 | 13:
$J=5/2$
$M=$-3/2 | 14:
$J=5/2$
$M=$-5/2 |  |  |

The **final state** calculation can be performed as

```text

   % mpirun -np 4 ./openmx C2H2-CH.dat
```

where the input file 'C2H2-CH.dat' is avalilable in the directory 'work'.
The geometrical structure is specified as follows:

```text

   Atoms.Number         4
   Atoms.SpeciesAndCoordinates.Unit   Ang # Ang|AU
   <Atoms.SpeciesAndCoordinates           # Unit=Ang.
     1  C1  0.6005  0.000  0.000  3.0 3.0
     2  C  -0.6005  0.000  0.000  3.0 3.0
     3  H   1.8015  0.000  0.000  0.5 0.5
     4  H  -1.8015  0.000  0.000  0.5 0.5
   Atoms.SpeciesAndCoordinates>
```

The atomic positions are exactly the same as for the initial state calculation, which means that the atomic relaxation
during the excitation process is not taken into account.
It is important to note that the species for atom 1 is 'C1' for which we allocate 'C7.0_1s_CH.pao' being the basis set
for the final state. For the final state calculation, you need to specify the following keywords:

```text

    scf.system.charge            1.0    # default=0.0
    scf.coulomb.cutoff            on    # default = off
    scf.core.hole                 on    # default = off
    <core.hole.state
      1 s 1
    core.hole.state>
```

Considering that the final state has $(N-1)$ electrons, the number of electrons is reduced by 1 with the keyword 'scf.system.charge'.
Then, we again use the Coulomb cutoff method [[91](bibliography.md#Jarvis1997)] using the keyword 'scf.coulomb.cutoff'
to avoid the spurious interaction of core holes between supercells.
If the Coulomb cutoff method is not employed, a compensation uniform charge automatically introduced
to avoid the Coulomb divergence in periodic charged systems. Since the treatment leads to a spurious interaction,
the comparison between the initial and final states for the total energy cannot be simply performed.
The core hole state that we target can be specified by the keyword 'core.hole.state'.
The first number is the atomic serial index which is specified in the keyword 'Atoms.SpeciesAndCoordinates', the second symbol
specifies the target $l$-channel which can be '$s$', '$p$', '$d$', or '$f$'. The last number specifies the orbital
index which can be 1 to $4l+1$. The relation between the index and the state is given in Table [12](absolute-binding-energies-of-core-levels-xps-core-level-energies-gaseous-systems.md#table:XPS-Col-orbitals).
It it noted that the target state that we create a core hole is the lowest state with the $l$-channel included
in the pseudopotential as valence states. In the case of C$_2$H$_2$ molecule, the pseudopotential of 'C_PBE19_1s.vps' includes
the 1s state as valence state. Thus, the following specification:

```text

    <core.hole.state
      1 s 1
    core.hole.state>
```

means that the state of
$\vert 1s\uparrow\rangle$ on atom 1 is chosen as target state for 'scf.SpinPolarization=on'.
When a $s$-state is chosen as target state, 'scf.SpinPolarization=on' can be specified, while 'scf.SpinPolarization=nc'
can also be employed.
On the other hand,
'scf.SpinPolarization=nc' has to be specified to include spin-orbit coupling when a $p$-, $d$-, or $f$-state
is chosen as target state.

After finishing the calculations for the initial and final states, you may obtain the total energies
from the out files as

```text

     Initial state: -76.787732114928 (Hartree)
     Final state:   -66.084858926233 (Hartree)
```

Then, using Eq. ([12](absolute-binding-energies-of-core-levels-xps-core-level-energies-general.md#eq:XPS-Eq1)) the binding energy is found to be

| $\displaystyle E^{\rm (gas)}_{\rm b}$ | $\textstyle =$ | $\displaystyle E^{(0)}_{\rm f}(N-1) - E^{(0)}_{\rm i}(N),$ |  |
| --- | --- | --- | --- |
|  | $\textstyle =$ | $\displaystyle -66.084858926233 - (-76.787732114928) = 10.702873188695 ({\rm Hartree}),$ |  |
|  | $\textstyle \approx$ | $\displaystyle 291.24 ({\rm eV}).$ |  |

The obtained value of 291.24 eV is well compared to an experimental
value of 291.14 eV [[90](bibliography.md#Jolly1984)]. The other examples of calculations and input files used for the calculations
can be found in the website:
https://t-ozaki.issp.u-tokyo.ac.jp/vps_pao_core2019/.
