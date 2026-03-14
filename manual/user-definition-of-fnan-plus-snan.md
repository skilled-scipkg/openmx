<a id="SECTION000244000000000000000"></a>
<a id="sec:User_definition_of_FNAN+SNAN"></a>
## User definition of FNAN+SNAN

<a id="1585"></a>
In all the O($N$) methods supported by OpenMX Ver. 3.9, neighboring atoms in each truncated
cluster are classified into two categories: *first* and *second* neighboring
atoms. If the sum, $r_0+r_{\rm N}$, of a cutoff radius, $r_0$, of basis functions allocated
to the central atom and that, $r_{\rm N}$, of a neighboring atom is smaller than the
distance between the two
atoms, then the neighboring atom is regarded as a first neighboring atom, and
the other atoms, which does not satisfy the criterion, in the truncated cluster are
called the second neighboring atom.
The second neighboring atoms are determined by a keyword 'orderN.HoppingRanges'.
The numbers of the first and second neighboring atoms determined by the keyword
are shown in the standard output as *FNAN* and *SNAN*, respectively.
In addition to the use of the keyword 'orderN.HoppingRanges' for determining FNAN and SNAN,
one can directory control the number, FNAN+SNAN, by the following keyword:

```text

  <orderN.FNAN+SNAN
    1  60 
    2  65 
    3  60
    4  50 
    ..
    .
  orderN.FNAN+SNAN>
```

In this specification, the number of row should be equivalent to that of atoms.
The first column is a serial number corresponding to the serial number defined in
the keyword 'Atoms.SpeciesAndCoordinates', and the second column is the number of
FNAN+SNAN. Then, the first and second neighboring atoms in each truncated cluster
are determined by taking account of the distance between the central atom and
neighboring atoms so that the number of FNAN+SNAN can be equivalent to the value
provided by the second column. FNAN+SNAN may largely change when unit vectors are
changed, leading to sudden change of the total energy as a function of
lattice constant. The user definition of FNAN+SNAN is useful to avoid such a case.
