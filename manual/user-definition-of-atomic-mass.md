<a id="SECTION000187000000000000000"></a>
## User definition of atomic mass

<a id="1197"></a>
In molecular dynamics simulations, OpenMX uses the atomic mass defined in
'Set_Atom_Weight() of SetPara_DFT.c'. However, one can easily change the
atomic mass by the keyword

'Definition.of.Atomic.Species'.
In such a case, the atomic mass is defined by the fourth column as

```text

  <Definition.of.Atomic.Species
   H   H5.0-s1          H_PBE19      2.0
   C   C5.0-s1p1        C_PBE19     12.0
  Definition.of.Atomic.Species>
```

If the fourth column is not given explicitly, then the default atomic mass
will be used. This may be useful to investigate the effect of atomic mass
in molecular dynamics, and also may allow us to use a larger time step by using
especially the deuterium mass for hydrogen atom.
For the definition of atomic mass, we use the unified atomic mass unit
that the principal isotope of carbon atom is 12.0.

---
