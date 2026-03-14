# openmx documentation map: Examples and Tutorials

Use these docs to pick the smallest shipped example before diving deeper.

## Manual entry points
- `manual/test-calculation.md` | smallest end-to-end example
- `manual/examples-and-keywords.md` | NEB example and keyword walkthrough
- `manual/examples-of-the-input-files.md` | cross-package example index
- `manual/examples-for-generating-mlwfs.md` | MLWF example selection
- `manual/example-of-test-calculation.md` | baseline regression example
- `manual/electric-transport-calculations-examples.md` | NEGF example sequence
- `manual/absolute-binding-energies-of-core-levels-xps-core-level-energies-examples.md` | XPS/core-hole example route

## Shipped example roots
- `work/input_example` | standard SCF examples
- `work/geoopt_example` | geometry-optimization examples
- `work/cellopt_example` | cell-optimization examples
- `work/negf_example` | transport examples
- `work/wf_example` | MLWF examples
- `work/cddf_example` | CDDF examples
- `work/unfolding_example` | unfolding examples
- `work/nbo_example` | NBO examples
- `work/C2H4_NEB.dat` | standalone NEB tutorial input
- `work/Si8_NEB.dat` | second standalone NEB tutorial input
- `work/Si-Wannier90.dat` | interface-to-Wannier90 tutorial input
- `work/Si_BoltzTraP.dat` | interface-to-BoltzTraP tutorial input

## Validation fixtures
- `work/input_example/runtest.result_mx17` | SCF regression reference
- `work/negf_example/runtestNEGF.result` | transport regression reference
- `work/cddf_example/runtestCDDF.result` | CDDF regression reference
- `work/geoopt_example/Methane_BFGS.out` | small relaxation reference
- `work/cellopt_example/Cdia-OptC1.out` | small cell-optimization reference
