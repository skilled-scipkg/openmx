<a id="SECTION000760000000000000000"></a>
# Known problems

<a id="5790"></a>
<a id="5794"></a>
- Overcompleteness of basis functions
  <a id="5790"></a>
  When a large number of basis functions is used for dense bulk
  systems with fcc, hcp, and bcc like structures, the basis set
  tends to be overcomplete. In such a case, you may observe erratic
  eigenvalues. To avoid the overcompleteness, a small number of optimized
  basis functions should be used. Another way to avoid the problem is to
  switch off the keyword 'scf.ProExpn.VNA' as
  ```text

    scf.ProExpn.VNA      off       # on|off, default = on
  ```
  In this case, you may need to increase the cutoff energy for the numerical grid in real space
  by the keyword 'scf.energycutoff'.
- Difficulty in getting the SCF convergence
  For large-scale systems with a complex (non-collinear) magnetic structure,
  a metallic electric structure, or the mixture, it is quite difficult
  to get the SCF convergence.
  In such a case, one has to mix the charge density very slowly,
  indicating that the number of SCF steps to get the convergence
  becomes large unfortunately.
- Difficulty in getting the optimized structure
  For weak interacting systems such as molecular systems,
  it is not easy to obtain a completely optimized structure, leading
  that the large number of iteration steps is required. Although the default value of
  criterion for geometrical optimization is $10^{-4}$ Hartree/Bohr for the largest
  force, it would be a compromise to increase the criterion from $10^{-4}$ to

  $5 \times 10^{-4}$ in such a case.
