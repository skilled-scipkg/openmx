<a id="SECTION000670000000000000000"></a>
# Automatic determination of the cell size

<a id="5697"></a>
<a id="5698"></a>
When you calculate an isolated system, you are required to provide
a super cell so that the isolated system does not overlap with the
image systems in the repeated cells via basis orbitals. The larger cell size can cause
a numerical inefficiency, since a larger number of grids are used
in the solution of the Poisson's equation in this case.
Therefore, the use of the minimum cell size is desirable in terms
of computational efficiency. OpenMX supports the requirement.
If you remove the specification for the cell size, that is,
from '$<$Atoms.UnitVectors'
to 'Atoms.UnitVectors$>$',
then OpenMX automatically determines an appropriate cell which
does not overlap the next cells and fulfills the required
cutoff energy.
The determined cell vectors are displayed in the standard output
like this:

```text

  <Set_Cluster_UnitCell> automatically determined UnitCell(Ang.)
  <Set_Cluster_UnitCell> from atomic positions and Rc of PAOs (margin= 10.00%)
  <Set_Cluster_UnitCell> 6.614718 0.000000 0.000000
  <Set_Cluster_UnitCell> 0.000000 6.041246 0.000000
  <Set_Cluster_UnitCell> 0.000000 0.000000 6.614718

  widened unit cell to fit energy cutoff (Ang.)
  A = 6.744142 0.000000 0.000000 (48)
  B = 0.000000 6.322633 0.000000 (45)
  C = 0.000000 0.000000 6.744142 (48)
```

---
