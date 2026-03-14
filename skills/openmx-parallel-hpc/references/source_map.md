# openmx source map: Parallel and HPC

Use this map only after the manual/example route is exhausted.

## Fast navigation
- `rg -n "runtestL|runtestNEGF|runtestWF|runtestCDDF|-nt" source/openmx.c source/Runtest.c`
- `rg -n "MPI|Comm_World|Distribute|NEB\\.Parallel|kSpin" source/Make_Comm_Worlds.c source/TRAN_Distribute_Node.c source/neb.c source/kSpin.c`

## Suggested source entry points
- `source/openmx.c` | `main()` handles runtime flags, including `-nt` and `-runtest*`
- `source/Runtest.c` | regression-suite dispatcher and comparison logic
- `source/Make_Comm_Worlds.c` | communicator splitting helpers for multi-world execution
- `source/TRAN_Distribute_Node.c` | transport-specific node/rank distribution
- `source/neb.c` | image grouping and NEB parallel structure
- `source/Band_DFT_Col_NEGF.c` | transport solver path exercised by parallel NEGF runs
- `source/kSpin.c` | MPI-aware post-processing driver
- `source/Inputtools_kSpin.c` | kSpin input parsing for MPI utilities
- `source/mpi_non_blocking.c` | standalone MPI communication test
- `source/mpi_multi_world.c` | standalone multi-world MPI example
- `source/mpi_multi_world2.c` | second multi-world MPI example
- `source/test_openmp.c` | OpenMP runtime check
- `source/test_mpi.c` | MPI runtime check
