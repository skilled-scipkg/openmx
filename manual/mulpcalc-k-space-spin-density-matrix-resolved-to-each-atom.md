<a id="SECTION000546000000000000000"></a>
<a id="sec:MulPCalc"></a>
## MulPCalc: k-space spin density matrix resolved to each atom

*MulPCalc* can extract data to analyze the Mulliken population from AtomMulP files, MulP_xx files,
AMulPBand files or AMulPBand_xx files obtained by kSpin.
The executable file can be obtained by compilation in the directory 'source'
as follows:

```text

    % make MulPCalc
```

After the successful compilation, you will find the executable file 'MulPCalc' in the directory 'work'.
Also, you find an example of an input file 'SiC_Primitive_BD.dat' in the directory 'work'.
After the SCF calculation, please perform a *BandDispersion* calculation by 'kSpin'
with the following settings:

```text

    Filename.scfout    sic_primitive.scfout # default: default
    Filename.outdata   sic_primitive_BD     # default: default
    Calc.Type          BandDispersion       # default: MulPOnly
    Energy.Range       -10.0  6.0           # eV; default: 0.0  0.0
```

Next, please execute *MulPCalc* as

```text

    % ./MulPCalc SiC_Primitive_BD.dat
```

with the following settings to extract data of $p_z$ orbitals on a carbon atom:

```text

    Filename.atomMulP sic_primitive_BD.AMulPBand_p3 # default: default
    Filename.xyzdata   sic_primitive_BD_MC_C_p3     # default: default
    Num.of.Extract.Atom        1                 # default: 1
    Extract.Atom               1                 # default: 1 2 ... (Num.of.Extract.Atom)
```

In addtion, you can adjust data for making better figures by the following keywords and values:

```text

    MulP.Vec.Scale       0.1  0.1  0.1           # default: 1.0  1.0  1.0
    Data.Reduction             2                 # default: 1
```

Figure [69](mulpcalc-k-space-spin-density-matrix-resolved-to-each-atom.md#fig:Rashba-Fig5) can be obtained by executing *MulPCalc* several times similarly
and plotting extracted data of the eleventh, four, and fifth columns stored in MulPop files
by using the circles style of gnuplot.

<a id="fig:Rashba-Fig5"></a>
<a id="6414"></a>
| ![\includegraphics[width=12.0cm]{Rashba-Fig5.eps}](assets/img435.png) |
| --- |

In addition, in the directory 'work', there is another example of an input file 'Au111Surface23_FL.dat' for
a slab model with two clean Au(111) surfaces, which may take much more time than the other examples.
You can try it similarly. After the SCF calculation and subsequent *FermiLoop* calculation,
you may find the band dispersion and spin textures as shown in Figs. [70](fig:Rashba-Fig6)(a) and [70](ig:Rashba-Fig6)(b),
respectively,
where there are two pairs of Rashba bands, which are degenerated because one surface is equivalent to the other.
In this case, you may need to obtain the contribution of atoms in one surface by *MulPCalc*.
By using *MulPCalc*, you can get it and find spin texture in one surface as shown in Fig. [70](fig:Rashba-Fig6)(c).

<a id="fig:Rashba-Fig6"></a>
<a id="6406"></a>
| ![\includegraphics[width=11.0cm]{Rashba-Fig6.eps}](assets/img436.png) |
| --- |

The specification of each keyword is explained below:

**List of keywords (common) relevant to MulPCalc**

**Filename.atomMulP**

Specify the name of an AtomMulP file, a MulP_xx file, an AMulPBand file or an AMulPBand_xx file.

**Filename.xyzdata**

Specify a name for output files. This keyword corresponds to the keyword 'System.Name'.

**Num.of.Extract.Atom**

Specify the number of atoms for which MulPCalc should extract data of the Mulliken population. The default is '1'.

**Extract.Atom**

Specify atoms for which MulPCalc should extract data of the Mulliken population.
The default is '1 2 ... (the value for the keyword 'Num.of.Extract.Atom')'.

**Data.Reduction**

Specify the number of k-points every which MulPCalc should extract data of the Mulliken population.
This keyword is useful in thinning out k-points or reducing data size.

**MulP.Vec.Scale**

Specify a scale to draw vectors expressing spin textures. For example, values '0.1 0.2 0.3' specifies
the scale as follows: 0.1 for x-axis, 0.2 for y-axis, 0.3 for z-axis. The default is '1.0 1.0 1.0'.

**Filename.outdata**

Keep the specification in kSpin.

**Calc.Type**

Keep the specification in kSpin.

**List of keywords (Calc.Type = FermiLoop or GridCalc) relevant to MulPCalc**

**Search.kCentral**

Keep the specification in kSpin.

**Calc.Type.3mesh**

Keep the value in kSpin.

**Energy.Range**

Keep the value in kSpin.

**List of keywords (Calc.Type = BandDispersion) relevant to MulPCalc**

**Energy.Range**

Keep the value in kSpin.

**Band.Nkpath**

Keep the value in kSpin.

**Band.kpath**

Keep the value in kSpin.

**List of keywords (Calc.Type = MulPOnly) relevant to MulPCalc**

**Calc.Type.3mesh**

Specify a plane to calculate as follows: Set a value '1', '2', and , '3',
for the case of $k_ak_b$-, $k_bk_c$-, and $k_ck_a$- planes, respectively. The default is '1'.

**Output files**

After the calculation by 'MulPCal' is completed normally, you obtain the following output files in the working directory'.

**MulPop file**

This file stores data for each k-point. The first, second, and third columns correspond to the $k_x$, $k_y$, and $k_z$
components of the k-points in units of Å$^{-1}$, respectively.
The fourth column corresponds to the energy in units of eV; The fifth, sixth, and seventh columns correspond to
the number of electrons: Total, $\alpha $-spin, and $\beta $-spin, respectively.
The eighth, nineth, and tenth columns correspond to the expectation value of the $\sigma_x$, $\sigma_y$, and $\sigma_z$
in units of the Bohr magneton, respectively. If the value for the keyword 'Calc.Type' is 'BandDispersion',
the eleventh column corresponds to the distance for the k-points along each k-path in units of Bohr$^{-1}$.

**MulPop_YY file**

This file stores data for each k-point with the band index YY. The notation of contents of this file is the same as the MulPop file.

**plotexample file**

If the value for the keyword 'Calc.Type' is not 'GridCalc', this file supplies an example of gnuplot scripts.

**plotexample_YY file**

If the value for the keyword 'Calc.Type' is 'GridCalc',
this file supplies an example of gnuplot scripts for the band with the band index YY.
