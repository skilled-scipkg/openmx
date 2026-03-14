<a id="SECTION000271000000000000000"></a>
## Conventional scheme

Using the conventional diagonalization method, OpenMX Ver. 3.9 is capable of performing
geometry optimization for systems consisting of 1000 atoms if several hundreds processor cores
are available. To demonstrate the capability, one can perform 'runtestL2' as follows:

```text

     % mpirun -np 128 openmx -runtestL2 -nt 4
```

Then, OpenMX will run with 7 test files, and compare calculated results with the reference
results which are stored in 'work/large2_example'.
The following is a result of 'runtestL2' performed using 640 MPI processes and 1 OpenMP threads on a Xeon cluster machine.

| 1 | large2_example/C1000.dat | Elapsed time(s)= 777.60 | diff Utot= 0.000000007341 | diff Force= 0.000000008795 |
| --- | --- | --- | --- | --- |
| 2 | large2_example/Fe1000.dat | Elapsed time(s)= 8181.70 | diff Utot= 0.000000002241 | diff Force= 0.000000011061 |
| 3 | large2_example/GRA1024.dat | Elapsed time(s)= 927.20 | diff Utot= 0.000000012903 | diff Force= 0.000000004981 |
| 4 | large2_example/Ih-Ice1200.dat | Elapsed time(s)= 445.88 | diff Utot= 0.000000000216 | diff Force= 0.000000001451 |
| 5 | large2_example/Pt500.dat | Elapsed time(s)= 2629.20 | diff Utot= 0.000000015832 | diff Force= 0.000000001879 |
| 6 | large2_example/R-TiO2-1050.dat | Elapsed time(s)= 844.58 | diff Utot= 0.000000002263 | diff Force= 0.000000001108 |
| 7 | large2_example/Si1000.dat | Elapsed time(s)= 658.53 | diff Utot= 0.000000000404 | diff Force= 0.000000000908 |

Total elapsed time (s) 14464.69

The quality of all the calculations is at a level of production run where double valence plus a single polarization
functions are allocated to each atom as basis functions. Except for 'Pt500.dat', all the systems include more than
1000 atoms, where the last number of the file name implies the number of atoms for each system, and the elapsed time
implies that geometry optimization for systems consisting of 1000 atoms
is possible if several hundreds processor cores are available. The input files used for the calculations and the output
files are found in the directory 'work/large2_example'.
The following information is compiled from the output files.

| No. | Input file | SCF steps | Elapsed time(s/SCF/spin) | Dimension |
| --- | --- | --- | --- | --- |
| 1 | large2_example/C1000.dat | 53 | 14.7 | 13000 |
| 2 | large2_example/Fe1000.dat | 408 | 10.0 | 13000 |
| 3 | large2_example/GRA1024.dat | 72 | 12.9 | 13312 |
| 4 | large2_example/Ih-Ice1200.dat | 57 | 7.8 | 9200 |
| 5 | large2_example/Pt500.dat | 161 | 16.3 | 12500 |
| 6 | large2_example/R-TiO2-1050.dat | 38 | 22.2 | 15750 |
| 7 | large2_example/Si1000.dat | 45 | 14.6 | 13000 |

The dimension of the Kohn-Sham Hamiltonian is of the order of 10000, and the elapsed time per SCF step
is around 15 seconds for all the systems, implying that the difference in the total elapsed time mainly comes
from the difference in the SCF iterations to achieve the SCF convergence of 10e-10 (Hartree) for the band energy.
