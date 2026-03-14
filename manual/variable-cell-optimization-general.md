<a id="SECTION000171000000000000000"></a>
## General

The variable cell optimizations with/without constraints are supported in OpenMX Ver. 3.9.
The relevant keywords for the variable cell optimizations are listed below:

```text

   MD.Type                     RFC5       # OptC1|OptC2|OptC3|OptC4|OptC5
                                          # OptC6|OptC7|RFC5|RFC6|RFC7
   MD.Opt.DIIS.History          3         # default=3
   MD.Opt.StartDIIS             5         # default=5
   MD.Opt.EveryDIIS            200        # default=200
   MD.maxIter                  100        # default=1
   MD.Opt.criterion          1.0e-4       # default=0.0003 (Hartree/Bohr)
```

As confirmed, the keywords listed above are exactly the same as in the section 'Geometry optimization'.
Thus, the variable cell optimization can be controlled just like the geometry optimization.
The variable cell optimization is supported for only the collinear calculations including the plus U method,
while, however, the cell optimization for the DFT-D2 and DFT-D3 methods for vdW interaction is not supported.
By the keyword 'MD.Type', a method for the variable cell optimization is specified.
When you perform the variable cell optimization, you can choose the following option
for the keyword 'MD.Type':

- OptC1
  Cell vectors are optimized without any constraint, while keeping the initial fractional coordinates.
  The optimization is performed by a steepest decent method with a variable prefactor.
- OptC2
  Cell vectors are optimized with a constraint that angles between cell vectors are fixed at
  the initial values, while keeping the initial fractional coordinates.
  Thus, only the length of cell vectors is optimized during the optimization.
  The optimization is performed by a steepest decent method with a variable prefactor.
- OptC3
  Cell vectors are optimized with a constraint that angles between cell vectors are fixed at
  the initial values and the length of cell vectors is equivalent to each other:

  $\vert {\bf a}_1\vert=\vert {\bf a}_2\vert=\vert {\bf a}_3\vert$,
  while keeping the initial fractional coordinates during the optimization.
  Thus, only the length of cell vectors is optimized.
  The optimization is performed by a steepest decent method with a variable prefactor.
- OptC4
  Cell vectors are optimized with a constraint that angles between cell vectors are fixed at
  the initial values and the length of cell vectors is optimized under a condition:

  $\vert {\bf a}_1\vert=\vert {\bf a}_2\vert\neq\vert {\bf a}_3\vert$,
  while keeping the initial fractional coordinates.
  Thus, only the length of cell vectors is optimized during the optimization.
  The optimization is performed by a steepest decent method with a variable prefactor.
- OptC5
  Cell vectors and internal coordinates are simultaneously optimized without any constraint
  by using a steepest decent method with a variable prefactor.
- OptC6
  Cell vectors and internal coordinates are simultaneously optimized with a constraint
  that a cell vector ${\bf a}_3$ is fixed. The optimization is performed
  with a steepest decent method with a variable prefactor.
- OptC7
  Cell vectors and internal coordinates are simultaneously optimized with a constraint
  that two cell vectors ${\bf a}_2$ and ${\bf a}_3$ are fixed.
  The optimization is performed
  with a steepest decent method with a variable prefactor.
- RFC5
  Cell vectors and internal coordinates are simultaneously optimized without any constraint
  by using a combination scheme of the rational function (RF) method [[64](bibliography.md#Banerjee)] and
  the direct inversion iterative sub-space (DIIS) method [[62](bibliography.md#Csaszar)]
  with a BFGS update [[65](bibliography.md#BFGS)] for the approximate Hessian.
  The initial Hessian is given by an identity matrix or a model Hessian by Schlegel [[66](bibliography.md#Schlegel)],
  which can be specified by the keyword 'MD.Opt.Init.Hessian' in the same way as
  in the geometry optimization. See the details for the section 'Geometry optimization'.
- RFC6
  Cell vectors and internal coordinates are simultaneously optimized witht a constraint
  that a cell vector ${\bf a}_3$ is fixed. The optimization is performed
  with the same way as for the RFC5.
- RFC7
  Cell vectors and internal coordinates are simultaneously optimized witht a constraint
  that two cell vectors ${\bf a}_2$ and ${\bf a}_3$ are fixed. The optimization is performed
  with the same way as for the RFC5.

Depending on your purpose, one of the options listed above should be properly chosen. Other constraint
schemes will be implemented in future work.

As an example of the variable cell optimization, we show the simultaneous optimization of cell vectors and
internal coordinates for the diamond primitive cell below. The calculation can be performed by

```text

     % mpirun -np 16 openmx Cdia-RFC5.dat > Cdia-RFC5.std &
```

where the input file 'Cdia-RFC5.dat' can be found in the directory 'work/cellopt_example', so that you can trace the same
calculation.
As an illustration the initial structure is distorted as shown below:

```text

   Atoms.Number         2
   Atoms.SpeciesAndCoordinates.Unit   frac # Ang|AU
   <Atoms.SpeciesAndCoordinates
      1    C    0.10000000000000    0.00000000000000   -0.05000000000000     2.0     2.0
      2    C    0.25000000000000    0.25000000000000    0.25000000000000     2.0     2.0
   Atoms.SpeciesAndCoordinates>
   Atoms.UnitVectors.Unit             Ang # Ang|AU
   <Atoms.UnitVectors
     1.6400  1.6400  0.0000
     1.6400  0.0000  1.6400
     0.0000  1.6400  1.6400
   Atoms.UnitVectors>
```

Using a cluster machine consisting of Intel Xeon of 2.6 GHz, the elapsed time of
the calculation was 326 sec., which corresponds to 12 optimization steps.
The history of the total energy and the maximum gradients of the total energy
with respect to atomic coordinates or cell vectors
can be confirmed in '*System.Name*.out'. You may find the following information in 'Cdia-RFC5.out'
for the case.

```text

***********************************************************
***********************************************************
                History of cell optimization
***********************************************************
***********************************************************

MD_iter   SD_scaling     |Maximum force|   Maximum step        Utot             Enpy           Volume
                         (Hartree/Bohr)        (Ang)         (Hartree)        (Hartree)        (Ang^3)

  1       1.25981732       0.16438857       0.10583545     -11.59621750     -11.59621750       8.82188800
  2       1.25981732       0.08853079       0.05902053     -11.64994330     -11.64994330       9.81261691
  3       1.25981732       0.04581932       0.03054622     -11.66453803     -11.66453803      10.28662955
  4       1.25981732       0.02205340       0.01470227     -11.66928384     -11.66928384      10.56026328
  5       3.14954331       0.01336972       0.02228286     -11.67121215     -11.67121215      10.73689973
  6       3.14954331       0.00678359       0.01130598     -11.67332696     -11.67332696      11.04288573
  7       3.14954331       0.00487464       0.01195765     -11.67421713     -11.67421713      11.13669753
  8       3.14954331       0.00354039       0.02370087     -11.67479906     -11.67479906      11.18107598
  9       3.14954331       0.00157491       0.00373195     -11.67534267     -11.67534267      11.29495641
 10       3.14954331       0.00137813       0.00160469     -11.67537385     -11.67537385      11.34330266
 11       3.14954331       0.00067979       0.00165878     -11.67538616     -11.67538616      11.37836604
 12       3.14954331       0.00003708       0.00000000     -11.67538985     -11.67538985      11.39519327
```

It can be seen that the absolute value of the maximum gradient rapidly converged, and dropped
to below the criterion of $0.0003$ Hartree/bohr.

Other examples (input and output files) for the variable cell optimization can be found
in a directory 'work/cellopt_example'.
