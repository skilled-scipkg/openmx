<a id="SECTION000300000000000000000"></a>
# Virtual atom with fractional nuclear charge

It is possible to treat a virtual atom with fractional nuclear
charge by using a pseudopotential with the corresponding fractional
nuclear charge. The pseudopotential for the virtual atom can be generated
by ADPACK. The relevant keywords in ADPACK are given by

```text

     AtomSpecies            6.2
     total.electron         6.2
     valence.electron       4.2 
     <occupied.electrons 
      1   2.0
      2   2.0  2.2
     occupied.electrons>
```

The above example is for a virtual atom on the way of carbon and
nitrogen atoms.
Also, it is noted that basis functions for the pseudopotential
of the virtual atom must be generated for the virtual atom with
the same fractional nuclear charge, since the atomic charge density
stored in *.pao is used to make the neutral atom potential.

As an illustration, the DOS of C$_{7.8}$N$_{0.2}$ calculated
using the method is shown in Fig. [30](virtual-atom-with-fractional-nuclear-charge.md#fig:dia8-va). The input file is
'DIA8-VA.dat' which can be found in the directory 'work'.
In the calculation, one of eight carbon atoms in the unit cell was
replaced by a virtual atom with an effective nuclear charge of 4.2,
which corresponds to a stoichiometric compound of C$_{7.8}$N$_{0.2}$.

<a id="fig:dia8-va"></a>
<a id="6284"></a>
| ![\includegraphics[width=13.0cm]{dia8-va.eps}](assets/img189.png) |
| --- |
