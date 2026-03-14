<a id="SECTION000540000000000000000"></a>
# Analysis of spin texture in the k-space

Spin splitting in the band structure as can be seen in the Rashba effect may occur when the spin-orbit
coupling is taken into account.
The spin splitting can be resolved in each state and wave vector **k**, and the state- and **k**-resolved
spin splitting, which is a spin structure on the band dispersion relation in the reciprocal space, is called spin texture.
Using a post-processing code 'kSpin' one can calculate the spin texture in the case of a non-collinear calculation
with spin-orbit coupling. The state- and **k**-resolved spin density matrix,
which is referred to as the k-space spin density matrix hereafter, is calculated from the two component
spinor, and takes a form of a $2\times 2$ matrix. The spin texture is actually calculated using the $2\times 2$ matrix.
In addition to the spin texture, 'kSpin' provides us the k-space spin density matrix so that
physical origins of phenomena caused by spin-orbit interaction such as the Rashba effect can be analyzed.
'kSpin' also supports the analysis of spin texture resolved for not only each state and wave vector **k**,
but also atom and pseudo-atomic orbital, which may help us to understand which atom and orbital play a central role
of the spin splitting. Note that 'kSpin' is applicable to not only the Rashba effect but also topological
insulators and systems with non-Rashba type spin splitting.

In the following subsequent subsections, we explain how 'kSpin' can be used for such an analysis
with instructive examples of calculations.
It should be noted that 'kSpin' is compatible with only the non-collinear case, and not supported
for the collinear case.
See also the section of
[34](non-collinear-dft.md#sec:Non-collinear_DFT) 'Non-collinear DFT' to get information of non-collinear calculations.

To acknowledge in any publications by using the functionality,
the citation of the reference [[78](bibliography.md#Kotaka2013)] would be appreciated.
Also, a technical note regarding the implementation of the functionality is available
at http://www.openmx-square.org/tech_notes/note_kSpin-1_0.pdf.

---

**Subsections**

- [General](analysis-of-spin-texture-in-the-k-space-general.md)
- [FermiLoop: Calculation on a constant-energy level](fermiloop-calculation-on-a-constant-energy-level.md)
- [GridCalc: Calculation on a k-point grid](gridcalc-calculation-on-a-k-point-grid.md)
- [BandDispersion: Calculation on the band dispersion relation](banddispersion-calculation-on-the-band-dispersion-relation.md)
- [MulPOnly: Calculation on user-specified k-points](mulponly-calculation-on-user-specified-k-points.md)
- [MulPCalc: k-space spin density matrix resolved to each atom](mulpcalc-k-space-spin-density-matrix-resolved-to-each-atom.md)
- [MPI parallelization of kSpin](mpi-parallelization-of-kspin.md)
