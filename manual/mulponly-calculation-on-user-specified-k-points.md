<a id="SECTION000545000000000000000"></a>
<a id="sec:MulPOnly"></a>
## MulPOnly: Calculation on user-specified k-points

'kSpin' has four ways to calculate the k-space spin density matrix, which can be specified
by a keyword 'Calc.Type'. Here we introduce *MulPOnly* among the four ways.
*MulPOnly* can calculate the k-space spin density matrix on user-specified k-points for user-specified bands.
The calculation of spin texture using *MulPOnly* and *MulPCalc* is illustrated here with a simple
model of an Au(111) surface.

After a calculation of OpenMX with an input file 'Au111Surface_MO.dat' stored
in the directory 'work', you may try to run 'kSpin'.
The keywords relevant to the executation of kSpin can be found at the bottom of the input file
'Au111Surface_MO.dat' stored in the directory 'work' as shown below:

<a id="4241"></a>
<a id="4242"></a>
<a id="4243"></a>
<a id="4244"></a>
**List of keywords relevant to kSpin**

```text

    Filename.scfout       Au111Surface.scfout 
    Filename.outdata      Au111Surface_MO     
    Calc.Type             MulPOnly               # FermiLoop, GridCalc,
                                                   BandDispersion, or MulPOnly 
                                                   default: MulPOnly
    Filename.kpointdata   kpoint.in
```

In addition, another input file, whose file name is specified by the keyword 'Filename.kpointdata', is required to
specify k-points on which the k-space spin density matrix is calculated by *MulPOnly*.
For the exercise, the file 'kpoint.in' is stored in the directory 'work'.
The notation follows the following rule: In the first row, you need to specify the number of k-points
where *MulPOnly* will calculate the k-space spin density matrix.
Then, specify a k-point (the first, second, and third columns correspond to $k_x$, $k_y$, and $k_z$, respectively, in Bohr^-1.)
and a band index (the fourth column) for it.
The file 'kpoint.in' stores information of the k-points on the circle around the $\Gamma $-point in the reciprocal space.
For example, you can prepare this file as follows:

```text

  rm -f kpoint.in && awk '{for (i=0; i<$1; i++){printf "%17.14f %17.14f %17.14f %d\n", 0, $2*cos(2*atan2(0, -1)/$1*i), 
  $2*sin(2*atan2(0, -1)/$1*i), $3 >> "buffer"}; sum+=$1; if (!$1) {print sum; exit}}' - > N.in && cat N.in buffer >> kpoint.in && rm N.in buffer
```

After that, if you give values as follows:

```text

 40 0.18 55   <- # of k-points; radius; state (band index) (outer circle in k-space)
 40 0.15 56   <- # of k-points; radius; state (band index) (inner circle in k-space)
 0            <- exit
```

Then, you will get 'kpoint.in' and you can see the content of 'kpoint.in' as follows:

```text

  % cat kpoint.in
  80
  0.00000000000000 0.18000000000000 0.00000000000000 55
  0.00000000000000 0.17778390130712 0.02815820370724 55
  0.00000000000000 0.17119017293313 0.05562305898749 55
  0.00000000000000 0.16038117435391 0.08171828995312 55
  0.00000000000000 0.14562305898749 0.10580134541265 55
  0.00000000000000 0.12727922061358 0.12727922061358 55
  0.00000000000000 0.10580134541265 0.14562305898749 55
  0.00000000000000 0.08171828995312 0.16038117435391 55
  0.00000000000000 0.05562305898749 0.17119017293313 55
  0.00000000000000 0.02815820370724 0.17778390130712 55
  0.00000000000000 0.00000000000000 0.18000000000000 55
  0.00000000000000 -0.02815820370724 0.17778390130712 55
  ...
  ..
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
The default setting is *MulPOnly*. Here we choose *MulPOnly* for the exercise.

**Filename.kpointdata**

Specify the name of an data file of k-points and band indices.

**Calculation**

The k-space spin density matrix resolved to each atom is calculated by a post-processing code 'kSpin'
in the directory 'work'. Please move to the directory 'work', and perform a calculation as follows:

```text

    % ./kSpin Au111Surface_MO.dat
```

or for the MPI calculation, for example, the case with 4 MPI processes

```text

    % mpirun -np 4 ./kSpin Au111Surface_MO.dat
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

    Start "MulPOnly" Calculation (6).  

    ########### ORBITAL DATA ##################
    ClaOrb_MAX[0]:   2
    ClaOrb_MAX[1]:   8
    Total Band (2*n): 124
    ###########################################

    ############ CALC TIME ####################
      Total Calculation Time:  0.642631 (s)
    ###########################################
    ############ CALC TIME ####################
      Total Calculation Time:  0.660566 (s)
    ###########################################
```

When the calculation is completed normally as shown above, you can find the following
output files in the directory 'work':

```text

    Au111Surface_MO.AtomMulP
    Au111Surface_MO.MulP_s
    Au111Surface_MO.MulP_p
    Au111Surface_MO.MulP_p1
    Au111Surface_MO.MulP_p2
    Au111Surface_MO.MulP_p3
    Au111Surface_MO.MulP_d
    Au111Surface_MO.MulP_d1
    Au111Surface_MO.MulP_d2
    Au111Surface_MO.MulP_d3
    Au111Surface_MO.MulP_d4
    Au111Surface_MO.MulP_d5
    Au111Surface_MO.atominfo
    temporal_12345.input
```

**Output files**

The content of each output file is explained below:

**AtomMulP file**

This file stores data of the k-space spin density matrix resolved to each atom,
and can be analyzed by [53.6](mulpcalc-k-space-spin-density-matrix-resolved-to-each-atom.md#sec:MulPCalc) *MulPCalc*.

**MulP_xx file**

This file stores data of the xx-component of the k-space spin density matrix resolved to each atom,
and can be analyzed by [53.6](mulpcalc-k-space-spin-density-matrix-resolved-to-each-atom.md#sec:MulPCalc) *MulPCalc*.

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
Let us analyze spin textures for the Rashba spin splitting in the Au(111) surface. First, add the following
keywords and values into the input file 'Au111Surface_MO.dat', for example:

```text

    Filename.atomMulP Au111Surface_MO.AMulPBand   # default: default
    Filename.xyzdata   Au111Surface_MO_MC         # default: default
    Num.of.Extract.Atom        3                  # default: 1
    Extract.Atom               1 2 3              # default: 1 2 ... (Num.of.Extract.Atom)
    Calc.Type.3mesh            2                  # default: 1
```

And, after the above calculation, you can analyze spin textures as follows:

```text

    % ./MulPCalc Au111Surface_MO.dat
```

In addtion, you can adjust data for making better figures by the following keywords and values:

```text

    MulP.Vec.Scale       0.1  0.1  0.1          # default: 1.0  1.0  1.0
    Data.Reduction             1                # default: 1
```

After executing *MulPCalc*, you can find the following output files in the directory 'work'.

```text

    Au111Surface_MO_MC.MulPop
    Au111Surface_MO_MC.MulPop55
    Au111Surface_MO_MC.MulPop56
    Au111Surface_MO_MC.plotexample
```

As an example, by executing the following command, you can obtain a figure of spin textures for the Rashba
spin splitting in the Au(111) surface as shown in Fig. [68](mulponly-calculation-on-user-specified-k-points.md#fig:Rashba-Fig-MulPOnly).

```text

    % gnuplot Au111Surface_MO_MC.plotexample
```

For more information of *MulPCalc*, see also the subsection of [53.6](mulpcalc-k-space-spin-density-matrix-resolved-to-each-atom.md#sec:MulPCalc) *MulPCalc*.

<a id="fig:Rashba-Fig-MulPOnly"></a>
<a id="4319"></a>
| ![\includegraphics[width=10.0cm]{Rashba-Fig-MulPOnly.eps}](assets/img434.png) |
| --- |
