<a id="SECTION000252000000000000000"></a>
## Cluster calculation

<a id="1604"></a>
In the cluster calculation, a double parallelization is made for two loops:
spin multiplicity and eigenstates, where the spin multiplicity is
one for the spin-unpolarized and non-collinear calculation, and two for
the spin-polarized calculation, respectively.
The priority of parallelization is in order of spin multiplicity and eigenstates.
OpenMX Ver. 3.9 employs ELPA [[39](bibliography.md#ELPA)] to solve the eigenvalue problem in the cluster
calculation, which is a highly parallelized eigevalue solver.
Either ELPA1 or ELPA2 can be chosen by the following keyword:

```text

     scf.eigen.lib      elpa1    # elpa1|elpa2, default=elpa1
```

The default choice is ELPA1. Our benchmark calculations suggest that ELPA1 and ELPA2 are comparable
to each other with respect to the computational speed, while we do not show the benchmark calculations here.
Figure [25](o-n-calculation.md#fig:DIA-MPI) (b) shows the speed-up ratio as a function of processors in the elapsed
time for a spin-polarized calculation of a single molecular
magnet consisting of 148 atoms. The input file 'Mn12.dat' is found in the directory 'work'.
It is found that the speed-up ratio is 11 and 17 using 32 and 64 processes, respectively.

---
