<a id="SECTION000502000000000000000"></a>
## How to perform

The NEB calculation is performed by the following three steps:

1. Geometry optimization of a precursor
2. Geometry optimization of a product
3. Optimization of a minimum energy path (MEP) connecting the precursor and product

where in the three calculations users have to keep the same computational parameters
such as unit cell, cutoff energy, basis functions, pseudopotentials, and electronic
temperatures to avoid numerical inconsistency.
After the calculations 1 and 2, files '*System.Name*.dat#' are generated. By using the atomic
coordinates in the files '*System.Name*.dat#', one can easily construct an input file for
the calculation 3. Once you have an input file for the calculation 3, the execution
of the NEB calculation is the same as for the conventional OpenMX calculation such as

```text

  % mpirun -np 32 openmx input.dat -nt 4
```

---
