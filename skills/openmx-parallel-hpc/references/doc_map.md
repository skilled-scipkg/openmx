# openmx documentation map: Parallel and HPC

Use these docs before opening MPI/OpenMP implementation sources.

## Manual entry points
- `manual/parallel-calculation.md` | NEB image grouping and parallel layout
- `manual/mpi-openmp-hybrid-parallelization.md` | hybrid launch syntax and tradeoffs
- `manual/automatic-running-test.md` | baseline MPI/MPI+OpenMP regression
- `manual/automatic-running-test-with-large-scale-systems.md` | large-scale benchmark suites
- `manual/automatic-running-test-of-negf.md` | transport regression suite
- `manual/automatic-running-test-of-mlwf.md` | MLWF regression suite
- `manual/optical-conductivity-and-dielectric-function-automatic-running-test.md` | CDDF regression suite
- `manual/parallelization-of-negf.md` | transport-specific parallelization
- `manual/mpi-parallelization.md` | general MPI parallelization notes
- `manual/mpi-parallelization-of-kspin.md` | kSpin MPI behavior
- `manual/fully-three-dimensional-parallelization.md` | 3D parallelization details

## Shipped example roots
- `work/large_example` | `-runtestL` inputs and reference outputs
- `work/large2_example` | `-runtestL2` inputs and reference outputs
- `work/large3_example` | `-runtestL3` inputs and reference outputs
- `work/negf_example` | transport regression inputs
- `work/cddf_example` | CDDF regression inputs
- `work/C2H4_NEB.dat` | NEB input for image-group tuning
- `work/Au111Surface_FL.dat` | MPI-capable kSpin example

## Validation fixtures
- `work/input_example/runtest.result_mx17` | standard regression reference
- `work/large_example/runtestL.result_mx17` | large-system reference
- `work/large2_example/runtestL2.result_enaga` | second large-system reference
- `work/large3_example/runtestL3.result_hster` | third large-system reference
- `work/negf_example/runtestNEGF.result` | NEGF reference
- `work/cddf_example/runtestCDDF.result` | CDDF reference
