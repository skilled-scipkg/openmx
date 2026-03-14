# openmx source map: API and Scripting

Use this map only after the manual/example route is exhausted.

## Fast navigation
- `rg -n "HS\\.fileout|scfout|read_scfout" source/SCF2File.c source/read_scfout.c source/analysis_example.c`
- `rg -n "MPI_Comm_spawn|Make_Comm_Worlds" source/example_mpi_spawn.c source/Make_Comm_Worlds.c`

## Suggested source entry points
- `source/SCF2File.c` | `SCF2File()` writes the `.scfout` payload behind `HS.fileout`
- `source/read_scfout.c` | `read_scfout()` and `free_scfout()` implement the reader API
- `source/read_scfout.h` | exported data structures for custom post-processing
- `source/analysis_example.c` | minimal consumer of `read_scfout()`
- `source/example_mpi_spawn.c` | sample host program for `MPI_Comm_spawn`
- `source/Make_Comm_Worlds.c` | `Make_Comm_Worlds()` splits communicators for multi-job launches
- `source/openmx.c` | runtime behavior of spawned child jobs and CLI flags
- `source/Generate_Wannier.c` | Wannier90 export behavior when interface files look wrong
