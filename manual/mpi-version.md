<a id="SECTION00043000000000000000"></a>
## MPI version

To proceed the installation of the MPI version, move to the directory
'source', and modify 'makefile' in 'source' to specify
the compiler and libraries by **CC**, **FC**, and **LIB**.
The default specification of **CC**, **FC**, and **LIB** in
'makefile' is as follows:

```text

     MKLROOT = /opt/intel/mkl
     CC = mpicc -O3 -xHOST -ip -no-prec-div -qopenmp -I/opt/intel/mkl/include/fftw
     FC = mpif90 -O3 -xHOST -ip -no-prec-div -qopenmp
     LIB= -L${MKLROOT}/lib/intel64 -lmkl_scalapack_lp64 -lmkl_intel_lp64 \
          -lmkl_intel_thread -lmkl_core -lmkl_blacs_open mpi_lp64 \
          -lmpi_usempif08 -lmpi_usempi_ignore_tkr \
          -lmpi_mpifh -liomp5 -lpthread -lm -ldl
```

**CC** and **FC** are the specification for C and FORTRAN compilers, respectively,
and **LIB** is the specification for libraries which are linked.
Although the specification of **FC** is not required up to and including Ver. 3.6,
**FC** must be specified in Ver. 3.9 due to the introduction of the ELPA based parallel
eigensolver [[39](bibliography.md#ELPA)]. The option '-Dnoomp' should be added under environment that OpenMP
is not available.
You need to set the **CC**, **FC** and **LIB** appropriately
on your computer environment so that the compilation and linking can be properly performed
and the executable file can be well optimized, while the specification largely depends on your computer
environment.
After specifying **CC**, **FC** and **LIB** appropriately, then install as follows:

```text

     % make install
```

When the compilation is completed normally, then you can find
the executable file 'openmx' in the directory 'work'.
To make the execution of OpenMX efficient, you can change a compiler and
compile options appropriate for your computer environment,
which can generate an optimized executable file.
Several examples for **CC**, **FC** and **LIB** can be found in 'makefile'
in the directory 'source' for your convenience.
