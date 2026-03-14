<a id="SECTION000601000000000000000"></a>
## General

In OpenMX Ver. 3.9, the conductivity and dielectric function can be calculated based on the Kubo-Greenwood formula [[98](bibliography.md#YTLee2018)].
Starting from the Born approximation, the complex tensor of conductivity and dielectric function which are frequency dependent are
calculated within a linear response to a perturbing frequency dependent electric field.
Other physical quantities such as absorption, extinction, transmission, reflection, and refractive index are also calculated,
which are all derived from the conductivity. The functionality is compatible with only the collinear calculations.
The extension of the functionality to the non-collinear case will be supported in the future release.
Since the multi-level parallelization has been implemented, it is possible to perform large-scale calculations of systems
including more than 1000 atoms on massively parallel computers.

---
