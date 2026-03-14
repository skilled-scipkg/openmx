<a id="SECTION000501000000000000000"></a>
## General

To search a minimum energy path (MEP) in geometrical phase space connecting two stable
structures, a nudged elastic band (NEB) method based on Ref. [[134](bibliography.md#Henkelman00)] is
supported in OpenMX Ver. 3.9. The detail of the implementation is summarized as follows:

- Calculation of tangents based on Eqs. (8)-(11) in Ref. [[134](bibliography.md#Henkelman00)]
- Calculation of perpendicular forces based on Eq. (4) in Ref. [[134](bibliography.md#Henkelman00)]
- Calculation of parallel forces based on Eq. (12) in Ref. [[134](bibliography.md#Henkelman00)]
- Optimization method based on a hybrid DIIS+BFGS optimizer

In order to minimize user's efforts in using it, the functionality of NEB has been
realized as one of geometry optimizers with the following features:

- Easy to use
- Hybrid MPI/OpenMP parallelization
- Initial path by the straight line or user's definition
- Only three routines added

---
