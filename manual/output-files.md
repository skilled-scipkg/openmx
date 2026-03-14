<a id="SECTION00090000000000000000"></a>
# Output files

<a id="514"></a>
In case of 'level.of.fileout=0', the following files are generated.
In the following, '*System.Name*' is the file name specified by the keyword 'System.Name'.

- *System.Name*.out
  The history of SCF calculations, the history of geometry optimization,
  Mulliken charges, the total energy, and the dipole moment.
- *System.Name*.xyz
  The final geometrical structure obtained by MD or the geometry
  optimization, which can be read by OpenMX Viewer [[152](bibliography.md#YTL-OpenMX-Viewer),[151](bibliography.md#OpenMX-Viewer)] and XCrySDen [[105](bibliography.md#XCrySDen)].
- *System.Name*.bulk.xyz
  If 'scf.EigenvalueSolver=Band', atomic coordinates including atoms
  in copied cells are output, which can be read by OpenMX Viewer [[152](bibliography.md#YTL-OpenMX-Viewer),[151](bibliography.md#OpenMX-Viewer)] and XCrySDen [[105](bibliography.md#XCrySDen)].
- *System.Name*_rst/
  The directory storing restart files.
- *System.Name*.md
  Geometrical coordinates at every MD step in the xyz format, which can be read
  by OpenMX Viewer [[152](bibliography.md#YTL-OpenMX-Viewer),[151](bibliography.md#OpenMX-Viewer)].
- *System.Name*.md2
  Geometrical coordinates at the final MD step with the species names
  that you specified .
- *System.Name*.cif
  Initial geometrical coordinates in the cif format.
- *System.Name*.ene
  Values computed at every MD step. The values are found in the routine 'iterout.c'.

<a id="531"></a>
In case of 'level.of.fileout=1', the following Gaussian cube files
are generated, in addition to files generated in 'level.of.fileout=0',
In the following, '*System.Name*' is the file name specified by the keyword 'System.Name'.

- *System.Name*.tden.cube
  Total electron density in the Gaussian cube format.
- *System.Name*.sden.cube
  If the spin-polarized calculation using 'LSDA-CA', 'LSDA-PW', or 'GGA-PBE'
  is performed, then spin electron density is output in the Gaussian
  cube format.
- *System.Name*.dden.cube
  Difference electron density taken from superposition of atomic densities of constituent atoms
  in the Gaussian cube format.
- *System.Name*.v0.cube
  The Kohn-Sham potential excluding the non-local potential for up-spin in the Gaussian cube format.
  If the projector expansion method is switched on by the keyword 'scf.ProExpn.VNA', the VNA potential is also excluded.
  See also the technical note 'Total Energy and Forces' at http://www.openmx-square.org/tech_notes/tech_notes.html .
- *System.Name*.v1.cube
  The Kohn-Sham potential excluding the non-local potential
  for down-spin in the Gaussian cube format
  in the spin-polarized calculation.
  If the projector expansion method is switched on by the keyword 'scf.ProExpn.VNA', the VNA potential is also excluded.
  See also the technical note 'Total Energy and Forces' at http://www.openmx-square.org/tech_notes/tech_notes.html .
- *System.Name*.vhart.cube
  The Hartree potential calculated by the difference charge density in the Gaussian cube format.
  See also the technical note 'Total Energy and Forces' at

  http://www.openmx-square.org/tech_notes/tech_notes.html .

<a id="541"></a>
In case of 'level.of.fileout=2', the following files are generated
in addition to files generated in level.of.fileout=1,
In the following, '*System.Name*' is the file name specified by the keyword 'System.Name'.

- *System.Name*.vxc0.cube
  The exchange-correlation potential for up-spin
  in the Gaussian cube format.
- *System.Name*.vxc1.cube
  The exchange-correlation potential for down-spin in
  the Gaussian cube format.
- *System.Name*.grid
  The real space grids which are used numerical integrations and the solution
  of Poisson's equation.

<a id="548"></a>
<a id="549"></a>
If 'MO.fileout=ON' and
'scf.EigenvalueSolver=Cluster',
the following files are also generated:

- *System.Name*.homo0_0.cube, *System.Name*.homo0_1.cube, ...
  The HOMOs are output in the Gaussian cube format.
  The first number below 'homo' means a spin state
  (up=0, down=1). The second number specifies the eigenstates, i.e.,
  0, 1, and 2 correspond to HOMO, HOMO-1, and HOMO-2, respectively.
- *System.Name*.lumo0_0.cube, *System.Name*.lumo0_1.cube, ...
  The LUMOs are output in the Gaussian cube format.
  The first number below 'lumo' means a spin state
  (up=0, down=1). The second number specifies the eigenstates, i.e.,
  0, 1, and 2 correspond to LUMO, LUMO+1, and LUMO+2, respectively.

<a id="556"></a>
<a id="557"></a>
If 'MO.fileout=ON' and
'scf.EigenvalueSolver=Band',
the following files are also generated:

- *System.Name*.homo0_0_0_r.cube, *System.Name*.homo1_0_1_r.cube, ... *System.Name*.homo0_0_0_i.cube, *System.Name*.homo1_0_1_i.cube, ...
  The HOMOs are output in the Gaussian cube format.
  The first number below 'homo' means the k-point
  number, which is specified by the keyword 'MO.kpoint'.
  The second number is a spin state (up=0, down=1). The third number
  specifies the eigenstates, i.e., 0, 1, and 2 correspond to HOMO, HOMO-1,
  and HOMO-2, respectively.
  The 'r' and 'i' mean the real and imaginary parts of the wave function.
- *System.Name*.lumo0_0_0_r.cube, *System.Name*.lumo1_0_1_r.cube, ... *System.Name*.lumo0_0_0_i.cube, *System.Name*.lumo1_0_1_i.cube, ...
  The LUMOs are output in the Gaussian cube format.
  The first number below 'lumo' means the k-point
  number, which is specified in the keyword, MO.kpoint.
  The second number is a spin state (up=0, down=1). The third number
  specifies the eigenstates, i.e., 0, 1, and 2 correspond to LUMO, LUMO+1,
  and LUMO+2, respectively.
  The 'r' and 'i' mean the real and imaginary parts of the wave function.

<a id="568"></a>
<a id="569"></a>
If 'Band.Nkpath' is not 0 and
'scf.EigenvalueSolver=Band',
the following file is also generated:

- *System.Name*.Band
  A data file for the band dispersion.

<a id="573"></a>
If 'Dos.fileout=ON', the following files are also generated:

- *System.Name*.Dos.val
  A data file of eigenvalues for calculating the density of states.
- *System.Name*.Dos.vec
  A data file of eigenvectors for calculating the density of states.

<a id="578"></a>
<a id="579"></a>
If 'scf.SpinPolarization=NC'
and 'level.of.fileout=1' or '2',
the following files are also generated:

- *System.Name*.nco.xsf
  A vector file which stores a non-collinear orbital moment
  projected on each atom by means of Mulliken analysis, which
  can be visualized using 'Display$\to $Forces' in XCrySDen.
- *System.Name*.nc.xsf
  A vector file which stores a non-collinear spin moment
  projected on each atom by means of Mulliken analysis, which
  can be visualized using 'Display$\to $Forces' in XCrySDen.
- *System.Name*.ncsden.xsf
  A vector file which stores a non-collinear spin moment
  on real space grids, which can be visualized using
  'Display$\to $Forces' in XCrySDen.
