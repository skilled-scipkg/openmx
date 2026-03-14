---
name: openmx-parallel-hpc
description: This skill should be used when users ask about parallel and hpc in openmx; it prioritizes documentation references and then source inspection only for unresolved details.
---

# openmx: Parallel and HPC

## High-Signal Playbook
- Route conditions:
  Use this skill for MPI/OpenMP launch shape, large-scale regression runs, NEB load balance, transport/k-point post-processing at scale, and diagnosing rank/thread-dependent failures.
  Route build/link issues to `openmx-build-and-install`, ordinary workflow setup to `openmx-simulation-workflows`, and developer-side MPI spawning to `openmx-api-and-scripting`.
- Triage questions:
  What is the target workflow: ordinary SCF, NEB, NEGF, MLWF/CDDF test, or a kSpin utility?
  How many MPI ranks, threads per rank, and nodes are available?
  Is the current bottleneck wall time, memory, or a crash that appears only in parallel?
  Do you need a minimal sanity check first, or a large-scale benchmark?
  Is there a shipped reference result you can compare against immediately?
- Canonical workflow:
  1. Validate the current build with the smallest relevant MPI job before changing parallel shape.
  2. Start with flat MPI, then compare against MPI/OpenMP hybrid using the same example input.
  3. For large-scale checks, run the smallest built-in regression that exercises the target feature: `-runtest`, `-runtestNEGF`, `-runtestWF`, `-runtestCDDF`, `-runtestL`, `-runtestL2`, or `-runtestL3`.
  4. For NEB memory pressure, tune `MD.NEB.Parallel.Number` so the image grouping matches the available ranks.
  5. Compare numerical differences against the shipped reference result files before chasing performance-only tuning.
  6. If scaling or correctness still depends strongly on rank/thread count, inspect the targeted source entry point from `references/source_map.md`.
- Minimal working example:
```text
cd work
mpirun -np 32 ./openmx large_example/DIA512-1.dat > dia512-1.std
mpirun -np 32 ./openmx large_example/DIA512-1.dat -nt 4 > dia512-1-hybrid.std
mpirun -np 16 ./openmx -runtestNEGF
mpirun -np 112 ./openmx -runtestL
```
```text
MD.Type                    NEB
MD.NEB.Number.Images       8
MD.NEB.Parallel.Number     4
```
- Pitfalls/fixes:
  OpenMX 3.9 supports hybrid MPI/OpenMP, but the manual does not promise hybrid will always be faster than flat MPI.
  Large-scale tests are memory hungry; a segmentation fault on too few ranks can be a resource issue rather than a physics bug.
  NEB load balance is much better when the number of MPI ranks is divisible by the number of images or by `MD.NEB.Parallel.Number`.
  Parallel transport and kSpin post-processing have separate data-distribution paths from ordinary SCF; validate them with their shipped fixtures instead of with Methane.
  `MPI_Comm_spawn` examples are not a substitute for normal production launch scripts.
- Validation checks:
  `-runtest` should agree with the shipped reference files in `work/input_example/`.
  `-runtestL`, `-runtestL2`, and `-runtestL3` should agree with the shipped result files in `work/large_example`, `work/large2_example`, and `work/large3_example`.
  `-runtestNEGF` should agree with `work/negf_example/runtestNEGF.result`.
  `-runtestCDDF` should agree with `work/cddf_example/runtestCDDF.result` and satisfy the documented `0.1` tolerance.
  NEB runs should keep reducing the maximum force in `.neb.opt` without rank-count-dependent instabilities.

## Primary documentation references
- `manual/parallel-calculation.md`
- `manual/mpi-openmp-hybrid-parallelization.md`
- `manual/automatic-running-test.md`
- `manual/automatic-running-test-with-large-scale-systems.md`
- `manual/automatic-running-test-of-negf.md`
- `manual/automatic-running-test-of-mlwf.md`
- `manual/optical-conductivity-and-dielectric-function-automatic-running-test.md`
- `manual/parallelization-of-negf.md`
- `manual/mpi-parallelization.md`
- `manual/mpi-parallelization-of-kspin.md`
- `manual/fully-three-dimensional-parallelization.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `work/large_example`
- `work/large2_example`
- `work/large3_example`
- `work/negf_example`
- `work/cddf_example`
- `work/C2H4_NEB.dat`
- `work/Au111Surface_FL.dat`

## Test references
- `work/input_example`
- `work/large_example`
- `work/large2_example`
- `work/large3_example`
- `work/negf_example`
- `work/cddf_example`

## Optional deeper inspection
- `source`

## Source entry points for unresolved issues
- `source/openmx.c`
- `source/Runtest.c`
- `source/Make_Comm_Worlds.c`
- `source/TRAN_Distribute_Node.c`
- `source/neb.c`
- `source/Band_DFT_Col_NEGF.c`
- `source/kSpin.c`
- `source/Inputtools_kSpin.c`
- `source/mpi_non_blocking.c`
- `source/mpi_multi_world.c`
- `source/mpi_multi_world2.c`
- `source/test_openmp.c`
- `source/test_mpi.c`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" source`).
