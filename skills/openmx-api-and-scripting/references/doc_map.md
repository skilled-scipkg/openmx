# openmx documentation map: API and Scripting

Use these docs before inspecting helper-code sources.

## Manual entry points
- `manual/interface-for-developers.md` | `HS.fileout`, `.scfout`, and `analysis_example`
- `manual/calling-openmx-as-library-or-computational-engine.md` | `MPI_Comm_spawn` host-program pattern
- `manual/interface-with-wannier90.md` | Wannier90 export path
- `manual/maximally-localized-wannier-function-output-files.md` | `.mmn`, `.amn`, `.eigen`, and `.HWR`
- `manual/maximally-localized-wannier-function.md` | MLWF prerequisites for export
- `manual/optical-conductivity-and-dielectric-function-codes.md` | source-level optical/CDDF code layout
- `manual/additional-functionalities.md` | cross-links to developer-facing extras

## Shipped example roots
- `work/input_example/Methane.dat` | smallest `HS.fileout`-style parent run
- `work/wf_example/Si.dat` | compact MLWF export example
- `work/Si-Wannier90.dat` | direct Wannier90 export example
- `work/Si_BoltzTraP.dat` | downstream tool handoff example
