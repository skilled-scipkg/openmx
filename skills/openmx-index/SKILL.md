---
name: openmx-index
description: This skill should be used when users ask how to use openmx and the correct generated documentation skill must be selected before going deeper into source code.
---

# openmx Skills Index

## Route the request
- Route to the smallest surviving topic skill before opening `source/`.
- Prefer the enriched core skills for first-pass answers; use `openmx-advanced-topics` for narrow manual pages that were collapsed out of the tree.

## Topic skills
- `openmx-build-and-install`: compiler/library setup, `make` targets, smoke tests, and install verification
- `openmx-inputs-and-modeling`: input structure, basis and VPS choices, XC functionals, DFT+U setup
- `openmx-simulation-workflows`: SCF, restart, geometry optimization, cell optimization, MD, and NEB
- `openmx-theory-and-methods`: NEGF, MLWF, optical conductivity, unfolding, and other advanced methods
- `openmx-analysis-and-output`: output files, visualization, bands, DOS, and downstream analysis tools
- `openmx-api-and-scripting`: `HS.fileout`, `read_scfout`, `analysis_example`, `MPI_Comm_spawn`, and Wannier90 export
- `openmx-parallel-hpc`: MPI/OpenMP execution, large-scale runtests, and JX/HPC scaling concerns
- `openmx-examples-and-tutorials`: closest shipped example or tutorial to clone before editing inputs
- `openmx-advanced-topics`: collapsed niche topics such as DFT+U variants, non-collinear extras, JX config, Voronoi/Zeeman/orbital-moment analysis, transmission/current-density details, and known problems

## Main docs and code roots
- Docs: `manual/index.md`, `manual/contents.md`, `manual/README.md`
- Examples: `work/input_example`, `work/geoopt_example`, `work/cellopt_example`, `work/negf_example`, `work/wf_example`, `work/cddf_example`, `work/unfolding_example`, `work/nbo_example`
- Large-scale tests: `work/large_example`, `work/large2_example`, `work/large3_example`
- Source: `source`

## Routing rules
- Build failures, missing libraries, or post-install verification -> `openmx-build-and-install`
- Input syntax, basis/VPS, k-grid, XC, or DFT+U choices -> `openmx-inputs-and-modeling`
- Fixed-SCF, restart, relaxation, cell optimization, MD, or NEB -> `openmx-simulation-workflows`
- Lead/device transport, MLWF, CDDF, unfolding, or advanced formalism questions -> `openmx-theory-and-methods`
- Output interpretation, plotting, DOS/bands, NBO/Voronoi analysis, or post-processing data products -> `openmx-analysis-and-output`
- Matrix export, embedding OpenMX, helper binaries, or external-code interfaces -> `openmx-api-and-scripting`
- MPI/OpenMP launch shape, `-runtestL*`, or large-node behavior -> `openmx-parallel-hpc`
- Single manual-page leftovers or niche troubleshooting -> `openmx-advanced-topics`

## Escalate only when needed
- Start from topic skill primary references.
- If those references are insufficient, search the topic skill `references/doc_map.md`.
- If documentation still leaves ambiguity, open `references/source_map.md` inside the same topic skill and inspect the suggested source entry points.
- Use targeted symbol search while inspecting source (e.g., `rg -n "<symbol_or_keyword>" source`).
