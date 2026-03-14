<a id="SECTION000521000000000000000"></a>
## DFT-D2 method

The following keywords are relevant to the DFT-D2 method.

```text

  scf.dftD                     on           # on|off, default=off
  DFTD.Unit                   Ang           # Ang|AU
  DFTD.rcut_dftD             100.0          # default=100 (DFTD.Unit)
  DFTD.d                      20.0          # default=20
  DFTD.scale6                 0.75          # default=0.75
  DFTD.IntDirection          1 1 1          # default=1 1 1 (1:on 0:off)
```

When you include the vdW correction, switch on 'scf.dftD'.
The cutoff radius for the pairwise interaction is given by 'DFTD.rcut_dftD',
where the unit is given by 'DFTD.Unit'.
The 'd' value in Eq. (12) in Grimme's paper [[135](bibliography.md#Grimme06)] is given by 'DFTD.d',
while the default value is 20. The scaling factor in Eq. (11) in
Grimme's papar [[135](bibliography.md#Grimme06)] is given by 'DFTD.scale6', while the default value
for the PBE functional is 0.75. Also, the interaction can be cut along the **a**-, **b**-,
and **c**-axes by 'DFTD.IntDirection', where 1 means that the interaction is included,
and 0 not.
Also, the periodicity for each atom can be controlled by

```text

  <DFTD.periodicity 
  1   1
  2   1
  3   1
  4   1
  ....
  DFTD.periodicity>
```

where the first column is a serial number which is the same as in the
'Atoms.SpeciesAndCoordinates', and the second column is a flag which means
that 1 is periodic, and 0 is non-periodic for the corresponding atom.
By considering the periodicity or non-periodicity of each atom, the interaction
is automatically cut when they are non-periodic.

The main modifications are placed at only two routines:
DFTDvdW_init.c and Calc_EdftD() of Total_Energy.c.
In DFTDvdW_init.c, you can easily change the parameters for the vdW correction,
and in Calc_EdftD() of Total_Energy.c you can confirm how they are calculated.

Since OpenMX uses localized orbitals as basis function, it is very important to
take account of basis set superposition error (BSSE) when we investigate an effect
of a weak interaction such as vdW interaction. To estimate BSSE, the counterpoise
(CP) method [[46](bibliography.md#Boys70),[47](bibliography.md#Simon96)] can be used.
As for the CP method, see the Section 'Empty atom scheme'.
