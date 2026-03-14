<a id="SECTION00048000000000000000"></a>
## Tips for installation

Most problems in the installation of OpenMX are caused by the linking of ScaLAPACK and BLACS or
its alternative. We would recommend users to link MKL in most cases.
Examples on how to link them can be found in 'makefile' in the directory 'source'.

Also, we provide a couple of tips for the installation on popular platforms below.
OpenMX requires C and FORTRAN compilers, ScaLAPACK and BLACS libraries, and FFTW3 library.
In addition, as the C compiler is used for linking, the corresponding FORTRAN library of the compiler
should be explicitly specified. Here we provide some sample settings for installation on platforms with
several popular compilers and ScaLAPACK and BLACS libraries under an assumption that the FFT library is
installed in /usr/local/fftw3/.

- Intel C and FORTRAN compilers (icc, ifort) and the MKL library for ScaLAPACK and BLACS
  MKLROOT = /opt/intel/mkl

  CC = mpicc -O3 -xHOST -ip -no-prec-div -qopenmp -I/usr/local/fftw3/include

  FC = mpif90 -O3 -xHOST -ip -no-prec-div -qopenmp

  LIB= -L/usr/local/fftw3/lib -lfftw3 \

  -L$MKLROOT/lib/intel64 -lmkl_scalapack_lp64 -lmkl_intel_lp64 \

  -lmkl_intel_thread -lmkl_core -lmkl_blacs_open mpi_lp64 \

  -lmpi_usempif08 -lmpi_usempi_ignore_tkr \

  -lmpi_mpifh -liomp5 -lpthread -lm -ldl
- GNU C and FORTRAN compilers (gcc, g++, gfortran) and the MKL library for ScaLAPACK and BLACS
  MKLROOT=/opt/intel/mkl

  CC = mpicc -O3 -ffast-math -fopenmp -I/usr/local/fftw3/include -I/$MKLROOT/include

  FC = mpif90 -O3 -ffast-math -fopenmp -I/$MKLROOT/include

  LIB= -L/usr/local/fftw3/lib -lfftw3 \

  -L$MKLROOT/lib/intel64 -lmkl_scalapack_lp64 -lmkl_intel_lp64 \

  -lmkl_intel_thread -lmkl_core -lmkl_blacs_open mpi_lp64 \

  -lmpi_usempif08 -lmpi_usempi_ignore_tkr \

  -lmpi_mpifh -liomp5 -lpthread -lm -ldl
- GNU C and FORTRAN compilers (gcc, g++, gfortran) and ScaLAPACK and BLACS
  CC = mpicc -O3 -ffast-math -fopenmp -Dkcomp -I/usr/local/include -I/home/ytl/openmpi-3.0.1/ompi/include

  FC = mpif90 -O3 -ffast-math -fopenmp -Dkcomp -I/home/ytl/openmpi-3.0.1/ompi/include

  LIB= -L/usr/local/lib -lfftw3 -L/home/ytl/openmpi-3.0.1/ompi -lmpi -lmpi_mpifh \

  -L/home/ytl/Packages/lapack-3.7.0 -llapack -lrefblas -lgfortran
- FUJITSU compilers on FX100 machines
  CC = mpifccpx -Kfast -Dnosse -Dkcomp

  FC = mpifrtpx -Kfast -Dkcomp

  LIB = -lfftw3 -SCALAPACK -SSL2BLAMP

Other combinations of the compiler and ScaLAPACK and BLACS libraries can be done in the same fashion.
The following commands can be used to show information about the compiler (Intel, PGI, GNU, etc.) used by MPI.

```text

      %mpicc -compile-info (with MPICH)
      %mpicc -help  (with OpenMPI)
```

In some cases, the location of the FORTRAN library is unknown to the C compiler, resulting in the following link errors:

```text

      /usr/bin/ld: cannot find -lifcore
```

with the Intel compiler,

```text

      /usr/bin/ld: cannot find -lpgf90
```

with the PGI compiler, or

```text

     -lpgf90_rpm1, -lpgf902, -lpgf90rtl, -lpgftnrtl
```

as the "-pgf90libs" flag is just a shortcut for them,

```text

      /usr/bin/ld: cannot find -lgfortran
```

with the GNU compiler.

To solve this link-time problem, the location of the FORTRAN library must be explicitly specified as follows.
First, the location of the FORTRAN compiler can be identified with the following commands.

```text

      %which ifort (with the Intel compiler)
      /opt/intel/fce/10.0.026/bin/ifort

      %which pgf90 (with the PGI compiler)
      /opt/pgi/linux86-64/7.0/bin/pgf90

      %which gfortran (with the GNU compiler)
      /usr/bin/gfortran
```

Then, the location of the FORTRAN library usually resides in /lib of the parent folder of /bin,
and must be specified in LIB such as

```text

     LIB= ... -L/opt/intel/fce/10.0.026/lib -lifcore (with the Intel compiler)
     LIB= ... -L/opt/pgi/linux86-64/7.0/lib -pgf90libs (with the PGI compiler)
     LIB= ... -L/usr/lib -lgfortran (with the GNU compiler)
```

As for the Intel Math Kernel Library, you may use the folowing website:
Intelé Math Kernel Library Link Line Advisor

```text

     https://software.intel.com/en-us/articles/intel-mkl-link-line-advisor
```

which gives us a suggestion for linking of libraries and compiler options.
