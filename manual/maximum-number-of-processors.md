<a id="SECTION000255000000000000000"></a>
## Maximum number of processors

Up to and including Ver. 3.6, the number of MPI processes that users can utilize
for the parallel calculations is limited up to the number of atoms in the system.
OpenMX Ver. 3.9 does not have the limitation. Even if the number of MPI processes exceeds
the number of atoms, the MPI parallelization is efficiently performed.
The capability may be useful especially for a calculation where the number of **k**-points
is much larger than the number of atoms in the system.

---
