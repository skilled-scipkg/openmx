<a id="SECTION00050000000000000000"></a>
# Test calculation

If the installation is completed normally, please move to the directory
'work' and perform the program 'openmx' using an input file
'Methane.dat' which can be found in the directory 'work' as follows:

```text

     % mpirun -np 1 openmx Methane.dat > met.std &
```

Or if you use the MPI/OpenMP version:

```text

     % mpirun -np 1 openmx Methane.dat -nt 1 > met.std &
```

The test input file 'Methane.dat' is for performing the SCF calculation
of a methane molecule with a fixed structure (No MD). The calculation is
performed in only about 5 seconds by using a single core on a 2.6 GHz Xeon machine,
although it is dependent on a computer. When the calculation is completed
normally, 11 files and one directory

```text

      met.std               standard output of the SCF calculation    
      met.out               input file and standard output    
      met.xyz               final geometrical structure  
      met.ene               values computed at every MD step
      met.md                geometrical structures at every MD step 
      met.md2               geometrical structure of the final MD step 
      met.cif               cif file of the initial structure for Material Studio 
      met.tden.cube         total electron density in the Gaussian cube format 
      met.v0.cube           Kohn-Sham potential in the Gaussian cube format 
      met.vhart.cube        Hartree potential in the Gaussian cube format 
      met.dden.cube         difference electron density measured from atomic density 
      met_rst/              directory storing restart files
```

are output to the directory 'work'.
The output data to a standard output is stored to the file 'met.std'
which is helpful to know the computational flow of the SCF procedure.
The file 'met.out' includes computed results such as the total
energy, forces, the Kohn-Sham eigenvalues, Mulliken charges, the convergence
history for the SCF calculation, and analyzed computational time.
A part of the file 'met.out' is shown below. It is found that
the eigenvalues energy converges by 14 iterations
within 1.0e-10 Hartree.

```text

***********************************************************
***********************************************************
                  SCF history at MD= 1
***********************************************************
***********************************************************

   SCF=   1  NormRD=  1.000000000000  Uele= -3.523169099731
   SCF=   2  NormRD=  0.181517404404  Uele= -3.686855123738
   SCF=   3  NormRD=  0.449067381009  Uele= -4.193062144919
   SCF=   4  NormRD=  0.541215648203  Uele= -4.381387140154
   SCF=   5  NormRD=  0.509921689399  Uele= -4.352426233337
   SCF=   6  NormRD=  0.004026023243  Uele= -3.886371199720
   SCF=   7  NormRD=  0.000838640096  Uele= -3.889312346884
   SCF=   8  NormRD=  0.000420666755  Uele= -3.889396659132
   SCF=   9  NormRD=  0.000241013350  Uele= -3.889362708861
   SCF=  10  NormRD=  0.000573725679  Uele= -3.889427222948
   SCF=  11  NormRD=  0.000000150516  Uele= -3.889316043314
   SCF=  12  NormRD=  0.000000001917  Uele= -3.889316014533
   SCF=  13  NormRD=  0.000000000005  Uele= -3.889316014156
   SCF=  14  NormRD=  0.000000000001  Uele= -3.889316014146
```

Also, the total energy, chemical potential, Kohn-Sham eigenvalues,
the Mulliken charges, dipole moment, forces, fractional coordinate,
and analysis of computational time are output in 'met.out' as follows:

```text

*******************************************************
        Total energy (Hartree) at MD = 1
*******************************************************

  Uele.         -3.889316014146

  Ukin.          5.533759381370
  UH0.         -14.855519969177
  UH1.           0.041396138425
  Una.          -5.040606545149
  Unl.          -0.134650846490
  Uxc0.         -1.564720263874
  Uxc1.         -1.564720263874
  Ucore.         9.551521413583
  Uhub.          0.000000000000
  Ucs.           0.000000000000
  Uzs.           0.000000000000
  Uzo.           0.000000000000
  Uef.           0.000000000000
  UvdW           0.000000000000
  Uch            0.000000000000
  Utot.         -8.033540955187

  Note:

  Utot = Ukin+UH0+UH1+Una+Unl+Uxc0+Uxc1+Ucore+Uhub+Ucs+Uzs+Uzo+Uef+UvdW

  Uene:   band energy
  Ukin:   kinetic energy
  UH0:    electric part of screened Coulomb energy
  UH1:    difference electron-electron Coulomb energy
  Una:    neutral atom potential energy
  Unl:    non-local potential energy
  Uxc0:   exchange-correlation energy for alpha spin
  Uxc1:   exchange-correlation energy for beta spin
  Ucore:  core-core Coulomb energy
  Uhub:   DFT+U energy
  Ucs:    constraint energy for spin orientation
  Uzs:    Zeeman term for spin magnetic moment
  Uzo:    Zeeman term for orbital magnetic moment
  Uef:    electric energy by electric field
  UvdW:   semi-empirical vdW energy

  (see also PRB 72, 045121(2005) for the energy contributions)

  Chemical potential (Hartree)       0.000000000000

***********************************************************
***********************************************************
           Eigenvalues (Hartree) for SCF KS-eq.
***********************************************************
***********************************************************

   Chemical Potential (Hartree) =   0.00000000000000
   Number of States             =   8.00000000000000
   HOMO =  4
   Eigenvalues
                Up-spin            Down-spin
          1  -0.69897506408475  -0.69897506408475
          2  -0.41523055776668  -0.41523055776668
          3  -0.41523055768741  -0.41523055768741
          4  -0.41522182758055  -0.41522182758055
          5   0.21221759603691   0.21221759603691
          6   0.21221759685634   0.21221759685634
          7   0.21230533059490   0.21230533059490
          8   0.24741918440773   0.24741918440773

***********************************************************
***********************************************************
                   Mulliken populations
***********************************************************
***********************************************************

  Total spin moment (muB)   0.000000000

                    Up spin      Down spin     Sum           Diff
      1    C      2.509748760  2.509748760   5.019497520   0.000000000
      2    H      0.372562810  0.372562810   0.745125620   0.000000000
      3    H      0.372562810  0.372562810   0.745125620   0.000000000
      4    H      0.372562810  0.372562810   0.745125620   0.000000000
      5    H      0.372562810  0.372562810   0.745125620   0.000000000

 Sum of MulP: up   =     4.00000 down          =     4.00000
              total=     8.00000 ideal(neutral)=     8.00000

  Decomposed Mulliken populations
    1    C          Up spin      Down spin     Sum           Diff
            multiple
  s           0    0.681737894  0.681737894   1.363475787   0.000000000
   sum over m      0.681737894  0.681737894   1.363475787   0.000000000
   sum over m+mul  0.681737894  0.681737894   1.363475787   0.000000000
  px          0    0.609352701  0.609352701   1.218705403   0.000000000
  py          0    0.609305463  0.609305463   1.218610926   0.000000000
  pz          0    0.609352702  0.609352702   1.218705404   0.000000000
   sum over m      1.828010866  1.828010866   3.656021733   0.000000000
   sum over m+mul  1.828010866  1.828010866   3.656021733   0.000000000

    2    H          Up spin      Down spin     Sum           Diff
            multiple
  s           0    0.372562810  0.372562810   0.745125620   0.000000000
   sum over m      0.372562810  0.372562810   0.745125620   0.000000000
   sum over m+mul  0.372562810  0.372562810   0.745125620   0.000000000

    3    H          Up spin      Down spin     Sum           Diff
            multiple
  s           0    0.372562810  0.372562810   0.745125620   0.000000000
   sum over m      0.372562810  0.372562810   0.745125620   0.000000000
   sum over m+mul  0.372562810  0.372562810   0.745125620   0.000000000

    4    H          Up spin      Down spin     Sum           Diff
            multiple
  s           0    0.372562810  0.372562810   0.745125620   0.000000000
   sum over m      0.372562810  0.372562810   0.745125620   0.000000000
   sum over m+mul  0.372562810  0.372562810   0.745125620   0.000000000

    5    H          Up spin      Down spin     Sum           Diff
            multiple
  s           0    0.372562810  0.372562810   0.745125620   0.000000000
   sum over m      0.372562810  0.372562810   0.745125620   0.000000000
   sum over m+mul  0.372562810  0.372562810   0.745125620   0.000000000

***********************************************************
***********************************************************
                    Dipole moment (Debye)
***********************************************************
***********************************************************

 Absolute D        0.00000000

                      Dx                Dy                Dz
 Total              0.00000000        0.00000000        0.00000000
 Core               0.00000000        0.00000000        0.00000000
 Electron           0.00000000        0.00000000        0.00000000
 Back ground       -0.00000000       -0.00000000       -0.00000000

***********************************************************
***********************************************************
       xyz-coordinates (Ang) and forces (Hartree/Bohr)
***********************************************************
***********************************************************

<coordinates.forces
  5
    1     C     0.00000   0.00000   0.00000   0.000000000000  0.00...
    2     H    -0.88998  -0.62931   0.00000  -0.064890985127 -0.04...
    3     H     0.00000   0.62931  -0.88998   0.000000000002  0.04...
    4     H     0.00000   0.62931   0.88998   0.000000000002  0.04...
    5     H     0.88998  -0.62931   0.00000   0.064890985122 -0.04...
coordinates.forces>

***********************************************************
***********************************************************
       Fractional coordinates of the final structure
***********************************************************
***********************************************************

     1      C     0.00000000000000   0.00000000000000   0.00000000000000
     2      H     0.91100190000000   0.93706880000000   0.00000000000000
     3      H     0.00000000000000   0.06293120000000   0.91100190000000
     4      H     0.00000000000000   0.06293120000000   0.08899810000000
     5      H     0.08899810000000   0.93706880000000   0.00000000000000

***********************************************************
***********************************************************
               Computational Time (second)
***********************************************************
***********************************************************

   Elapsed.Time.         4.600

                               Min_ID   Min_Time       Max_ID   Max_Time
   Total Computational Time =     0        4.600          0        4.600
   readfile                 =     0        2.578          0        2.578
   truncation               =     0        0.146          0        0.146
   MD_pac                   =     0        0.000          0        0.000
   OutData                  =     0        0.283          0        0.283
   DFT                      =     0        1.591          0        1.591

*** In DFT ***

   Set_OLP_Kin              =     0        0.052          0        0.052
   Set_Nonlocal             =     0        0.039          0        0.039
   Set_ProExpn_VNA          =     0        0.156          0        0.156
   Set_Hamiltonian          =     0        0.663          0        0.663
   Poisson                  =     0        0.214          0        0.214
   Diagonalization          =     0        0.005          0        0.005
   Mixing_DM                =     0        0.000          0        0.000
   Force                    =     0        0.039          0        0.039
   Total_Energy             =     0        0.256          0        0.256
   Set_Aden_Grid            =     0        0.019          0        0.019
   Set_Orbitals_Grid        =     0        0.015          0        0.015
   Set_Density_Grid         =     0        0.124          0        0.124
   RestartFileDFT           =     0        0.004          0        0.004
   Mulliken_Charge          =     0        0.000          0        0.000
   FFT(2D)_Density          =     0        0.000          0        0.000
   Others                   =     0        0.005          0        0.005
```

The files 'met.tden.cube', 'met.v0.cube', 'met.vhart.cube', and 'met.dden.cube',
are the total electron density, the Kohn-Sham potential, the Hartree potential,
and the difference electron density taken from the superposition of atomic densities
of constituent atoms, respectively, which are output in the Gaussian cube format.
Since the Gaussian cube format is one of well used grid formats, you can visualize
the files using free molecular modeling software such as VESTA [[103](bibliography.md#VESTA)],
Molekel [[104](bibliography.md#Molekel)], and XCrySDen [[105](bibliography.md#XCrySDen)].
The visualization will be illustrated in the later section.
