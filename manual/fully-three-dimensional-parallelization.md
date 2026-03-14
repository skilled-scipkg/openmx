<a id="SECTION000254000000000000000"></a>
## Fully three dimensional parallelization

OpenMX Ver. 3.9 supports a fully three dimensional parallelization for data distribution,
while up to and including Ver. 3.6, the parallelization is made by a simple one-dimensional
domain decomposition for **a**-axis of the unit cell for data distribution.
Thus, users do not need to care about how unit cells are specified
to achieve good road balancing. In OpenMX Ver. 3.9, a nearly equivalent parallel efficiency
will be obtained without depending on choice of the unit cell vectors.

---
