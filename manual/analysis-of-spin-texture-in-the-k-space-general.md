<a id="SECTION000541000000000000000"></a>
## General

In this subsection, the calculation of spin textures is illustrated with a simple
model of an Au(111) surface. The spin texture/k-space spin density matrix are analyzed
by the following two or three steps:

**1. SCF calculation**

<a id="3850"></a>
<a id="3851"></a>
First, please perform a conventional SCF calculation using an input file 'Au111Surface_FL.dat'
stored in the directory 'work'. Then, the following keywords 'scf.SpinPolarization' and 'HS.fileout'
should be switched to 'NC' and 'ON', respectively, as follows:

```text

    scf.SpinPolarization         NC    # On|Off|NC
    HS.fileout                   ON    # on|off, default=Off
```

Also, when you consider to investigate spin texture,
the keyword 'scf.SpinOrbit.Coupling' should be switched on:

```text

    scf.SpinOrbit.Coupling       ON    # On|Off
```

Once the calculation is completed normally, you can obtain an output file 'Au111Surface.scfout'
in the directory 'work'. Figure [64](analysis-of-spin-texture-in-the-k-space-general.md#fig:Rashba-Fig1) shows the band structure of the Au(111) surface.

<a id="fig:Rashba-Fig1"></a>
<a id="6377"></a>
| ![\includegraphics[width=12.0cm]{Rashba-Fig1.eps}](assets/img417.png) |
| --- |

**2. Calculation of the spin texture and k-space spin density matrix**

Let us analyze Rashba bands with a spin splitting shown in Fig. [64](analysis-of-spin-texture-in-the-k-space-general.md#fig:Rashba-Fig1).
The spin texture and k-space spin density matrix are calculated by a post-processing code 'kSpin'.
The executable file can be obtained by compilation in the directory 'source' as follows:

```text

    % make kSpin
```

After the successful compilation, you can find the executable file 'kSpin' in the directory 'work'.
Then, please move to the directory 'work', and perform as follows:

```text

    % ./kSpin Au111Surface_FL.dat
```

Note that the input file must include appropriate keywords about 'kSpin', which will be explained later on.
'kSpin' has four ways to calculate the k-space spin density matrix: *FermiLoop*, *GridCalc*,
*BandDispersion*, and *MulPOnly*.
The details of the four ways are provided in each subsection.
The example 'Au111Surface_FL.dat' is for *FermiLoop* so that you can proceed with this exercise by moving to
the subsection of [53.2](fermiloop-calculation-on-a-constant-energy-level.md#sec:FermiLoop) *FermiLoop*.

**3. (Optional) Analysis of the k-space spin density matrix**

You may need to analyze the k-space spin density matrix, or atomic decomposition of it.
Moreover, it can be decomposed into the $s$-, $p$-, $d$-, or $f$-character components.
You can use a post-processing code 'MulPCalc' to analyze the k-space spin density matrix resolved
atom and pseudo-atomic orbital. How to do that will be explained
in the subsection of [53.6](mulpcalc-k-space-spin-density-matrix-resolved-to-each-atom.md#sec:MulPCalc) *MulPCalc*.
