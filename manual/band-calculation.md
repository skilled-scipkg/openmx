<a id="SECTION000253000000000000000"></a>
## Band calculation

<a id="1621"></a>
In the band calculation, a triple parallelization is made for three loops:
spin multiplicity, **k**-points, and eigenstates, where the spin multiplicity is
one for the spin-unpolarized and non-collinear calculations, and two for the spin-polarized
calculation, respectively. The priority of parallelization is in order of spin multiplicity,
**k**-points, and eigenstates.
In addition, when the number of processes used in the parallelization
exceeds (spin multiplicity)$\times $(the number of k-points), OpenMX uses
an efficient way in which finding the Fermi level and calculating
the density matrix are performed by just one diagonalization at each **k**-point.
For the other cases, twice diagonalizations are performed at each **k**-point
for saving the size of used memory in which the second diagonalization is
performed to calculate the density matrix after finding the Fermi level.
In Fig. [25](o-n-calculation.md#fig:DIA-MPI) (c) we see a good speed-up ratio as a function of processes
in the elapsed time for a spin-unpolarized calculation of carbon diamond consisting
of 64 carbon atoms with 3$\times $3$\times $3 k-points.
The input file 'DIA64_Band.dat' is found in the directory 'work'.
In this case the spin multiplicity is one, and the number of k-points used for
the actual calculation is (3*3*3-1)/2+1=14, since the **k**-points in the half
Brillouin zone is taken into account for the collinear calculation, and
the $\Gamma $-point is included when all the numbers of **k**-points for **a**-, **b**-,
and **c**-axes are odd. So it is found that the speed-up ratio exceeds the ideal one
in the range of processes over 14, which means the algorithm in the
parallelization is changed to the efficient scheme.
As well as the cluster calculation, OpenMX Ver. 3.9 employs ELPA [[39](bibliography.md#ELPA)] to
solve the eigenvalue problem in the band calculation, which is a highly parallelized
eigevalue solver.
Either ELPA1 or ELPA2 can be chosen by the following keyword:

```text

     scf.eigen.lib      elpa1    # elpa1|elpa2, default=elpa1
```

The default choice is ELPA1. Our benchmark calculations suggest that ELPA1 and ELPA2 are comparable
to each other with respect to the computational speed, while we do not show the benchmark calculations here.
