<a id="SECTION000260000000000000000"></a>
# MPI/OpenMP hybrid parallelization

The MPI/OpenMP hybrid parallel execution can be performed by

```text

   % mpirun -np 32 openmx DIA512-1.dat -nt 4 > dia512-1.std &
```

where '-nt' means the number of threads in each process managed by MPI.
If '-nt' is not specified, then the number of threads is set to 1, which
corresponds to the flat MPI parallelization.
Since the parallelization of OpenMX Ver. 3.9 is largely changed from OpenMX Ver. 3.6,
we do not have enough data to validate the hybrid parallelization compared to the flat MPI
with respect to efficiency of computation and memory usage.
However, our preliminary benchmark calculations imply that the hybrid parallelization
seems to be efficient as for memory usage,
while the computational efficiency seems to be comparable to each other.

---
