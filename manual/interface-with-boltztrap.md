<a id="SECTION000610000000000000000"></a>
# Interface with BoltzTraP

OpenMX is interfaced with BoltzTraP [[99](bibliography.md#BoltzTraP2006)] which calculates electron transport coefficients
based on the Boltzmann theory from the wave number dependence of the energy eigenvalues in the Kohn-Sham equation.
The interface [[100](bibliography.md#Miyata_BoltzTraP2017)] with BoltzTraP enables us to calculate physical properties
such as the Seebeck coefficient, electrical conductivity, electronic thermal conductivity, and the Hall coefficient.
The functionality is compatible with not only the collinear calculations, but also the non-collinear calculations.
When you publish a paper using the functionality, we would like to appreciate your citation
of Ref. [[100](bibliography.md#Miyata_BoltzTraP2017)]. The interface with BoltzTraP2 will be released in the next version.
The interface, which bridges between OpenMX and BoltzTraP, can be used by copying MX_TRAP.sh which is stored
in the directory 'source' to the directory 'work' and executing it.
As an example, let us introduce a calculation of non-doped Si bulk. One can perform the SCF calculation using
an input file 'Si_BoltzTraP.dat' which is available in the directory 'work' as follows:

```text

    % mpirun -np 28 ./openmx Si_BoltzTraP
```

After the SCF calculation finishes normally, you obtain the out file 'Si_BoltzTraP.out'.
Then, you need to copy MX_TRAP.sh which is stored in the directory 'source' to the directory 'work'.
After that, you can perform MX_TRAP.sh as follows:

```text

    % sh MX_TRAP.sh
```

Then, the name of the 'out' files in the directory is listed as may be shown below.

```text

    =========================Outputfile List==========================    
    Si_BoltzTraP.out
    ==================================================================

    Please enter the outputfile name ; Outputfile name =
```

Then, please enter the file name of the 'out' file after "Outputfile name =" and execute it by typing enter.
Here we take Si_BoltzTraP.out as an example, and you may enter as

```text

    Please enter the output file name: Outputfile name = Si_BoltzTraP.out
```

When you press the enter key, the following message will be displayed:

```text

    ..
    ....
    Nospin::kloop kx ky kz:1681/1686
    Nospin::kloop kx ky kz:1682/1686
    Nospin::kloop kx ky kz:1683/1686
    Nospin::kloop kx ky kz:1684/1686
    Nospin::kloop kx ky kz:1685/1686
    Nospin::kloop kx ky kz:1686/1686
    .energy file for BoltzTraP has been generated.

    .struct file for BoltzTraP has been generated.

    .intrans file for BoltzTraP has been generated.

    Conversion has been finished.

    Directory is Si_BoltzTraP
```

<a id="fig:BoltzTraP-Fig1"></a>
<a id="5535"></a>
| ![\includegraphics[width=16.0cm]{BoltzTraP-Fig1.eps}](assets/img600.png) |
| --- |

After the above message is displayed, a directory named 'Si_BoltzTraP' is created, and four files such as
'Si_BoltzTraP.energy','Si_BoltzTraP.intrans', and 'Si_BoltzTraP.struct' will be stored in the directory
as shown below:

```text

  % cd Si_BoltzTraP
  % ls 
  Si_BoltzTraP.out Si_BoltzTraP.energy Si_BoltzTraP.struct Si_BoltzTraP.intrans
```

The '.out' file is a copy of the out file which was analyzed by the conversion.
The '.energy' file is a file of energy eigenvalues.
If the keyword 'scf.SpinPolarization' in the '.out' file is 'ON',
then the '.energyup' and ".energydn" files are output, while '.energyso' file is output if the keyword
'scf. SpinPolarization' in the '.out' file is 'NC'.
The '.struct' file is a file of unit lattice vectors. The unit is converted automatically
into atomic units. The '.intrans' file describes input parameters necessary for electronic
transport calculation. For details, please refer to the pdf manual enclosed with BoltzTraP package.
The numerical value of the first item in the third line is the chemical potential $\mu$
calculated by OpenMX (unit is Ryd). The value of 10 in the fifth line is the Fourier interpolation
factor of the band,
which is set to 10 by default. The numerical value in the eighth row is the electron temperature of
the Fermi distribution. The first item is the maximum temperature. The second item is the temperature
step size when calculating the temperature dependence.
If the temperature dependence is not to be calculated, then enter the same value as the first item.
By default, the temperature specified by 'scf.ElectronicTemperature' in the '.out' file is entered.
If 'scf.ElectronicTemperature' is not specified, $T = 300 K$ will be assigned.

<a id="fig:BoltzTraP-Fig2"></a>
<a id="6491"></a>
| ![\includegraphics[width=17.0cm]{BoltzTraP-Fig2.eps}](assets/img603.png) |
| --- |

Next, please move to the directory 'Si_BoltzTraP' and type BoltzTraP as shown below.
The procedure from this point is the same as the normal BoltzTraP calculation.
Therefore, please refer to the PDF manual enclosed in the BoltzTraP package for details.

```text

    % cd Si_BoltzTraP
    % 'path to BoltzTrap'/boltztrap-1.2.5/sr/x_trans BoltzTraP
```

If the stored energy eigenvalue file is '.energyup', '.energydn' or '.energyso',
please add '-up', '-dn', or '-so' as an option after x_trans BoltzTraP, and execute it.
Then, electron transport calculations are performed for the energy eigenvalue file specified by the option.
When the calculation is completed normally, the following message will be displayed:

```text

    ========================== BoltzTraP vs 1.2.5 =============
    99.786 u 0.076 s 1: 40.04 99.8\% 0 + 0 k 0 + 1612 0 io 0 pf + 0 w
```

The average values of the electron transport properties over the $x$-, $y$-, and $z$-axes are stored
in 'Si_BoltzTraP.trace.', while the electron transport properties of the $x$-, $y$-, and $z$-axes are
stored in 'Si_BoltzTraP.condtens'.
Figure [85](interface-with-boltztrap.md#fig:BoltzTraP-Fig1) summarizes the computational protocol of the electron transport calculation
by OpenMX and BoltzTraP. In Fig. [86](interface-with-boltztrap.md#fig:BoltzTraP-Fig2) we show the Seebeck coefficient $S$ and chemicafnl
potential $\mu$ dependence of electrical conductivity
$\sigma \tau _{\rm el}^{-1}$ of non-doped Si bulk.
The input file 'Si_BoltzTraP.dat' used for the calculation is available in the directory 'work'.

Extensitve benchmark calculations using the functionality are found in the supplementary material:
'11664_2017_6020_MOESM1_ESM.pdf' of Ref. [[100](bibliography.md#Miyata_BoltzTraP2017)].
Among the benchmark calculations we show in Fig. [87](interface-with-boltztrap.md#fig:BoltzTraP-Fig3) a computational result
for GaCuS$_2$ bulk in which the non-collinear calculation with spin-orbit coupling was performed.
The input file 'GaCuS2_mp-5238_symmetrized_SOC.dat' used
for the calculation is available in the directory 'work'.

<a id="fig:BoltzTraP-Fig3"></a>
<a id="6492"></a>
| ![\includegraphics[width=16.5cm]{BoltzTraP-Fig3.eps}](assets/img604.png) |
| --- |
