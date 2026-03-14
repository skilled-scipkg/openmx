<a id="SECTION0004411000000000000000"></a>
## Automatic running test of NEGF

To check whether the NEGF calculation part is properly installed or not,
an automatic running test for the NEGF calculation can be performed by

**For the MPI parallel running**

```text

  % mpirun -np 16 openmx -runtestNEGF
```

**For the MPI/OpenMP parallel running**

```text

  % mpirun -np 8 openmx -runtestNEGF -nt 2
```

Then, OpenMX will run with five test cases including calculations of
the steps 1 and 2, and compare calculated
results with the reference results which are stored in 'work/negf_example'.
The comparison (absolute difference in the total energy, force,
the averaged current density, the sum of the eigen transmission) is
stored in a file 'runtestNEGF.result' in the directory 'work'.
The reference results were calculated using 16 MPI processes of
a 2.6GHz Xeon machine. If the difference is within last
seven digits, we may consider that the installation is successful.

---
