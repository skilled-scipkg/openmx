# openmx documentation map: Build and Install

Use these docs before opening `source/`.

## Manual entry points
- `manual/installation.md` | baseline build flow and install layout
- `manual/mpi-version.md` | supported MPI build path in OpenMX 3.9
- `manual/mpi-openmp-version.md` | hybrid build flags and runtime `-nt` usage
- `manual/options-for-make.md` | `make install`, `make all`, and helper-code targets
- `manual/tips-for-installation.md` | common compiler and linker failures
- `manual/installation-fftw3.md` | FFTW3 include/library requirements
- `manual/compilation-of-jx.md` | extra `make jx` build path
- `manual/test-calculation.md` | smallest smoke-test command
- `manual/automatic-running-test.md` | `-runtest` semantics and success criteria

## Shipped example and validation roots
- `work/input_example/Methane.dat` | smallest post-build smoke test
- `work/input_example/runtest.result_mx17` | reference format for the standard regression suite
- `work/large_example/runtestL.result_mx17` | reference format for `-runtestL`
- `work/negf_example/runtestNEGF.result` | reference format for `-runtestNEGF`
- `work/cddf_example/runtestCDDF.result` | reference format for `-runtestCDDF`
- `work/wf_example` | MLWF example set exercised by `-runtestWF`
