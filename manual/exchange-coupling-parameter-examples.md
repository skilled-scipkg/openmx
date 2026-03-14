<a id="SECTION000436000000000000000"></a>
## Examples

As an example of the **cluster case**, using an input file 'Fe_Cluster_jx.dat' which is stored in the directory 'work',
you can first perform a conventional calculation using 'openmx' as

```text

     % mpirun -np 2 ./openmx Fe_Cluster_jx.dat
```

The input file 'Fe_Cluster_jx.dat' is for the SCF calculation of a iron dimer.
After finishing the calculation normally, you can obtain a scfout file 'Fe_Cluster_jx.scfout'.
Then the calculation by 'jx' is performed as

```text

     % ./jx Fe_Cluster_jx.scfout jx_cluster.config
```

where 'jx_cluster.config' is also available in the directory 'work'.
Then, you may see the following message on your screen.

```text

     ********************************************************************
     ********************************************************************
      jx: code for calculating an effective exchange coupling constant J 
      Copyright (C), 2003, Myung Joon Han, Jaejun Yu, and Taisuke Ozaki 
                     2019, Asako Terasawa and Taisuke Ozaki 
      This is free software, and you are welcome to         
      redistribute it under the constitution of the GNU-GPL.
     ********************************************************************
     ********************************************************************

     Read the scfout file (Fe_Cluster_jx.scfout)
     ***
     The file format of the SCFOUT file:  3
     And it supports the following functions:
     - jx
     - polB
     - kSpin
     - Z2FH
     - calB
     ***

      Previous eigenvalue solver = Cluster
      atomnum                    = 2
      ChemP                      = -0.089740215968 (Hartree)
      E_Temp                     = 300.000000000000 (K)
 
     Evaluation of J based on cluster calculation
 
         i     j            J [meV]            J [mRy]
     -------------------------------------------------
         1     1   1591.520791120630    116.974621661729
         1     2    106.511867492210      7.828477938772
         2     2   1591.520746009061    116.974618346089

      Elapsed time = 0.036225 (s)
```

The exchange coupling constant $J_{12}$ between atoms 1 and 2 is calculated to be 106.5 meV.

As an example of the **bulk case**, you can perform a conventional calculation using 'openmx'
and an input file 'Fe_Bulk_jx.dat' available in the directory 'work' as

```text

     % mpirun -np 28 ./openmx Fe_Bulk_jx.dat
```

The input file 'Fe_Bulk_jx.dat' is for the SCF calculation of a BCC iron.
After finishing the calculation normally, you can obtain a scfout file 'Fe_Bulk_jx.scfout'.
Then the calculation by 'jx' is performed as

```text

     % mpirun -np 112 ./jx Fe_Bulk_jx.scfout Fe_Bulk_jx.config | tee jx.log
```

where 'Fe_Bulk_jx.config' is available in the directory 'work'.
Then, you may see the following message on your screen.

```text

   ********************************************************************
   ********************************************************************
    jx: code for calculating an effective exchange coupling constant J 
    Copyright (C), 2003, Myung Joon Han, Jaejun Yu, and Taisuke Ozaki 
                   2019, Asako Terasawa and Taisuke Ozaki 
    This is free software, and you are welcome to         
    redistribute it under the constitution of the GNU-GPL.
   ********************************************************************
   ********************************************************************

   Read the scfout file (Fe_Bulk_jx.scfout)
   ***
   The file format of the SCFOUT file:  3
   And it supports the following functions:
   - jx
   - polB
   - kSpin
   - Z2FH
   - calB
   ***

    Previous eigenvalue solver = Band
    atomnum                    = 2
    ChemP                      = -0.205912787451 (Hartree)
    E_Temp                     = 300.000000000000 (K)

    Jij calculation for a periodic structure
      Number of k-grids: 27 27 27 
      flag_periodic_sum = 0: coupling between site i at cell 0 and site j at cell R 
        Number of poles of Fermi-Dirac continued fraction (PRB.75.035123): 60

       i     j    c1    c2    c3            J [meV]            J [mRy]   time_eig [s] ...
   ---------------------------------------------------------------------------------- ...
       1     1    -2    -2    -2    -0.845809571401    -0.062165857439        0.51534 ...
       1     1    -2    -2    -1     0.274300677331     0.020160728111        0.00000 ...
       1     1    -2    -2     0     0.036006012552     0.002646393135        0.00000 ...
       1     1    -2    -2     1     0.274300705154     0.020160730156        0.00000 ...
       1     1    -2    -2     2    -0.845809596417    -0.062165859278        0.00000 ...
       1     1    -2    -1    -2     0.274300737539     0.020160732536        0.00000 ...
       1     1    -2    -1    -1    -0.206315672897    -0.015163922403        0.00000 ...
       1     1    -2    -1     0     0.149714301525     0.011003798302        0.00000 ...
       1     1    -2    -1     1    -0.206315540488    -0.015163912672        0.00000 ...
       1     1    -2    -1     2     0.274300804604     0.020160737465        0.00000 ...
       ...
       ..
       2     2     0    -1     2     0.149714016159     0.011003777328        0.00000 ...
       2     2     0     0    -2     0.401809366424     0.029532443987        0.00000 ...
       2     2     0     0    -1    11.452192349598     0.841720620155        0.00000 ...

    Elapsed time = 340.817975 (s)
```

In Fig. [38](exchange-coupling-parameter-examples.md#fig:jx_examples) (a), the obtained exchange coupling constant $J$ for the bcc Fe
is plotted as a function of distance as well as cases of (b) hcp Co, (c) fcc Ni, and (d) Fe dimer.
In all the calculations, basis sets of A6.0H-s2p2d2 (A=Fe, Ni, Co), exchange correlation functions
of GGA-PBE, and ferromagnetic spin configurations are adopted. The input files used for the calculations
are Fe_Bulk_jx.(dat,config), Co_Bulk_jx.(dat,config), Ni_Bulk_jx.(dat,config), and Fe_Cluster_jx.(dat,config)
which are all available in the directory 'work'. The details of the calculations can be found in Ref. [[19](bibliography.md#Terasawa2019)].

It is also possible to calculate the Curie temperature of periodic systems from calculated exchange coupling
constants and the mean field approximation.
That is, the Curie temperature
$T_{\mathrm{C}}$ of general periodic system can
be obtained as the maximum eigenvalue of the following eigenvalue equation:

<a id="eq:jx_curie"></a>
| $\displaystyle T\langle\vec{s}_{i}\rangle_{z}$ | $\textstyle =$ | $\displaystyle \frac{2}{3 k_{\mathrm{B}}}\sum_{j}\tilde{J}_{ij}\langle\vec{s}_{j}\rangle_{z}$ | (9) |
| --- | --- | --- | --- |
| $\displaystyle \tilde{J}_{ij}$ | $\textstyle \equiv$ | $\displaystyle J_{ij}-J_{i\mathbf{0},j\mathbf{0}}\delta_{ij}.$ | (10) |

Here, the definitions of $J_{ij}$ and
$J_{i\mathbf{0},j\mathbf{0}}$ are found
in Eqs. ([5](exchange-coupling-parameter-general.md#eq:Jij_indiv_res)) and ([8](exchange-coupling-parameter-general.md#eq:Jij_periodic)), respectively.
Table [8](exchange-coupling-parameter-examples.md#table:jx_curie_temperature) shows the calculated Curie temperature by Eq. ([9](exchange-coupling-parameter-examples.md#eq:jx_curie))
for the bcc Fe, hcp Co, and fcc Ni together with the experimental values.

<a id="fig:jx_examples"></a>
<a id="2470"></a>
| ![\includegraphics[width=160mm]{jx_examples.eps}](assets/img268.png) |
| --- |

<a id="6320"></a>
| $T_\mathrm{C}$ [K]

System
calculated
experimental

bcc Fe
1321
1040

hcp Co
1640
1131

fcc Ni
445
627 |  |  |
| --- | --- | --- |
|  | $T_\mathrm{C}$ [K] |  |
| System | calculated | experimental |
| bcc Fe | 1321 | 1040 |
| hcp Co | 1640 | 1131 |
| fcc Ni | 445 | 627 |
