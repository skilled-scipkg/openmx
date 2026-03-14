<a id="SECTION000310000000000000000"></a>
# LCAO coefficients

<a id="1720"></a>
It is possible to analyze LCAO coefficients in both the cluster
and band calculations.
In the cluster calculation, if a keyword 'level.of.fileout''
is set in '2', the LCAO coefficients are added into a file '*System.Name*.out'.
As an example, LCAO coefficients of
'Methane.dat' discussed in the Section 'Test calculation'
are shown below:

```text

***********************************************************
***********************************************************
  Eigenvalues (Hartree) and Eigenvectors for SCF KS-eq.
***********************************************************
***********************************************************

   Chemical Potential (Hartree) =   0.00000000000000
   HOMO =  4

   LCAO coefficients for up (U) and down (D) spins

                          1 (U)     2 (U)     3 (U)     4 (U)     5 (U)     6 (U)
                        -0.69899  -0.41525  -0.41525  -0.41524   0.21215   0.21215

   1   C 0 s             0.69137  -0.00000   0.00000   0.00000   0.00000   0.00000
         0 px            0.00000  -0.10055   0.63544   0.00033  -0.68649  -1.00467
         0 py            0.00000   0.00028  -0.00029   0.64331   0.00000  -0.00001
         0 pz           -0.00000   0.63544   0.10055  -0.00023  -1.00467   0.68649
   2   H 0 s             0.12870   0.05604  -0.35474  -0.25425  -0.59781  -0.87489
   3   H 0 s             0.12870  -0.35475  -0.05627   0.25420  -0.87488   0.59781
   4   H 0 s             0.12870   0.35497   0.05604   0.25393   0.87488  -0.59781
   5   H 0 s             0.12870  -0.05626   0.35497  -0.25388   0.59781   0.87488

                          7 (U)     8 (U)
                         0.21223   0.24739

   1   C 0 s             0.00000   1.90847
         0 px            0.00000   0.00000
         0 py           -1.21683  -0.00000
         0 pz           -0.00000   0.00000
   2   H 0 s            -0.74926  -0.76083
   ......
   ....
```

In bulk calculations, if a keyword 'MO.fileout' is set to 'ON',
LCAO coefficients at k-points which are specified by the keyword
'MO.kpoint' are output into a file '*System.Name*.out'.
For cluster calculations, 'level.of.fileout'
should be 2 in order to output LCAO coefficients.
But, for band calculations, the relevant keyword
is 'MO.fileout' rather than
'level.of.fileout'.

---
