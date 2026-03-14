<a id="SECTION00044000000000000000"></a>
## MPI/OpenMP version

To generate the MPI/OpenMP hybrid version, all you have to do
is to include a compiler option for OpenMP parallelization for **CC** and **FC**
in 'makefile' in the directory 'source'.
To proceed the installation of the MPI/OpenMP version, move to the directory 'source',
and specify **CC**, **FC** and **LIB** in 'makefile', for example, as follows:

For icc

```text

     CC = mpicc -O3 -xHOST -ip -no-prec-div -qopenmp -I/opt/intel/mkl/include/fftw
     FC = mpif90 -O3 -xHOST -ip -no-prec-div -qopenmp
```

Note that the compiler option for OpenMP depends on compiler,
while the option corresponds to '-qopenmp' for the Intel compiler,
After specifying **CC**, **FC**, and **LIB** appropriately,
then install as follows:

```text

     % make install
```

When the compilation is completed normally, then you can
find the executable file 'openmx' in the directory 'work'.
To make the execution of OpenMX efficient, you can change a compiler and
compile options appropriate for your computer environment,
which can generate an optimized executable file.

---
