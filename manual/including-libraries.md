<a id="SECTION00041000000000000000"></a>
## Including libraries

OpenMX can be installed under linux environment where three library packages are
available as listed below:

- ScaLAPACK (and BLACS) (http://www.netlib.org/)
- FFTW (http://www.fftw.org/)
- MPI library such as MPICH2 and OpenMPI

If these library packages are not installed on your machine,
you are required to install them before the installation of OpenMX.
Note that a MPI library such as MPICH2 and OpenMPI has to be available
for the installation of OpenMX Ver. 3.9. Without a MPI library, OpenMX Ver. 3.9
cannot be installed. Also, OpenMX Ver. 3.9 requires ScaLAPACK and BLACS, and
the compilation of OpenMX Ver. 3.9 with LAPACK and BLAS is not supported.
As an alternative, the Intel Math Kernel Library (MKL) can also be utilized instead of the naive ScaLAPACK and BLACS.
If these libraries packages are available on your machine,
you can proceed the following procedure for the installation.
Then, after downloading 'openmx3.9.tar.gz', decompress it as follows:

```text

     % tar zxvf openmx3.9.tar.gz
```

When it is completed, you can find three directories 'source', 'work', 'DFT_DATA19'
under the directory 'openmx3.9'.
The directories 'source', 'work', and 'DFT_DATA19'
contain source files, input files, and data files for optimized pseudo-atomic
basis functions and pseudopotentials of Ver. 2019, respectively.

---
