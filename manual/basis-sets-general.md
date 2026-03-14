<a id="SECTION000111000000000000000"></a>
## General

OpenMX uses numerical pseudo-atomic orbitals (PAOs) $\chi$ as basis function to expand one-particle
Kohn-Sham wave functions. The PAO function is given by a product of a radial function $R$ and
a real spherical harmonic function $Y$ as

| $\displaystyle \chi({\bf r}) = R(r)Y(\hat{{\bf r}}),$ |  |  |  |
| --- | --- | --- | --- |

where the radial function $R$ is a numerically defined one, and finite within a cutoff radius
in real space. In other words, the function $R$ becomes zero beyond a pre-defined cutoff radius.
The PAO function calculated by ADPACK is called *primitive* function, and an *optimized* PAO
function is obtained by the orbital optimization method in OpenMX starting from
the primitive PAO function [[41](bibliography.md#Ozaki1)]. They are stored in a file with a file extension
of 'pao'. When the OpenMX calculation is performed, the numerical data stored in the
file are read, and the value at any $r$ is obtained by an interpolation technique.
The files with the file extension of 'pao' should be
stored in a directory, e.g., 'DFT_DATA19/PAO', where the directory without 'PAO' can be
specified by the following keyword:

```text

    DATA.PATH   ../DFT_DATA19    # default=../DFT_DATA19
```

Both the absolute and relative specifications are possible, and the default is '../DFT_DATA19'.

<a id="612"></a>
In an input file for the OpenMX calculation,
The basis set is specified by a keyword
'Definition.of.Atomic.Species'
as follows:

```text

   <Definition.of.Atomic.Species
     H   H5.0-s2p1      H_PBE19
     C   C5.0-s2p1      C_PBE19
   Definition.of.Atomic.Species>
```

where an abbreviation, H5.0-s2p1, of the basis function is introduced.
H5.0 stands for the file name of the PAO functions without the file extension
which must exist in a directory specified by the keyword 'DATA.PATH', e.g., DFT_DATA19/PAO,
and 5.0 implies the cutoff radius of the PAO functions.
Also, s2p1 means that two s-state radial functions and one p-state radial function
stored in the file are used.
In this case, totally five PAO basis functions (2x1+1x3=5) are assigned for 'H'.

Since optimized basis functions are available on the website (http://www.openmx-square.org/)
as the database Ver. 2019. We recommend for general users to use these optimized basis functions.
But for experts, both the primitive and optimized PAO functions are explained
in the subsequent sections.
