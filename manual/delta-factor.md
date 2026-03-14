<a id="SECTION000622000000000000000"></a>
## Delta factor

<a id="5586"></a>
As well as 'EvsLC', a similar functionality is provided as

```text

  MD.Type                     DF
```

by which OpenMX automatically calculates the total energy of the system with volumes of
-6, -4, -2, 0, 2, 4, and 6 %, where the original structure given in the input file is taken
to be the reference.
The regulation of volume is simply performed by considering uniform change of lattice vectors,
**a**-, **b**-, and **c**-axes. The volume and the corresponding total energy are output
to a file '*System.Name*.DF'. The data can be used to calculate the delta factor proposed in Ref. [[40](bibliography.md#DeltaFactor)].

---
