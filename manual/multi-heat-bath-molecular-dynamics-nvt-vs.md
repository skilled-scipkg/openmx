<a id="SECTION000184000000000000000"></a>
## Multi-heat bath molecular dynamics (NVT_VS)

<a id="1176"></a>
OpenMX Ver. 3.9 supports a multi-heat bath molecular dynamics simulation where
the temperature of each grouped atom is controlled with a heat-bath by a velocity
scaling scheme [[30](bibliography.md#Woodcock)].
The method is performed by the following keyword:

```text

    MD.Type          NVT_VS4
```

The number of groups is specified by

```text

    MD.num.AtomGroup    2
```

and the groups are defined by

```text

    <MD.AtomGroup
      1  1 
      2  1
      3  1
      4  2
      5  2
    MD.AtomGroup>
```

The beginning of the description must be '$<$MD.AtomGroup', and
the last of the description must be 'MD.AtomGroup$>$'.
The first column is a sequential serial number for identifying atoms.
The second column is an identification number for each atom, representing
the group to which the atom belongs. The identification number has to be specified
from 1, and followed by 2, 3, $\cdots$.
The above is an example where only five atoms are involved in the system and
there are two groups. In Ver. 3.9, the profile of temperature for all the groups
is controlled by the keyword 'MD.TempControl' as discussed in the subsection
'NVT molecular dynamics by a velocity scaling'. In the future release, we will
support a functionality that temperature is independently controlled for each group.
