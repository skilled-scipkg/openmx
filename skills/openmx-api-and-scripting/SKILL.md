---
name: openmx-api-and-scripting
description: This skill should be used when users ask about api and scripting in openmx; it prioritizes documentation references and then source inspection only for unresolved details.
---

# openmx: API and Scripting

## High-Signal Playbook
- Route conditions:
  Use this skill for `.scfout` consumers, `HS.fileout`, helper binaries such as `analysis_example`, embedding OpenMX via `MPI_Comm_spawn`, and export to Wannier90.
  Route method details of MLWF or optical conductivity back to `openmx-theory-and-methods`, and route install/compiler issues for helper binaries to `openmx-build-and-install`.
- Triage questions:
  Do you need matrix data from `System.Name.scfout`?
  Are you writing a custom post-processor or just using `analysis_example`?
  Are you trying to call OpenMX from another MPI program?
  Do you need OpenMX to emit Wannier90 input files?
  Is the source data coming from OpenMX 3.9, or from an older `scfout` format?
  Do you need matrices only, or also transport-region atom counts and spin-resolved blocks?
- Canonical workflow:
  1. For matrix export, enable `HS.fileout on` in the parent SCF input and run OpenMX normally.
  2. Build the helper binary with `make analysis_example`; the executable is copied into `work/`, where you can run `./analysis_example System.Name.scfout`.
  3. For custom tooling, include `read_scfout.h` and call `read_scfout(argv)` from your own MPI-aware main program.
  4. For embedding OpenMX, inspect `example_mpi_spawn.c`, `Make_Comm_Worlds.c`, build `make example_mpi_spawn`, and adapt the communicator-splitting pattern.
  5. For Wannier90 export, set `Wannier.Func.Calc on` plus `Wannier90.fileout on`; OpenMX writes `.amn`, `.mmn`, `.eig`, and `.win` for `wannier90.x`.
  6. Validate the files emitted by the interface before debugging downstream tools.
- Minimal working example:
```text
HS.fileout                 on
mpirun -np 4 openmx System.dat
cd source && make analysis_example
cd ../work && ./analysis_example System.scfout > HS.out
```
```c
#include "read_scfout.h"
int main(int argc, char *argv[]) {
  read_scfout(argv);
  return 0;
}
```
- Pitfalls/fixes:
  OpenMX 3.9 changed the `scfout` format; the manual explicitly says older `scfout` files cannot be analyzed by 3.9 helper codes.
  Without `HS.fileout on`, there is no `System.Name.scfout` to consume.
  `read_scfout.c` only supports SCFOUT format version 3 and exits on unsupported versions.
  The `MPI_Comm_spawn` manual page contains an explicit warning that part of the description was incorrect at release time; use it carefully.
  Spawned OpenMX children suppress most stdout and write to `System.Name.std`; this is expected behavior from `Input_std.c`.
  `Wannier90.fileout on` only produces interface files; actual MLWF construction still requires external `wannier90.x` / `postw90.x`.
- Convergence/validation checks:
  `analysis_example` should at least print atom counts and matrix blocks after reading the `.scfout`.
  `read_scfout` should report the supported SCFOUT format and finish without an endianness/version error.
  `example_mpi_spawn` should create separate OpenMX child jobs and corresponding `*.std` files.
  Wannier90 export is valid only when `.amn`, `.mmn`, `.eig`, and `.win` are all present.

## Primary documentation references
- `manual/interface-for-developers.md`
- `manual/calling-openmx-as-library-or-computational-engine.md`
- `manual/interface-with-wannier90.md`
- `manual/maximally-localized-wannier-function-output-files.md`
- `manual/maximally-localized-wannier-function.md`
- `manual/optical-conductivity-and-dielectric-function-codes.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `work/wf_example`
- `work/input_example`

## Test references
- `work/wf_example`

## Optional deeper inspection
- `source`

## Source entry points for unresolved issues
- `source/SCF2File.c`
- `source/analysis_example.c`
- `source/read_scfout.c`
- `source/read_scfout.h`
- `source/example_mpi_spawn.c`
- `source/Make_Comm_Worlds.c`
- `source/openmx.c`
- `source/Generate_Wannier.c`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" source`).
