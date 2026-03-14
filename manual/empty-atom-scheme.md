<a id="SECTION000115000000000000000"></a>
## Empty atom scheme

The primitive and optimized PAO functions are usually assigned to atoms.
Moreover, it is possible to assign basis functions
in any vacant region using an *empty* atom. You will find the empty atom 'E'
in the website of the database (http://www.openmx-square.org/).
Using the pseudopotential for the empty atom 'E', though the pseudopotential is
a flat zero potential, you can put basis functions at any place independently
of atomic position. To do that, you can define empty atoms by

```text

   <Definition.of.Atomic.Species
     H    H5.0-s2p1      H_PBE19
     C    C5.0-s2p1      C_PBE19
     EH   H5.0-s2p1      E
     EC   C5.0-s2p1      E
   Definition.of.Atomic.Species>
```

In the example, two sorts of empty atoms are defined as 'EH' and 'EC' which have
basis sets specified by 'H5.0-s2p1' and 'C5.0-s2p1', respectively, which means that
one can use any basis functions for an empty atom as shown above. Then 'EH' and 'EC'
can be put to any place by the keyword 'Atoms.SpeciesAndCoordinates', where the number
of electrons for the empty atom is zero. To define an empty atom, only thing you have
to do is to use 'E.vps' as pseudopotential for the empty atom.
The empty atom scheme enables us not only to estimate the basis set superposition error (BSSE)
using the counterpoise correction (CP) method [[46](bibliography.md#Boys70),[47](bibliography.md#Simon96)], but also to treat
a vacancy state and a nearly free electron state on metal surfaces within
the linear combination of pseudo-atomic orbitals (LCPAO) method.
As an example, a calculation of a F-center in NaCl with a Cl vacancy is shown in Fig. [3](empty-atom-scheme.md#fig:NaCl_FC).
We see that the highest occupied state at the $\Gamma $ point is the F-center state.
You can follow the calculation using 'NaCl_FC.dat' in the directory 'work'.

<a id="fig:NaCl_FC"></a>
<a id="6240"></a>
<a id="653"></a>
<a id="653"></a>
| ![\includegraphics[width=10.0cm]{NaCl_FC.eps}](assets/img110.png) |
| --- |
