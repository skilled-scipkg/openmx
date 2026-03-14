<a id="SECTION000131000000000000000"></a>
## Convergence

The computational effort and accuracy depend on the
cutoff energy, which is controlled by the keyword 'scf.energycutoff',
for the numerical integrations and the solution of Poisson's
equation [[42](bibliography.md#Ozaki2)].
Figure [5](convergence.md#fig:cutoff) shows the convergence of the total energy of a methane molecule
with respect to the cutoff energy, where the input file is 'Methane.dat'
used in the Section 'Input file'.
Since the cutoff energy is not for basis set as in plane wave methods, but for the numerical
integrations, the total energy does not have to converge from the upper
energy region with respect to the cutoff energy like that of plane wave basis set.
In most cases, the cutoff energy of 150-200 Ryd is an optimum choice.
However, it should be noted that there is a subtle problem which requires
the cutoff energy more than 300 Ryd. Calculations of a very flat potential
minimum and a small energy difference among different spin orders could be
such a subtle problem.

<a id="733"></a>
Structural parameters and the dipole moment of a water molecule,
calculated with a different cutoff energy, are shown in Table [3](convergence.md#table:cutoff_H2O),
where the input file is 'H2O.dat' in the directory 'work'.
A convergent result is obtained using around 90 Ryd.
Although a sufficient cutoff energy depends on elements, 150-200 Ryd
might be enough to achieve the convergence for most cases.
However, we recommend that you would check physical properties for your system.
For the other cutoff energy, 1DFFT.EnergyCutoff,
we commonly use 3600 (Ryd) which is quite enough for the convergence with no
high computational demands.

<a id="fig:cutoff"></a>
<a id="738"></a>
| ![\includegraphics[width=13.0cm]{cutoff.eps}](assets/img113.png) |
| --- |

<a id="table:cutoff_H2O"></a>
<a id="table:cutoff_H2O"></a>
| Ecut(Ryd)
r(H-O) (Å)
$\angle$ (H-O-H) (deg)
Dipole moment (Debye)

60
0.970
103.4
1.838

90
0.971
103.7
1.829

120
0.971
103.7
1.832

150
0.971
103.6
1.829

180
0.971
103.6
1.833

Exp.
0.957
104.5
1.85 |  |  |  |
| --- | --- | --- | --- |
| Ecut(Ryd) | r(H-O) (Å) | $\angle$ (H-O-H) (deg) | Dipole moment (Debye) |
| 60 | 0.970 | 103.4 | 1.838 |
| 90 | 0.971 | 103.7 | 1.829 |
| 120 | 0.971 | 103.7 | 1.832 |
| 150 | 0.971 | 103.6 | 1.829 |
| 180 | 0.971 | 103.6 | 1.833 |
| Exp. | 0.957 | 104.5 | 1.85 |
