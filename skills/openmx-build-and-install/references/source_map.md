# openmx source map: Build and Install

Use this map only after the manual/example route is exhausted.

## Fast navigation
- `rg -n "make install|DESTDIR|UTIL|analysis_example|example_mpi_spawn" source/makefile`
- `rg -n "runtest|maketest|-nt|-show" source/openmx.c source/Runtest.c`

## Suggested source entry points
- `source/makefile` | `PROG`, `DESTDIR`, and `UTIL` define the install target and helper binaries
- `source/openmx.c` | `main()` parses runtime flags such as `-nt`, `-show`, and `-runtest*`
- `source/Runtest.c` | `Runtest()` and `run_main()` drive the shipped regression suites
- `source/test_mpi.c` | minimal MPI runtime sanity check
- `source/test_openmp.c` | minimal OpenMP runtime sanity check
- `source/analysis_example.c` | standalone helper built by `make analysis_example`
- `source/example_mpi_spawn.c` | standalone helper built by `make example_mpi_spawn`
