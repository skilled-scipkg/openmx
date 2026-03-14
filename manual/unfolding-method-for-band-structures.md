<a id="SECTION000530000000000000000"></a>
<a id="sec:Unfolding_method_for_band_structures"></a>
# Unfolding method for band structures

When the band structure of a system with imperfection such as surfaces, impurities, vacancies, and structural
distortion calculated by the supercell approach is compared to spectrum measured by
Angle-Resolved Photoemission Spectroscopy (ARPES), the experimentally measured periodicity
of the system is generally different from that of the supercell we introduced for the calculation.
In such a case, the band structure obtained by the supercell calculation should be represented
for the Brillouin zone of a proper unit cell so that the periodicity of calculated band structure
can be consistent with the measured one. Though the choice of the proper unit cell is
not obvious in general cases, OpenMX provides a method for unfolding the band structure of
the supercell into the Brillouin zone of a reference unit cell that a user specifies
in the input file [[142](bibliography.md#Chi-Cheng-Lee2013)].
The functionality is supported for not only collinear, but also non-collinear DFT calculations.
Even in case that you are not interested in comparison between calculations and experiments
by unfolding the band structrue, the method would be useful to analyze how each band consists
of pseudo-atomic orbitals, providing information for physical nature of bands, and how each
band is pertubed by the introduced imperfection.

In the following subsequent subsections we explain how these functionalities can be utilized
by demonstrating a series of calculations.

---

**Subsections**

- [Analysis of band structures](analysis-of-band-structures.md)
- [Unfolding of band structures](unfolding-of-band-structures.md)
- [The origin of the reference unit cell](the-origin-of-the-reference-unit-cell.md)
- [Intensity map of unfolded spectral weight](intensity-map-of-unfolded-spectral-weight.md)
- [In case of non-collinear DFT calculations](in-case-of-non-collinear-dft-calculations.md)
- [Examples](unfolding-method-for-band-structures-examples.md)
