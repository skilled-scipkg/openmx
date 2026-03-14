<a id="SECTION000607000000000000000"></a>
## Automatic running test

To check whether the functionality of the conductivity and dielectric function calculations is properly installed or not,
an automatic running test for the functionality can be performed by

**For the MPI parallel running**

```text

  % mpirun -np 112 ./openmx -runtestCDDF
```

**For the MPI/OpenMP parallel running**

```text

  % mpirun -np 56 ./openmx -runtestCDDF -nt 2
```

Then, OpenMX will run with five test cases, and compare calculated
results with the reference results which are stored in 'work/cddf_example'.
The comparison (absolute difference in the dielectric function) is
stored in a file 'runtestCDDF.result' in the directory 'work'.
The reference results were calculated using a Xeon cluster machine.
If the difference is less than 0.1, we may consider that the installation is successful.

---
