<a id="SECTION000547000000000000000"></a>
<a id="sec:MPI-kSpin"></a>
## MPI parallelization of kSpin

MPI parallelization is available for kSpin. More detailed information follows:

**FermiLoop**

Although MPI parallelization is done for k-points on a grid, the second search should be done in each domain picked out in the first search. Since the second search is done sequentially only in domains necessary for calculations, the maximum of the appropriate number of MPI processes is the product of the first and second values for the keyword 'k-plane.2ndStep'. Note that the second search should cost most of computation.

**GridCalc**

MPI parallelization is done for k-points on a grid so that the maximum of the appropriate number of MPI processes is the product of the first and second values for the keyword 'k-plane.1stStep'.

**BandDispersion**

MPI parallelization is done for k-points on every k-path so that the maximum of the appropriate number of MPI processes is the maximum number of k-points among k-paths.

**MulPOnly**

MPI parallelization is done for k-points so that the maximum of the appropriate number of MPI processes is the number of specified k-points.
