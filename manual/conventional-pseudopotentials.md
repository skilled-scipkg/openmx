<a id="SECTION000121000000000000000"></a>
## Conventional pseudopotentials

<a id="696"></a>
The core Coulomb potential in OpenMX is replaced by a tractable
norm-conserving pseudopotential proposed by Morrison, Bylander,
and Kleinman [[36](bibliography.md#MBK)], which is a norm-conserving version of the ultrasoft
pseudopotential by Vanderbilt [[37](bibliography.md#Vanderbilt)].
Although the pseudopotentials can be generated using ADPACK
which is a program package for atomic density functional calculations and
available from a website (http://www.openmx-square.org/),
for your convenience, we offer a database (http://www.openmx-square.org/)
of the pseudopotentials as the database Ver. 2019.
If you want to use pseudopotentials stored in the database, then
copy them to the directory, 'openmx3.9/DFT_DATA19/VPS/', while most of data have
been already copied in the distributed package of OpenMX Ver. 3.9.
You can freely utilize these data, but we cannot offer any warranty on these data.
The assignation of pseudopotentials can be made using a keyword
'Definition.of.Atomic.Species'
as in the case of specification of
basis functions as follows:

```text

   <Definition.of.Atomic.Species
     H   H6.0-s2p1        H_CA19
     C   C6.0-s2p2        C_CA19
   Definition.of.Atomic.Species>
```

The pseudopotential file can be specified in the third column, and
the file must be existing in the directory 'DFT_DATA19/VPS'.
In the specification of atomic coordinates, it is required to give
the number of electrons for up- and down-spin states for each atom as follows:

```text

   <Atoms.SpeciesAndCoordinates
     1   C      0.000000    0.000000    0.000000     2.0  2.0 
     2   H     -0.889981   -0.629312    0.000000     0.5  0.5
     3   H      0.000000    0.629312   -0.889981     0.5  0.5
     4   H      0.000000    0.629312    0.889981     0.5  0.5
     5   H      0.889981   -0.629312    0.000000     0.5  0.5
   Atoms.SpeciesAndCoordinates>
```

where the sixth and seventh columns give the number of initial charges for
up and down spin states for each atom, respectively. The sum of up and down charges
for the atomic element should be equivalent to the number of electrons which is taken
into account in the pseudopotential generation. Then, the proper number for
each pseudopotential can be found in the pseudopotential file '*.vps'.
For example, you will see the following line in the file 'C_PBE19.vps' for
carbon atom in the database Ver. 2019.

```text

    valence.electron            4.0000
```

The number '4.0' corresponds to the number of electrons which is taken into
account in the pseudopotential generation.
So, we see in the above example that the sum of up (2.0) and down (2.0) spins
charges is 4.0 for 'C' in the specification of
'Atoms.SpeciesAndCoordinates'.
In Tables [2](specification-of-a-directory-storing-pao-and-vps-files.md#table:Choice-PAOs2) and [1](specification-of-a-directory-storing-pao-and-vps-files.md#table:Choice-PAOs1) we show
the number of valence electrons in the pseudopotentials provided as the database Ver. 2019.

When you make pseudopotentials using ADPACK by yourself, you
should pay attention to the following points.

- Check whether unphysical calculations have been caused by the ghost states or not. Because of the use of the separable form, the ghost states often appear. You should check whether the pseudopotentials are appropriate or not by performing calculations of simple systems before you calculate systems that you are interested in.
- Make smooth core densities for the partial core correction. If not so, numerical instabilities appear often, since a high energy cutoff is needed for accurate numerical integrations.

You will find the further details in the manual of the program package 'ADPACK'.
However, it is noted that generation of good pseudopotentials requires considerable
experiences more than what we think at the beginning.
