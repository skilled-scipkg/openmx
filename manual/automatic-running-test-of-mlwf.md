<a id="SECTION000456000000000000000"></a>
## Automatic running test of MLWF

To check whether the MLWF calculation part is properly installed or not,
an automatic running test for the MLWF calculation can be performed by

**For the MPI parallel running**

```text

  % mpirun -np 16 openmx -runtestWF
```

**For the MPI/OpenMP parallel running**

```text

  % mpirun -np 8 openmx -runtestWF -nt 2
```

Then, OpenMX will run with eight test cases, and compare calculated
results with the reference results which are stored in 'work/wf_example'.
The comparison (absolute difference in the spread and $\Omega$ functions) is
stored in a file 'runtestWF.result' in the directory 'work'.
The reference results were calculated using a Xeon cluster machine.
If the difference is within last
seven digits, we may consider that the installation is successful.

---
