<a id="SECTION000543000000000000000"></a>
<a id="sec:GridCalc"></a>
## GridCalc: Calculation on a k-point grid

'kSpin' has four ways to calculate the k-space spin density matrix, which can be specified
by a keyword 'Calc.Type'. Here we introduce *GridCalc* among the four ways.
*GridCalc* can calculate the spin textures/k-space spin density matrix on a given
k-point grid for each band within a user-specified energy range.
You can also specify bands to calculate instead of specifying an energy range.
The calculation of spin textures using *GridCalc* is illustrated here with a simple
model of an Au(111) surface.

After a calculation of OpenMX with an input file 'Au111Surface_GC.dat' stored
in the directory 'work', you may try to run 'kSpin'.
The keywords relevant to the executation of kSpin can be found at the bottom of the input file
'Au111Surface_GC.dat' stored in the directory 'work' as shown below:

<a id="4022"></a>
<a id="4023"></a>
<a id="4024"></a>
<a id="4025"></a>
<a id="4026"></a>
<a id="4027"></a>
<a id="4028"></a>
<a id="4029"></a>
<a id="4030"></a>
<a id="4031"></a>
<a id="4032"></a>
<a id="4033"></a>
**List of keywords relevant to kSpin**

```text

    Filename.scfout      Au111Surface.scfout 
    Filename.outdata     Au111Surface_GL     
    Calc.Type            GridCalc          # FermiLoop, GridCalc,
                                             BandDispersion, or MulPOnly 
                                             default: MulPOnly
    Energy.Range        -1.0  1.0          # eV; default: 0.0  0.0
    Search.kCentral      0.0  0.0  0.0     # default: 0.0  0.0  0.0
    Calc.Type.3mesh      2                 # default: 1
    kRange.3mesh         0.5  0.5          # default: 0.5  0.5
    k-plane.1stStep      14 14             # default: 2 2
    Calc.Bandbyband      Off               # default: Off
    Calc.Band.Min        55
    Calc.Band.Max        56
    MulP.Vec.Scale       0.1  0.1  0.1     # default: 1.0  1.0  1.0
```

**Specification of keywords**

Although the keywords above are the same as for the case of *FermiLoop*,
for user's convenience the specification of each keyword is explained with emphasis on *GridCalc* below.
Note that the behavier of the keyword 'Enery.Range' is different from that in *FermiLoop*.

**Filename.scfout**

Specify the name of the scfout file which will be read by 'kSpin'.

**Filename.outdata**

Specify a name for output files. This keyword corresponds to the keyword 'System.Name'
for OpenMX calculations.

**Calc.Type**

Choose either *FermiLoop*, *GridCalc*, *BandDispersion*, or *MulPOnly*.
The default setting is *MulPOnly*. Here we choose *GridCalc* for the exercise.

**Energy.Range**

Specify the two different values for an energy range for which GridCalc should search bands.
The unit is in eV. This keyword should be valid when the keyword 'Calc.Bandbyband' is 'OFF'
(cf. Calc.Bandbyband). The default is '-0.5 0.5' (i.e. the range is [-0.5, 0.5]).

**Search.kCentral**

Specify a set of three values for the central k-point around which *GridCalc* should
search k-points on the specified energy range (i.e. values for the keyword 'Energy.Range').
The notation to specify the k-point follows the keyword 'Band.kpath'.
The default is '0.0 0.0 0.0' (i.e. $\Gamma $-point).

**Calc.Type.3mesh**

Specify a plane on which the spin texture is calculated.
Set a value '1', '2', and '3',
for the case of $k_ak_b$-, $k_bk_c$-, and $k_ck_a$-planes, respectively. The default is '1'.

**kRange.3mesh**

Specify two values for a two-dimensional domain in the reciprocal space where k-points
should be calculated.
For example, if the value for the keyword 'Calc.Type.3mesh' is '1' ($k_ak_b$-plane),
values '0.2 0.3' specifies a domain:
$-0.2\leq k_a\leq 0.2$,
$-0.3 \leq k_b \leq 0.3$.
The notation of the k-points follows the keyword 'Band.kpath'.
The default is '0.5 0.5' (i.e. the whole of the first brillouin zone).

**k-plane.1stStep**

Specify the number of grid points to divide the domain by the keyword 'kRange.3mesh' for the first search.
For example, if the value for the keyword 'Calc.Type.3mesh' is '1' ($k_ak_b$-plane), values '2 3' specifies the number
of grid points as follows: 2 for $k_a$-axis, 3 for $k_b$-axis. The default is '2 2'.

**Calc.Bandbyband**

Specify if *GridCalc* should calculate given bands (ON) or not (OFF). (cf. Calc.BandMin; Calc.BandMax).
The default is 'OFF'.

**Calc.BandMin**

Set the lower limit on the range for bands to calculate by specifying the band index.
This keyword is valid when the value for the keyword 'Calc.Bandbyband' is 'ON' (cf. Calc.Bandbyband; Calc.BandMax).
You can see band indices using OMXTool [[146](bibliography.md#OMXTool)] or [53.4](banddispersion-calculation-on-the-band-dispersion-relation.md#sec:BandDispersion) BandDispersion.

**Calc.BandMax**

Set the upper limit on the range for bands to calculate by specifying the band index.
This keyword is valid when the value for the keyword 'Calc.Bandbyband' is 'ON' (cf. Calc.Bandbyband; Calc.BandMin).
You can see band indices using OMXTool [[146](bibliography.md#OMXTool)] or [53.4](banddispersion-calculation-on-the-band-dispersion-relation.md#sec:BandDispersion) BandDispersion.

**MulP.Vec.Scale**

Specify a scale to draw vectors expressing the spin texture. For example, values '0.1 0.2 0.3' specifies the scale
as follows: 0.1 for x-axis, 0.2 for y-axis, 0.3 for z-axis.
This keyword affects only 'XXXXX.Pxyz_YY' (XXXXX = the value for the keyword 'Filename.outdata'; YY = the band index).
The default is '1.0 1.0 1.0'.

**Calculation**

The spin texture/k-space spin density matrix are calculated by a post-processing code 'kSpin' in the directory 'work'.
Then, please move to the directory 'work', and perform a calculation as follows:

```text

    % ./kSpin Au111Surface_GC.dat
```

or for the MPI calculation, for example, the case with 4 MPI processes

```text

    % mpirun -np 4 ./kSpin Au111Surface_GC.dat
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

    Start "GridCalc" Calculation (4).

    ########### ORBITAL DATA ##################
    ClaOrb_MAX[0]:   2
    ClaOrb_MAX[1]:   8
    Total Band (2*n): 124
    Central (  0.000000   0.000000   0.000000)
    ###########################################

    ########### EIGEN VALUE ###################
    The number of BANDs    8 (  49->  56)
    Total MulP data:1568
    ###########################################

    ############ CALC TIME ####################
      Total Calculation Time:  3.656405 (s)
            Eigen Value Calc:  3.498849 (s)
    ###########################################
    ############ CALC TIME ####################
      Total Calculation Time:  3.670708 (s)
    ###########################################
```

When the calculation is completed normally as shown above, you can find the following
output files in the directory 'work':

```text

    Au111Surface_GC.EigenMap_49
    Au111Surface_GC.Pxyz_49
    Au111Surface_GC.plotexample_49
    Au111Surface_GC.EigenMap_50
    Au111Surface_GC.Pxyz_50
    Au111Surface_GC.plotexample_50
    Au111Surface_GC.EigenMap_51
    Au111Surface_GC.Pxyz_51
    Au111Surface_GC.plotexample_51
    Au111Surface_GC.EigenMap_52
    Au111Surface_GC.Pxyz_52
    Au111Surface_GC.plotexample_52
    Au111Surface_GC.EigenMap_53
    Au111Surface_GC.Pxyz_53
    Au111Surface_GC.plotexample_53
    Au111Surface_GC.EigenMap_54
    Au111Surface_GC.Pxyz_54
    Au111Surface_GC.plotexample_54
    Au111Surface_GC.EigenMap_55
    Au111Surface_GC.Pxyz_55
    Au111Surface_GC.plotexample_55
    Au111Surface_GC.EigenMap_56
    Au111Surface_GC.Pxyz_56
    Au111Surface_GC.plotexample_56
    Au111Surface_GC.AtomMulP
    Au111Surface_GC.MulP_s
    Au111Surface_GC.MulP_p
    Au111Surface_GC.MulP_p1
    Au111Surface_GC.MulP_p2
    Au111Surface_GC.MulP_p3
    Au111Surface_GC.MulP_d
    Au111Surface_GC.MulP_d1
    Au111Surface_GC.MulP_d2
    Au111Surface_GC.MulP_d3
    Au111Surface_GC.MulP_d4
    Au111Surface_GC.MulP_d5
    Au111Surface_GC.atominfo
    temporal_12345.input
```

As an example, by executing the following command, you can obtain figures of the spin texture for
the Rashba spin splitting in the Au(111) surface as shown in Figs. [66](gridcalc-calculation-on-a-k-point-grid.md#fig:Rashba-Fig3)(a) and (b).
which exhibit the typical Rashba-type spin texture.

```text

    % gnuplot Au111Surface_GC.plotexample_55
    % gnuplot Au111Surface_GC.plotexample_56
```

<a id="fig:Rashba-Fig3"></a>
<a id="4094"></a>
| ![\includegraphics[width=16.0cm]{Rashba-Fig3.eps}](assets/img432.png) |
| --- |

**Output files**

The content of each output file is explained below:

**EigenMap_YY file**

This file stores a grid data for the band with the band index YY.
The first, second, and third columns correspond to the $k_x$, $k_y$, and $k_z$ components of
the k-points in units of Bohr$^{-1}$, respectively.
The fourth column corresponds to the energy in units of eV.

**Pxyz_YY file**

This file stores data of the expectation value of the Pauli matrices vectors for
each k-point stored in the FermiSurf_YY file. The first, second, and third columns
correspond to the $k_x$, $k_y$, and $k_z$ component of the k-points in units of Bohr$^{-1}$,
respectively. The fourth, fifth, and sixth columns correspond to the expectation value of the $\sigma_x$,
$\sigma_y$, and $\sigma_z$ in units of the Bohr magneton, respectively.

**AtomMulP file**

This file stores data of the k-space spin density matrix resolved to the atomic contribution,
which can be analyzed by [53.6](mulpcalc-k-space-spin-density-matrix-resolved-to-each-atom.md#sec:MulPCalc) *MulPCalc*.

**MulP_xx file**

This file stores data of the xx-component of the k-space spin density matrix resolved to the atomic contribution,
and can be analyzed by [53.6](mulpcalc-k-space-spin-density-matrix-resolved-to-each-atom.md#sec:MulPCalc) *MulPCalc*.

**plotexample file**

This file supplies an example of gnuplot scripts.

**atominfo file**

This file supplies information of lattice vectors and PAOs.

**temporal_12345.input**

This file is a copy of the input file stored in the scfout file.

**(Optional) Analysis of the k-space spin density matrix**

*MulPCalc* can extract data to analyze the k-space spin density matrix
from AtomMulP files or MulP_xx files. You can find an example of input files for *MulPCalc*
at the bottom of an input file 'Au111Surface_GC.dat' and proceed to the analysis of the k-space
spin density matrix after the above calculation as follows:

```text

    % ./MulPCalc Au111Surface_GC.dat
```

For more information of *MulPCalc*, see also the subsection of [53.6](mulpcalc-k-space-spin-density-matrix-resolved-to-each-atom.md#sec:MulPCalc) *MulPCalc*.
