<a id="SECTION000542000000000000000"></a>
<a id="sec:FermiLoop"></a>
## FermiLoop: Calculation on a constant-energy level

'kSpin' has four ways to calculate the k-space spin density matrix, which can be specified
by a keyword 'Calc.Type'. Here we introduce *FermiLoop* among the four ways.
*FermiLoop* can calculate the spin texture/k-space spin density matrix on a constant-energy
level (e.g. the Fermi level).
The calculation of spin texture using *FermiLoop* is illustrated here with a simple model of an Au(111) surface.
*FermiLoop* searches k-points by two steps: In the first step, *FermiLoop* performs a rough search
to find the bands to calculate; In the second step, *FermiLoop* detects k-points on the constant-energy level
using a triangular mesh.

After the calculation of 'Au111Surface_FL.dat' as explained above, you may try to run 'kSpin'.
The keywords relevant to the executation of kSpin can be found at the bottom of the input file
'Au111Surface_FL.dat' stored in the directory 'work' as shown below:

<a id="3895"></a>
<a id="3896"></a>
<a id="3897"></a>
<a id="3898"></a>
<a id="3899"></a>
<a id="3900"></a>
<a id="3901"></a>
<a id="3902"></a>
<a id="3903"></a>
<a id="3904"></a>
<a id="3905"></a>
<a id="3906"></a>
<a id="3907"></a>
<a id="3908"></a>
<a id="3909"></a>
**List of keywords relevant to kSpin**

```text

    Filename.scfout      Au111Surface.scfout 
    Filename.outdata     Au111Surface_FL     
    Calc.Type            FermiLoop         # FermiLoop, GridCalc,
                                             BandDispersion, or MulPOnly 
                                             default: MulPOnly
    Energy.Range         0.0  0.0          # eV; default: 0.0  0.0
    Search.kCentral      0.0  0.0  0.0     # default: 0.0  0.0  0.0
    Calc.Type.3mesh      2                 # default: 1
    kRange.3mesh         0.2  0.2          # default: 0.5  0.5
    k-plane.1stStep      21 21             # default: 2 2
    k-plane.2ndStep      3 3               # default: 3 3
    Eigen.Brent          On                # on|off, default: On
    Trial.Brent          5                 # default: 5
    Calc.Bandbyband      Off               # on|off, default: Off
    Calc.Band.Min        55
    Calc.Band.Max        56 
    MulP.Vec.Scale       0.1  0.1  0.1     # default: 1.0  1.0  1.0
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
The default setting is *MulPOnly*. Here we choose *FermiLoop* for the exercise.

**Energy.Range**

The keyword specifies the energy range in which bands to be analyzed are searched.
For *FermiLoop*, specify the two same values for an energy level.
The unit is 'eV'. If different values are set, the average of them will be used.
The default is '-0.5 0.5' (i.e. the Fermi level).

**Search.kCentral**

Specify a set of three values for the central k-point around which *FermiLoop* should
search k-points on the specified constant-energy level (i.e. values for the keyword 'Energy.Range').
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
of grid points as follows: 2 for $k_a$-axis, 3 for $k_b$-axis. If the values are '1 1' and the value for the keyword
'Calc.Bandbyband' is 'ON', *FermiLoop* will omit the first step, which is useful for a large-scale calculation
with many MPI processes (cf. k-plane.2ndStep; Calc.Bandbyband; Calc.BandMin; Calc.BandMax). The default is '2 2'.

**k-plane.2ndStep**

Specify the number of grid points for the second search, which divides each domain necessary for calculations picked out in the first search into smaller domains by using a triangular mesh. The notation is the same as that for the keyword 'k-plane.1stStep' (cf. k-plane.1stStep). The default is '3 3'.

**Eigen.Brent**

Specify if *FermiLoop* should use the Brent method (ON) or not (OFF) to search k-points on the specified
constant-energy level (i.e. values for the keyword 'Energy.Range'). If the value is 'OFF', *FermiLoop*
will use a linear interpolation scheme. The default is 'ON' (cf. Trial.Brent).

**Trial.Brent**

Specify the maximum number of steps for the Brent method (cf. Eigen.Brent). This keyword is valid
when the value for the keyword 'Eigen.Brent' is 'ON'. The default is '5' (cf. Eigen.Brent).

**Calc.Bandbyband**

Specify if *FermiLoop* should calculate given bands (ON) or not (OFF). (cf. Calc.BandMin; Calc.BandMax).
The default is 'OFF'.

**Calc.BandMin**

Set the lower limit on the range for bands to calculate by specifying the band index.
This keyword is valid when the value for the keyword 'Calc.Bandbyband' is 'ON' (cf. Calc.Bandbyband; Calc.BandMax).
You can see band indices using OMXTool [[146](bibliography.md#OMXTool)] or [53.4](banddispersion-calculation-on-the-band-dispersion-relation.md#sec:BandDispersion) *BandDispersion*.

**Calc.BandMax**

Set the upper limit on the range for bands to calculate by specifying the band index.
This keyword is valid when the value for the keyword 'Calc.Bandbyband' is 'ON' (cf. Calc.Bandbyband; Calc.BandMin).
You can see band indices using [[146](bibliography.md#OMXTool)] or [53.4](banddispersion-calculation-on-the-band-dispersion-relation.md#sec:BandDispersion) *BandDispersion*.

**MulP.Vec.Scale**

Specify a scale to draw vectors expressing the spin texture. For example, values '0.1 0.2 0.3' specifies the scale
as follows: 0.1 for x-axis, 0.2 for y-axis, 0.3 for z-axis.
This keyword affects only 'XXXXX.Pxyz_YY' (XXXXX = the value for the keyword 'Filename.outdata'; YY = the band index).
The default is '1.0 1.0 1.0'.

**Calculation**

The spin texture/k-space spin density matrix are calculated by a post-processing code 'kSpin' in the directory 'work'.
Then, please move to the directory 'work', and perform a calculation as follows:

```text

    % ./kSpin Au111Surface_FL.dat
```

or for the MPI calculation, for example, the case with 4 MPI processes

```text

    % mpirun -np 4 ./kSpin Au111Surface_FL.dat
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

    Start "FermiLoop" Calculation (5).

    ########### ORBITAL DATA ##################
    ClaOrb_MAX[0]:   2
    ClaOrb_MAX[1]:   8
    Total Band (2*n): 124
    Central (  0.000000   0.000000   0.000000)
    ###########################################

    ########### EIGEN VALUE ###################
    The number of BANDs    2 (  55->  56)
    ########### CONTOUR CALC ##################
      k-height :   0   0.000000
    The number of BANDs    2 (  55->  56)
     l=  55,   k_points: 139 (array: 277)
     l=  56,   k_points: 115 (array: 229)
    Total MulP data: 254
    ###########################################

    ###########################################

    ############ CALC TIME ####################
      Total Calculation Time: 26.851349 (s)
            Eigen Value Calc:  4.277838 (s)
     l=  55:    Contour Calc: 11.349228 (s)
                   MulP Calc:  1.120379 (s)
     l=  56:    Contour Calc:  9.179602 (s)
                   MulP Calc:  0.920524 (s)
    ###########################################
    ############ CALC TIME ####################
      Total Calculation Time: 26.869150 (s)
    ###########################################
```

When the calculation is completed normally as shown above, you can find the following
output files in the directory 'work':

```text

    Au111Surface_FL.FermiSurf_53
    Au111Surface_FL.Pxyz_53
    Au111Surface_FL.FermiSurf_54
    Au111Surface_FL.Pxyz_54
    Au111Surface_FL.FermiSurf_55
    Au111Surface_FL.Pxyz_55
    Au111Surface_FL.FermiSurf_56
    Au111Surface_FL.Pxyz_56
    Au111Surface_FL.AtomMulP
    Au111Surface_FL.MulP_s
    Au111Surface_FL.MulP_p
    Au111Surface_FL.MulP_p1
    Au111Surface_FL.MulP_p2
    Au111Surface_FL.MulP_p3
    Au111Surface_FL.MulP_d
    Au111Surface_FL.MulP_d1
    Au111Surface_FL.MulP_d2
    Au111Surface_FL.MulP_d3
    Au111Surface_FL.MulP_d4
    Au111Surface_FL.MulP_d5
    Au111Surface_FL.plotexample
    Au111Surface_FL.atominfo
    temporal_12345.input
```

As an example, by executing the following command, you can obtain a figure of spin texture
for the Rashba spin splitting in the Au(111) surface as shown in Fig. [65](fermiloop-calculation-on-a-constant-energy-level.md#fig:Rashba-Fig2).
which exhibits a typical Rashba-type spin texture.

```text

    % gnuplot Au111Surface_FL.plotexample
```

<a id="fig:Rashba-Fig2"></a>
<a id="3978"></a>
| ![\includegraphics[width=12.0cm]{Rashba-Fig2.eps}](assets/img425.png) |
| --- |

**Output files**

The content of each output file is explained below:

**FermiSurf_YY file**

This file stores data of the k-points for the band with the band index YY searched on the specified
constant-energy level. The first, second, and third columns correspond to the $k_x$, $k_y$, and $k_z$
components of the k-points in units of Bohr$^{-1}$, respectively.
The fourth, and fifth columns correspond to the band index, the energy (in units of eV), respectively.

**Pxyz_YY file**

This file stores data of the expectation value of the Pauli matricies vectors for each k-point stored
in the FermiSurf_YY file. The first, second, and third columns correspond to the $k_x$, $k_y$, and
$k_z$ components of the k-points in units of Bohr$^{-1}$, respectively.
The fourth, fifth, and sixth columns correspond to the expectation value of the $\sigma_x$, $\sigma_y$,
and $\sigma_z$ in units of the Bohr magneton, respectively.

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
at the bottom of an input file 'Au111Surface_FL.dat' and proceed to the analysis of the k-space
spin density matrix after the above calculation as follows:

```text

    % ./MulPCalc Au111Surface_FL.dat
```

For more information of *MulPCalc*, see also the subsection of [53.6](mulpcalc-k-space-spin-density-matrix-resolved-to-each-atom.md#sec:MulPCalc) *MulPCalc*.

**Other tips**

*GridCalc* may be useful in finding appropriate settings for FermiLoop because
*GridCalc* can draw spin the texture on a k-point grid to investigate a wider domain
in the reciprocal space.
Setting 'OFF' for the keyword 'Eigen.Brent' may be effective in reducing computational time.
In this case, you should use a fine mesh by increaing the values for the keywords 'k-plane.1stStep'
or 'k-plane.2ndStep' for accuracy.
