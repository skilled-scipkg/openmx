<a id="SECTION000603000000000000000"></a>
## Relevant keywords

The specification of each keyword relevant to calculations of conductivity tensor and dielectric function is given below.

<a id="5255"></a>
**CDDF.start**

Switch on the calculations of conductivity tensor and dielectric function when you want to perform them.
The default is 'off'. In case of 'off', the calculation of conductivity tensor and dielectric function is turned off.

```text

      CDDF.start   on         # on|off, default=off
```

<a id="5259"></a>
**CDDF.FWHM**

Setting the full width at half maximum of conductivity and dielectric function. The default is '0.2' in eV.
The Lorentian function is smeared out with the parameter.

```text

      CDDF.FWHM    0.2        # default = 0.2 (eV)
```

<a id="5263"></a>
**CDDF.maximum_energy**

Setting the maximum energy of optical spectra for calculations of conductivity and dielectric function.
The default is '10.0' in eV. The energy range begins from 0.0 eV.

```text

      CDDF.maximum_energy    10.0    # default = 10.0 (eV)
```

<a id="5267"></a>
**CDDF.additional_maximum_energy**

Setting the additional energy range in the frequency domain.
Although the energy range for the output of conductivity and dielectric function is specified by 'CDDF.maximum_energy',
for the calculations the states beyond the energy range of the output are also taken into account,
since the states beyond the energy range of the output may contribute because of the broadening of Lorentzian function.
The energy range for the calculations can be controlled by a keyword 'CDDF.additional_maximum_energy'.
For example, when the maximum energy is 10 eV, which is specified by 'CDDF.maximum_energy', and the additional
energy range is set to 1.0 eV by 'CDDF.additional_maximum_energy', then the total energy range becomes 11.0 (10.0+1.0) eV.
The default value is 0.0 eV.

```text

      CDDF.additional_maximum_energy        1.0    # default = 0.0 eV
```

<a id="5271"></a>
**CDDF.frequency.grid.total_number**

Setting the total number of grids for conductivity and dielectric function.
The default number of grids is '10000'. And, the interval in the energy grid is given by
( Maximum energy - 0.0 ) / total number of energy-grid, e.g.
$( 10.0 - 0.0 ) / 10000 = 0.0010 $ (eV).

```text

      CDDF.frequency.grid.total_number    10000    # default = 10000
```

<a id="5275"></a>
**CDDF.Kgrid**

Setting a set of numbers (n1,n2,n3) of grids to discretize the first Brillouin zone in the k-space, which
is used for the calculations of conductivity and dielectric function.
For the reciprocal vectors
${\bf\tilde{a}}$,
${\bf\tilde{b}}$, and
${\bf\tilde{c}}$ in the k-space, please provide
a set of numbers (n1,n2,n3) of grids as 'n1 n2 n3'.
According to the (n1,n2,n3), a regular mesh in the first Brillouin zone will be generated.
It does not need to be the same as scf.Kgrid which is used for the SCF calculation. So, one may use a rather coarse grid
for the SCF calculation, and change to a finer grid for the calculations of conductivity and dielectric function
to reduce the computational cost.

<a id="5280"></a>
**CDDF.material_type**

Setting the type of material: metal or insulator. 0 is for insulator, and 1 is for insulator and metal.

```text

      CDDF.material_type 0    # Default=0
```
