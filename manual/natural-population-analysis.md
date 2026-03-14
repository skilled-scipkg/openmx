<a id="SECTION000340000000000000000"></a>
# Natural population analysis

In the natural bond orbital (NBO) method developed by Weinhold [[6](bibliography.md#Weinhold)],
atomic population (or atomic charge) is calculated based on atomically localized orbitals,
natural atomic orbitals (NAO), which is referred to as natural population (NP).
OpenMX supports the NP analysis. Especially, for large-sized calculation models,
one can efficiently calculate and analyze NPs by selecting target atoms, which is an original scheme
based on a truncated cluster method [[7](bibliography.md#Ohwaki2014)]. In OpenMX, the NP calculation is carried out
after the SCF calculation, and results of NP analysis are shown in a standard output.
The way of NP calculation is as follows:

<a id="1820"></a>
**(a) Case of small-sized calculation (scf.EigenvalueSolver = Cluster)**

The NP calculation is supported by the following keyword :

```text

    NBO.switch   on1
```

This type of NP calculation is supported in case of 'scf.EigenvalueSolver = Cluster',
and carried out by using a full-sized density matrix.
As a sample of this type of NP calculation, users can refer to an input and output files for
an ethylene carbonate (EC) molecule including 10 atoms, 'EC_NAO.dat' and 'EC_NAO.std',
which are stored in a directory 'work/nbo_example'.

**(b) Case of large-size calculation (scf.EigenvalueSolver = Krylov)**

The NAO calculation for a large-sized model carried out with 'NBO.switch = on1'
will be sometimes hampered by memory shortage due to the large-sized density matrix.
For the NP calculation of a large-sized model, the following option for
the keyword 'NBO.switch' is available

```text

    NBO.switch   on2
```

The option 'on2' has to be used with the O(N) Krylov subspace calculation
(scf.EigenvalueSolver = Krylov). After the O(N) SCF calculation,
the NP calculation can be efficiently performed by selecting a few atoms
you are interested in.
When a large-sized model is treated, it is not always necessary for one
to calculate NPs for all atoms, that is, in most cases, NP analysis on
a few atoms in local regions is enough to investigate important events
such as chemical reactions. In OpenMX, target atoms for the NP analysis
can be selected by the following keywords:

```text

    NBO.Num.CenterAtoms     5
    <NBO.CenterAtoms
      269
      304
      323
      541
      574
    NBO.CenterAtoms>
```

By the keyword 'NBO.Num.CenterAtoms' , one designates the number of target atoms.
Between '$<$NBO.CenterAtoms' and 'NBO.CenterAtoms$>$', one describes serial indexes of
target atoms, which are specified by the keyword 'Atoms.SpeciesAndCoordinates'.
The keyword 'NBO.CenterAtoms' is valid only if 'on2' is chosen for 'NBO.switch'.
In case of 'on1' for the keyword 'NBO.switch', NPs for all atoms will be calculated regardless of
the specification of the keyword 'NBO.CenterAtoms'.
As a sample of the NP calculation for a large-sized model,
you can refer to an input and output files for amorphous SiO2 bulk system (648 atoms),
'SiO2_NAO.dat' and 'SiO2_NAO.std', which are stored in the directory 'work/nbo_example'.

<a id="1836"></a>
**(c) Parameter for NAO calculation: NAO.threshold**

The NAO calculation has a process of distinguishing occupied and Rydberg (low-occupied) NAOs.
The criterion of the distinction is given by the keyword 'NAO.threshold',
by which one designates the number of electrons per spin orbital.
The default value of this parameter is 0.85, with which most of NAO calculations
are executed normally. If the obtained number of occupied NAOs is abnormal,
you may need to adjust the value of 'NAO.threshold' .

**(d) Example**

Here the result of NP calculation for the EC molecule is shown. First, NPs for all the atoms
and summation of those NPs are output in the standard output as follows:

```text

     1   O :   6.46917105 
     2   C :   4.09908587 
     3   C :   4.09909317  
     4   O :   6.46902031 
     5   C :   3.14623972 
     6   O :   6.50714720 
     7   H :   0.80250093 
     8   H :   0.80249967 
     9   H :   0.80262024 
    10   H :   0.80262185 
  ------------------------
    Total  :  34.00000000 

   ## Global atom num.: 1 ( O ) / NP =   6.4692
  ---------------------------------------------------------------------------------
   NP in NAO         0.0013  1.6803  0.0046  1.6731  0.0055  1.3000  0.0073  1.7972
   Energy (Hartree)  1.2529 -0.7196  0.4452 -0.3208  0.7108 -0.2935  0.4327 -0.3005
  ---------------------------------------------------------------------------------
   1 s              -1.8000  1.2493 -0.0776  0.1255 -0.0125 -0.0027  0.0000  0.0000
   2 s               1.9201  0.0014  0.0530 -0.0030  0.0163  0.0015 -0.0000 -0.0000
   1 px             -0.4312  0.1031 -0.6568  1.0499  0.0431  0.0115 -0.0000 -0.0000
   2 px              0.1913 -0.0062  1.7251  0.0215 -0.0500 -0.0052  0.0000  0.0000
   1 py             -0.1040 -0.0056  0.0371  0.0110 -2.1699  1.0361 -0.0000 -0.0000
   2 py              0.0573  0.0025 -0.0493 -0.0052  3.4499  0.1576  0.0000  0.0000
   1 pz              0.0000 -0.0000 -0.0000 -0.0000 -0.0000 -0.0000 -0.6206  1.0131
   2 pz             -0.0000 -0.0000  0.0000  0.0000  0.0000  0.0000  1.7312  0.0267
   ...
   ..
```

After the NPs are shown for all the atoms, NPs and energy levels of NAOs on each atom are shown
in the first and second lows, respectively, and followed by LCPAO coefficients for the corresponding NAO.
In the near future, the calculation and analysis functions of NBO will be also supposed to be implemented in OpenMX.
