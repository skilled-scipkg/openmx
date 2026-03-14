<a id="SECTION000241000000000000000"></a>
## Divide-conquer method

<a id="1398"></a>
The DC method is a robust scheme and can be applicable to a wide variety
of materials with a reasonable degree of accuracy and efficiency, while
this scheme is suitable especially for covalent systems.
In this subsection, the O($N$) calculation using the DC method is
illustrated. In an input file 'DIA8_DC.dat' which can be found in the
directory 'work', please specify 'DC' for
the keyword 'scf.EigenvalueSolver'.

```text

     scf.EigenvalueSolver   DC
```

Then, one can execute OpenMX by:

```text

    % ./openmx DIA8_DC.dat
```

The input file is for an O($N$) calculation (1 MD step) of the diamond
including 8 carbon atoms. The computational time is 120 seconds using
a Xeon machine (2.6 GHz). Figure [17](divide-conquer-method.md#fig:DIA-ON) shows the computational time
and memory size to calculate a MD step of the carbon diamond as
a function of number of atoms in the supercell.
In fact, we see that the computational time and memory size are almost
proportional to the number of atoms.
The accuracy and efficiency of the DC method are controlled by
a single parameter: 'orderN.HoppingRanges'.

<a id="1439"></a>
<a id="1440"></a>
- orderN.HoppingRanges
  <a id="1440"></a>
  The keyword 'orderN.HoppingRanges'
  defines the radius of a sphere which is centered on each atom.
  The physically truncated cluster for each atom is constructed by
  picking up atoms inside the sphere with the radius in the DC, DC-LNO, and O($N$)
  Krylov subspace methods.

<a id="1449"></a>
If the number of atoms in the systems is $N$, $N$ small eigenvalue problems
for the $N$ physically truncated clusters are solved, and then the total
density of states (DOS) is constructed as the sum of the projected DOS
of each physically truncated cluster.
Although the appropriate value for
'orderN.HoppingRanges'
depends on systems,
for molecular systems
the following values are recommended as a trade-off between
the computational accuracy and efficiency:

```text

     orderN.HoppingRanges     6.0 - 7.0
```

Table [4](divide-conquer-method.md#table:orderN-time) shows the comparison in the total energy between the exact
diagonalization and the DC method for a C$_{60}$ molecule and small
peptide molecules (valorphin [[107](bibliography.md#valorphin)]), and DNA consisting of
cytosines and guanines.
We find that errors in the total energy calculated by the DC method are
about a few mHartree in the system size.
Also, it can be estimated that the DC method is faster
than the conventional diagonalization when the number of atoms is
larger than 500 atoms, while the crossing point between the conventional
diagonalization and the DC method with respect to computational time
depends on systems and the number of processors in the parallel calculation.

To see an overall tendency in the convergence properties of total energy
with respect to the size of truncated cluster, the error in the total
energy, compared to the exact diagonalization, is shown as a function
of the number of atoms in each cluster for (a) bulks with a finite gap,
(b) metals, and (c) molecular systems in Fig. [18](divide-conquer-method.md#fig:DC_Error).
We see that the error decreases almost exponentially for the bulks with
a finite gap and molecular systems, while the convergence speed is slower
for metals.

<a id="fig:DIA-ON"></a>
<a id="6269"></a>
<a id="1412"></a>
<a id="1412"></a>
| ![\includegraphics[width=12.0cm]{DIA-ON.eps}](assets/img167.png) |
| --- |

<a id="1423"></a>
<a id="table:orderN-time"></a>
<a id="1423"></a>
<a id="table:orderN-time"></a>
| Total energy (Hartree)
Computational time (s)

**C$_{60}$**

(60 atoms, 240 orbitals)

Conventional
-343.89680
36

DC (7.0)
-343.89555
37

**Valorphin**

(125 atoms, 317 orbitals)

Conventional
-555.28953
81

DC (6.5)
-555.29019
76

**DNA**

(650 atoms, 1880 orbitals)

Conventional
-4090.95463
576

DC (6.3)
-4090.95092
415 |  |  |
| --- | --- | --- |
|  | Total energy (Hartree) | Computational time (s) |
| **C$_{60}$** |  |  |
| (60 atoms, 240 orbitals) |  |  |
| Conventional | -343.89680 | 36 |
| DC (7.0) | -343.89555 | 37 |
| **Valorphin** |  |  |
| (125 atoms, 317 orbitals) |  |  |
| Conventional | -555.28953 | 81 |
| DC (6.5) | -555.29019 | 76 |
| **DNA** |  |  |
| (650 atoms, 1880 orbitals) |  |  |
| Conventional | -4090.95463 | 576 |
| DC (6.3) | -4090.95092 | 415 |

<a id="fig:DC_Error"></a>
<a id="1446"></a>
| ![\includegraphics[width=10.0cm]{DC_Error.eps}](assets/img168.png) |
| --- |
