<a id="SECTION00020000000000000000"></a>
# About OpenMX

OpenMX (Open source package for Material eXplorer) is a software package for
nano-scale material simulations based on density functional theories (DFT) [[1](bibliography.md#DFT)],
norm-conserving pseudopotentials [[32](bibliography.md#BHS),[33](bibliography.md#TM),[34](bibliography.md#KB),[35](bibliography.md#Blochl),[36](bibliography.md#MBK)], and pseudo-atomic
localized basis functions [[41](bibliography.md#Ozaki1)]. The methods and algorithms used in OpenMX and their implementation
are carefully designed for the realization of large-scale *ab initio* electronic structure calculations
on parallel computers based on the MPI or MPI/OpenMP hybrid parallelism.
The efficient implementation of DFT enables us to investigate electronic, magnetic, and geometrical structures
of a wide variety of materials such as bulk materials, surfaces, interfaces, liquids, and low-dimensional materials.
Systems consisting of 1000 atoms can be treated using the conventional diagonalization method if several hundreds
cores on a parallel computer are used.
Even *ab initio* electronic structure calculations for systems consisting of more than 10000 atoms are
possible with the O($N$) methods implemented in OpenMX if several thousands CPU cores on a parallel computer are available.
Since optimized pseudopotentials and basis functions, which are well tested, are provided for many elements,
users may be able to quickly start own calculations without preparing those data by themselves.
Considerable functionalities have been implemented for calculations of physical properties such as magnetic, dielectric,
and electric transport properties. Thus, it is expected that OpenMX can be a useful and powerful theoretical tool for
nano-scale material sciences, leading to better and deeper understanding of complicated and useful materials based on
quantum mechanics. The development of OpenMX has been initiated by the Ozaki group in 2000, and from then onward
many developers listed in the top page of the manual have contributed for further development of the open source
package.
The distribution of the program package and the source codes follow the practice of
the GNU General Public License version 3 (GPLv3) [[102](bibliography.md#GNU)], and they are
downloadable from [http://www.openmx-square.org/](http://www.openmx-square.org/)

Features and capabilities of OpenMX Ver. 3.9 are listed below:

- total energy and forces by cluster, band, O($N$), and low-order scaling methods
- local density approximation (LDA, LSDA) [[2](bibliography.md#LDA),[3](bibliography.md#LSDA),[4](bibliography.md#LSDA-PW)] and generalized gradient approximation (GGA) [[5](bibliography.md#GGA-PBE)] to the exchange-correlation potential
- DFT+U methods [[20](bibliography.md#Han2)]
- norm-conserving pseudopotentials [[2](bibliography.md#LDA),[33](bibliography.md#TM),[34](bibliography.md#KB),[36](bibliography.md#MBK)]
- variationally optimized pseudo-atomic basis functions [[41](bibliography.md#Ozaki1)]
- fully and scalar relativistic treatment within pseudopotential scheme [[12](bibliography.md#MacDonald),[32](bibliography.md#BHS),[16](bibliography.md#Theurich)]
- non-collinear DFT [[8](bibliography.md#Barth),[9](bibliography.md#Kubler),[10](bibliography.md#Sticht),[11](bibliography.md#Oda)]
- constraint DFT for non-collinear spin and orbital orientation [[13](bibliography.md#CNSDFT)]
- macroscopic polarization by Berry's phase [[15](bibliography.md#KingSmith)]
- O($N$) divide-conquer (DC) method [[50](bibliography.md#DC)]
- O($N$) divide-conquer with localized natural orbitals (DC-LNO) method [[51](bibliography.md#DC-LNO)]
- O($N$) Krylov subspace method [[43](bibliography.md#Ozaki3)]
- parallel eigensolver by ELPA [[39](bibliography.md#ELPA)]
- simple, RMM-DIIS [[58](bibliography.md#RMM-DIIS)], GR-Pulay [[57](bibliography.md#GR)], Kerker [[59](bibliography.md#Kerker)], RMM-DIIS with Kerker's metric [[58](bibliography.md#RMM-DIIS)], and RMM-DIIS for Hamiltonian matrix [[58](bibliography.md#RMM-DIIS)] charge mixing schemes
- exchange coupling parameter [[17](bibliography.md#Liechtenstein),[18](bibliography.md#Han1)]
- effective screening medium (ESM) method [[125](bibliography.md#Otani06),[128](bibliography.md#Ohwaki11)]
- scanning tunneling microscope (STM) simulation [[71](bibliography.md#TersoffHamann)]
- DFT-D2 and DFT-D3 method for vdW interaction [[135](bibliography.md#Grimme06),[136](bibliography.md#Grimme10),[137](bibliography.md#Grimme11)]
- unfolding method for band structures [[142](bibliography.md#Chi-Cheng-Lee2013)]
- nudged elastic band (NEB) method [[72](bibliography.md#NEB)]
- calculations of absolute binding energies of core levels in bulks [[88](bibliography.md#Ozaki_XPS2017)]
- optical conductivity and dielectric function [[98](bibliography.md#YTLee2018)]
- charge doping
- uniform electric field
- orbitally decomposed total energy
- fully and constrained geometry optimization
- fully and constrained variable cell optimization
- electric transport calculations by a non-equilibrium Green's function (NEGF) method [[73](bibliography.md#Ozaki_NEGF)]
- construction of maximally localized Wannier functions
- NVE ensemble molecular dynamics
- NVT ensemble molecular dynamics by a velocity scaling [[30](bibliography.md#Woodcock)] and the Nose-Hoover methods [[31](bibliography.md#NH)]
- Mulliken, Voronoi, and ESP fitting analysis of charge and spin densities
- natural population analysis [[7](bibliography.md#Ohwaki2014)]
- analysis of wave functions and electron (spin) densities
- dispersion analysis by the band calculation
- density of states (DOS) and projected DOS
- flexible data format for the input
- interface with BoltzTrap [[100](bibliography.md#Miyata_BoltzTraP2017),[101](bibliography.md#BoltzTraP_WEB)]
- interface with Wannier90 [[145](bibliography.md#wf90)]
- interface with XCrySDen for visualizing data such as charge density [[105](bibliography.md#XCrySDen)]
- completely dynamic memory allocation
- parallel execution by Message Passing Interface (MPI)
- parallel execution by OpenMP
- useful user interface for developers

The collinear and non-collinear (NC) DFT methods are implemented including scalar and fully relativistic
pseudopotentials, respectively. The constraint NC-DFT is also supported to control spin and orbital magnetic
moments. These methods will be useful to investigate complicated NC magnetic structures and the effect of
spin-orbit coupling. The diagonalization of the conventional calculations is performed by a ELPA
based parallel eigensolver [[39](bibliography.md#ELPA)] and ScaLAPACK which scales up to several thousands cores.
The feature may allow us to investigate systems consisting of 1000 atoms using the conventional diagonalization.
Not only the conventional diagonalization scheme is provided for clusters, molecules, slab, and solids,
but also linear scaling and a low-order scaling methods are supported as eigenvalue solver.
With a proper choice for the eigenvalue solvers, systems consisting of more than 10000 atoms can be treated
with careful consideration to balance between accuracy and efficiency.
The variable cell optimization and band unfolding method are available.
As new important features of OpenMX Ver. 3.9, it is worth mentioning that we release a novel O($N$) method based on
divide-conqure approach and localized natural orbitals, and calculations of absolute binding energies
of core levels in bulks, which can be directly compared to binding energies observed in X-ray
photoemission spectroscopy (XPS).
We are continuously working toward development. Motivated contributors who want to develop the open source
codes are always welcome.
