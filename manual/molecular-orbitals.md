<a id="SECTION000320000000000000000"></a>
# Molecular orbitals

Molecuar or crystal Kohn-Sham orbitals can be output in the Gaussian cube format,
and thereby visualized by many software such as VESTA [[103](bibliography.md#VESTA)] and
XCrySDen [[105](bibliography.md#XCrySDen)]. The relevant keywords are given by

```text

     MO.fileout         on    # on|off, default=off
     num.HOMOs           1    # default=2
     num.LUMOs           1    # default=2
     MO.Nkpoint          2    # default=1

     <MO.kpoint
       0.0  0.0  0.0
       0.5  0.0  0.0
     MO.kpoint>
```

When you want to generate the cube files, please swtich on the keyword 'MO.fileout'.
The numbers of the highest occupied molecular (crystal) orbitals (HOMOs) and the lowest occupied
molecular (crystal) orbitals (LUMOs) to be output can be specified by the keywords 'num.HOMOs'
and 'num.LUMOs', respectively. In case of a band calculation, the **k**-points at which
the HOMOs and LUMOs are calculated are specified
by the keywords: 'MO.Nkpoint' and 'MO.kpoint'.
The keyword 'MO.Nkpoint' gives the number of **k**-points at which
the HOMOs and LUMOs are calculated, and by the keyword 'MO.kpoint' you can specifiy
the **k**-points explicitly as shown above, where the specification is made based on
the reciprocal vectors for the unit cell vectors given by 'Atoms.UnitVectors'.
The output cube files are summarized as below:

**Cluster cases:**

<a id="1746"></a>
<a id="1747"></a>
If 'MO.fileout=ON' and
'scf.EigenvalueSolver=Cluster',
the following files are also generated:

- *System.Name*.homo0_0.cube, *System.Name*.homo0_1.cube, ...
  The HOMOs are output in the Gaussian cube format.
  The first number below 'homo' means a spin state
  (up=0, down=1). The second number specifies the eigenstates, i.e.,
  0, 1, and 2 correspond to HOMO, HOMO-1, and HOMO-2, respectively,
  whose number is specified by the keyword 'num.HOMOs'.
- *System.Name*.lumo0_0.cube, *System.Name*.lumo0_1.cube, ...
  The LUMOs are output in the Gaussian cube format.
  The first number below 'lumo' means a spin state
  (up=0, down=1). The second number specifies the eigenstates, i.e.,
  0, 1, and 2 correspond to LUMO, LUMO+1, and LUMO+2, respectively,
  whose number is specified by the keyword 'num.LUMOs'.

**Bulk cases:**

<a id="1756"></a>
<a id="1757"></a>
If 'MO.fileout=ON' and
'scf.EigenvalueSolver=Band',
the following files are also generated:

- *System.Name*.homo0_0_0_r.cube, *System.Name*.homo1_0_1_r.cube, ... *System.Name*.homo0_0_0_i.cube, *System.Name*.homo1_0_1_i.cube, ...
  The HOMOs are output in the Gaussian cube format.
  The first number below 'homo' means the k-point
  number, which is specified by the keyword 'MO.kpoint'.
  The second number is a spin state (up=0, down=1). The third number
  specifies the eigenstates, i.e., 0, 1, and 2 correspond to HOMO, HOMO-1,
  and HOMO-2, respectively,
  whose number is specified by the keyword 'num.HOMOs'.
  The 'r' and 'i' mean the real and imaginary parts of the wave function.
- *System.Name*.lumo0_0_0_r.cube, *System.Name*.lumo1_0_1_r.cube, ... *System.Name*.lumo0_0_0_i.cube, *System.Name*.lumo1_0_1_i.cube, ...
  The LUMOs are output in the Gaussian cube format.
  The first number below 'lumo' means the k-point
  number, which is specified in the keyword 'MO.kpoint'.
  The second number is a spin state (up=0, down=1). The third number
  specifies the eigenstates, i.e., 0, 1, and 2 correspond to LUMO, LUMO+1,
  and LUMO+2, respectively,
  whose number is specified by the keyword 'num.LUMOs'.
  The 'r' and 'i' mean the real and imaginary parts of the wave function.

As an example, Fig. [31](molecular-orbitals.md#fig:Val_MOs) show the HOMO and LUMO of a valorphin molecule.

<a id="fig:Val_MOs"></a>
<a id="6285"></a>
| ![\includegraphics[width=15.0cm]{Val_MOs.eps}](assets/img190.png) |
| --- |
