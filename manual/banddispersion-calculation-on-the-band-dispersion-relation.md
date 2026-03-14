<a id="SECTION000544000000000000000"></a>
<a id="sec:BandDispersion"></a>
## BandDispersion: Calculation on the band dispersion relation

'kSpin' has four ways to calculate the k-space spin density matrix, which can be specified
by a keyword 'Calc.Type'. Here we introduce *BandDispersion* among the four ways.
*BandDispersion* can calculate the k-space spin density matrix resolved to each atom
on the band dispersion relation within a user-specified energy range. First, the calculation
of the band dispersion using *BandDispersion* is illustrated here with a simple model
of an Au(111) surface.
Then, you can calculate spin textures using [53.6](mulpcalc-k-space-spin-density-matrix-resolved-to-each-atom.md#sec:MulPCalc) *MulPCalc*.

After a calculation of OpenMX with an input file 'Au111Surface_BD.dat' stored
in the directory 'work', you may try to run 'kSpin'.
The keywords relevant to the executation of kSpin can be found at the bottom of the input file
'Au111Surface_BD.dat' stored in the directory 'work' as shown below:

<a id="4136"></a>
<a id="4137"></a>
<a id="4138"></a>
<a id="4139"></a>
<a id="4140"></a>
<a id="4141"></a>
**List of keywords relevant to kSpin**

```text

    Filename.scfout      Au111Surface.scfout 
    Filename.outdata     Au111Surface_BD     
    Calc.Type            BandDispersion    # FermiLoop, GridCalc,
                                             BandDispersion, or MulPOnly 
                                             default: MulPOnly
    Energy.Range        -1.0  1.0          # eV; default: 0.0  0.0
    Band.Nkpath                2
    <Band.kpath
      135  0.0  0.500000  0.000000    0.0   0.000000  0.000000     M  G
      135  0.0  0.000000  0.000000    0.0  -0.500000  0.000000     G -M
    Band.kpath>
```

**Specification of keywords**

The specification of each keyword is explained below:

**Filename.scfout**

Specify the name of the scfout file which will be read by 'kSpin'.

**Filename.outdata**

Specify a name for output files. This keyword corresponds to the keyword 'System.Name'
for OpenMX calculations.

**Calc.Type**

Choose either *FermiLoop*, *GridCalc*, *BandDispersion*, or *MulPOnly*.
The default setting is *MulPOnly*. Here we choose *BandDispersion* for the exercise.

**Energy.Range**

Specify the two different values for an energy range for which BandDispersion should search bands.
The unit is in eV. The default is '-0.5 0.5' (i.e. the range is [-0.5, 0.5]).

**Band.Nkpath**

Specify the number of k-paths along which*BandDispersion* should calculate the band dispersion.
The notation is the same as that in the conventional calculation.

**Band.kpath**

Specify k-paths along which *BandDispersion* should calculate the band dispersion.
The notation is the same as that in the conventional calculation.

**Calculation**

The k-space spin density matrix resolved to each atom is calculated by a post-processing code 'kSpin'
in the directory 'work'.
Please move to the directory 'work', and perform a calculation as follows:

```text

    % ./kSpin Au111Surface_BD.dat
```

or for the MPI calculation, for example, the case with 4 MPI processes

```text

    % mpirun -np 4 ./kSpin Au111Surface_BD.dat
```

As the calculation proceeds, you may see the following standard output:

```text

    ******************************************************************
    ******************************************************************
     kSpin:
     code for evaluating spin related properties
     in momentum space of solid state materials.
     Copyright (C), 2019,
     Hiroki Kotaka, Naoya Yamaguchi and Fumiyuki Ishii.
     This software includes the work that is distributed
     in version 3 of the GPL (GPLv3).
 
     Please cite the following article:
     H. Kotaka, F. Ishii, and M. Saito,
     Jpn. J. Appl. Phys. 52, 035204 (2013).
     DOI: 10.7567/JJAP.52.035204.
    ******************************************************************
    ******************************************************************

    Input filename is "Au111Surface.scfout"  

    Start "BandDispersion" Calculation (3).  
    line_Nk[1]:  0.665829
    ( 0.000000,  0.500000,  0.000000 ) -> ( 0.000000,  0.000000,  0.000000 )
    line_Nk[2]:  1.331658
    ( 0.000000,  0.000000,  0.000000 ) -> ( 0.000000, -0.500000,  0.000000 )
    ########### ORBITAL DATA ##################
    ClaOrb_MAX[0]:   2
    ClaOrb_MAX[1]:   8
    Total Band (2*n): 124
    ###########################################
    Band.Nkpath: 2
    135 ( 0.000000,  0.500000,  0.000000 ) >>> ( 0.000000,  0.000000,  0.000000 ) M G
    135 ( 0.000000,  0.000000,  0.000000 ) >>> ( 0.000000, -0.500000,  0.000000 ) G -M
    l_min:  49   l_max:  56   l_cal:   8 
    Au111Surface_BD.Band49_1
    Au111Surface_BD.Band50_1
    Au111Surface_BD.Band51_1
    Au111Surface_BD.Band52_1
    Au111Surface_BD.Band53_1
    Au111Surface_BD.Band54_1
    Au111Surface_BD.Band55_1
    Au111Surface_BD.Band56_1
    l_min:  49   l_max:  56   l_cal:   8 
    Au111Surface_BD.Band49_2
    Au111Surface_BD.Band50_2
    Au111Surface_BD.Band51_2
    Au111Surface_BD.Band52_2
    Au111Surface_BD.Band53_2
    Au111Surface_BD.Band54_2
    Au111Surface_BD.Band55_2
    Au111Surface_BD.Band56_2
    ###########################################
    Total MulP data:2176
    ############ CALC TIME ####################
      Total Calculation Time:  4.772406 (s)
    ###########################################
```

When the calculation is completed normally as shown above, you can find the following
output files in the directory 'work':

```text

    Au111Surface_BD.BAND
    Au111Surface_BD.Band49_1
    Au111Surface_BD.Band50_1
    Au111Surface_BD.Band51_1
    Au111Surface_BD.Band52_1
    Au111Surface_BD.Band53_1
    Au111Surface_BD.Band54_1
    Au111Surface_BD.Band55_1
    Au111Surface_BD.Band56_1
    Au111Surface_BD.Band49_2
    Au111Surface_BD.Band50_2
    Au111Surface_BD.Band51_2
    Au111Surface_BD.Band52_2
    Au111Surface_BD.Band53_2
    Au111Surface_BD.Band54_2
    Au111Surface_BD.Band55_2
    Au111Surface_BD.Band56_2
    Au111Surface_BD.AMulPBand
    Au111Surface_BD.AMulPBand_s
    Au111Surface_BD.AMulPBand_p
    Au111Surface_BD.AMulPBand_p1
    Au111Surface_BD.AMulPBand_p2
    Au111Surface_BD.AMulPBand_p3
    Au111Surface_BD.AMulPBand_d
    Au111Surface_BD.AMulPBand_d1
    Au111Surface_BD.AMulPBand_d2
    Au111Surface_BD.AMulPBand_d3
    Au111Surface_BD.AMulPBand_d4
    Au111Surface_BD.AMulPBand_d5
    Au111Surface_BD.plotexample
    Au111Surface_BD.atominfo
    temporal_12345.input
```

As an example, by executing the following command, you can obtain a figure of the band dispersion for
the Rashba spin splitting in the Au(111) surface as shown in Fig. [67](banddispersion-calculation-on-the-band-dispersion-relation.md#fig:Rashba-Fig4)(a).

```text

    % gnuplot Au111Surface_BD.plotexample
```

In order to obtain information of spin textures on the band dispersion, you may try to analyze by
[53.6](mulpcalc-k-space-spin-density-matrix-resolved-to-each-atom.md#sec:MulPCalc) *MulPCalc*.

<a id="fig:Rashba-Fig4"></a>
<a id="4183"></a>
| ![\includegraphics[width=16.0cm]{Rashba-Fig4.eps}](assets/img433.png) |
| --- |

**Output files**

The content of each output file is explained below:

**BAND file**

This file stores data for the band dispersion. The first and second columns correspond to the
distance for the k-points along each k-path (in units of Bohr$^{-1}$) and
the energy for each of them (in units of eV), respectively.

**Band_YY_Z file**

This file stores data for the band dispersion of each branch with the band index YY and k-path index Z.
The notation of contents of this file is the same as the BAND file.

**AMulPBand file**

This file stores data of the k-space spin density matrix resolved to each atom,
and can be analyzed by [53.6](mulpcalc-k-space-spin-density-matrix-resolved-to-each-atom.md#sec:MulPCalc) *MulPCalc*.

**AMulPBand_xx file**

This file stores data of the xx-component of the k-space spin density matrix resolved to each atom,
and can be analyzed by [53.6](mulpcalc-k-space-spin-density-matrix-resolved-to-each-atom.md#sec:MulPCalc) *MulPCalc*.

**plotexample file**

This file supplies an example of gnuplot scripts.

**atominfo file**

This file supplies information of lattice vectors and PAOs.

**temporal_12345.input**

This file is a copy of the input file stored in the scfout file.

**Analysis of the k-space spin density matrix resolved to each atom**

*MulPCalc* can extract data to analyze the k-space spin density matrix resolved to each atom
from AMulPBand files or AMulPBand_xx files.
The executable file can be obtained by compilation in the directory 'source'
as follows:

```text

    % make MulPCalc
```

After the successful compilation, you can find the executable file 'MulPCalc' in the directory 'work'.
Let us analyze the k-space spin density matrix resolved to the atomic contribution on the band dispersion
for the Rashba spin splitting in the Au(111) surface. First, add the following keywords and values
into the input file 'Au111Surface_BD.dat', for example:

```text

    Filename.atomMulP Au111Surface_BD.AMulPBand # default: default
    Filename.xyzdata   Au111Surface_BD_MC       # default: default
    Num.of.Extract.Atom        3                # default: 1
    Extract.Atom               1 2 3            # default: 1 2 ... (Num.of.Extract.Atom)
```

After the above calculation, you can analyze the k-space spin density matrix resolved to the atomic contribution
as follows:

```text

    % ./MulPCalc Au111Surface_BD.dat
```

In addtion, you can adjust data for making better figures by the following keywords and values:

```text

    MulP.Vec.Scale       0.1  0.1  0.1          # default: 1.0  1.0  1.0
    Data.Reduction             1                # default: 1
```

After executing *MulPCalc*, you can find the following output files in the directory 'work'.

```text

    Au111Surface_BD_MC.MulPop
    Au111Surface_BD_MC.MulPop49
    Au111Surface_BD_MC.MulPop50
    Au111Surface_BD_MC.MulPop51
    Au111Surface_BD_MC.MulPop52
    Au111Surface_BD_MC.MulPop53
    Au111Surface_BD_MC.MulPop54
    Au111Surface_BD_MC.MulPop55
    Au111Surface_BD_MC.MulPop56
    Au111Surface_BD_MC.plotexample
```

As an example, by executing the following command, you can obtain a figure of the band dispersion
for the Rashba spin splitting in the Au(111) surface with the k-space spin density matrix resolved to the atom contribution
as shown in Fig. [67](banddispersion-calculation-on-the-band-dispersion-relation.md#fig:Rashba-Fig4)(b).

```text

    % gnuplot Au111Surface_BD_MC.plotexample
```

For more information of *MulPCalc*, see also the subsection of [53.6](mulpcalc-k-space-spin-density-matrix-resolved-to-each-atom.md#sec:MulPCalc) *MulPCalc*.
