<a id="SECTION000433000000000000000"></a>
## OpenMX calculation to generate jx input

In advance of the $J_{ij}$ calculation, it is necessary to perform a collinear DFT calculation to generate a scfout file.
To generate the scfout file, you can add the following keyword 'HS.fileout' in the OpenMX input file as follows:

```text

     HS.fileout                   on       # on|off, default=off
```

Note that it might be necessary to take a relatively small number of orbitals in the OpenMX calculation for the jx execution,
because the pseudo-atomic orbitals have to be localized well in the current implementation. For example, s2p2d2 for Fe and
s2p1d1 for Nd should be optimal setting for the atomic orbital specification.

---
