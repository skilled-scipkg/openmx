---
name: openmx-simulation-workflows
description: This skill should be used when users ask about simulation workflows in openmx; it prioritizes documentation references and then source inspection only for unresolved details.
---

# openmx: Simulation Workflows

## High-Signal Playbook
- Route conditions:
  Use this skill for SCF execution, continuation with restart files, geometry and cell optimization, MD, and NEB.
  Route input-model design to `openmx-inputs-and-modeling`, advanced transport/MLWF/CDDF/unfolding to `openmx-theory-and-methods`, and large-scale launch tuning to `openmx-parallel-hpc`.
- Triage questions:
  Is this fixed-geometry SCF, relaxation, variable-cell optimization, MD, or NEB?
  Is the system metallic or hard to converge?
  Are you restarting an existing job or starting fresh?
  Is the target cluster-like or periodic?
  For NEB, do precursor and product already exist with the same numerical settings?
  Do you need per-step output inspection or only a finished structure/trajectory?
- Canonical workflow:
  1. Start from the closest shipped input in `work/input_example`, `work/geoopt_example`, or `work/cellopt_example`.
  2. Run a fixed-geometry SCF first and confirm the model converges before turning on relaxation or MD.
  3. For continuation or follow-up band/DOS work, keep the same `System.Name` and switch `scf.restart on`.
  4. For geometry optimization, choose an optimizer (`BFGS`, `RF`, `EF`, `DIIS`, or `Opt`) and set `MD.Opt.criterion`.
  5. For variable-cell optimization, use an `OptC*` mode plus stress/cell constraints as needed.
  6. For MD, choose `NVE`, `NVT_VS`, `NVT_NH`, or `NVT_VS4`, then validate the expected ensemble behavior.
  7. For NEB, optimize precursor and product first with the same basis, VPS, cutoff, cell, and electronic temperature, then run `MD.Type NEB`.
  8. Inspect the generated `.out`, `.ene`, `.md`, `.xyz`, and NEB-specific `.neb.opt` / `.neb.ene` files before tightening tolerances.
- Minimal working example:
```text
scf.restart              on
MD.Type                  BFGS
MD.Opt.DIIS.History      3
MD.Opt.StartDIIS         8
MD.maxIter               200
MD.Opt.criterion         1.0e-4
```
```text
MD.Type                  NEB
MD.NEB.Number.Images     8
MD.NEB.Spring.Const      0.1
MD.Opt.DIIS.History      4
MD.Opt.StartDIIS         10
MD.maxIter               100
MD.Opt.criterion         1.0e-4
```
- Pitfalls/fixes:
  Restart calculations require the same `System.Name`; otherwise the `_rst` directory is ignored.
  Hard metallic or magnetic SCF problems often need slower mixing, larger `scf.Mixing.History`, and higher electronic temperature.
  Weakly interacting structures can require many geometry steps; the manual explicitly notes that loosening the force criterion to `5e-4` Hartree/Bohr can be a practical compromise.
  NEB endpoints must share the same unit cell, basis functions, pseudopotentials, cutoff energy, and electronic temperature to avoid inconsistent barriers.
  NEB memory failures on limited MPI ranks are often load-balance problems; use `MD.NEB.Parallel.Number` to group images instead of parallelizing every image at once.
  Variable-cell runs need stress-aware settings, not just the atom-only geometry optimizer.
- Convergence/validation checks:
  In `*.out`, `NormRD` and `Uele` should settle rather than oscillate indefinitely.
  Geometry optimization is converged only when the maximum force falls below `MD.Opt.criterion`.
  Variable-cell optimization should stabilize both forces and stress/enthalpy, not only total energy.
  MD should respect the intended ensemble: conserved energy for NVE, controlled temperature for NVT variants.
  NEB validation comes from the decreasing maximum force in `.neb.opt` and a sensible barrier profile in `.neb.ene`.

## Primary documentation references
- `manual/test-calculation.md`
- `manual/convergence.md`
- `manual/scf-convergence-general.md`
- `manual/restarting-general.md`
- `manual/geometry-optimization.md`
- `manual/variable-cell-optimization.md`
- `manual/variable-cell-optimization-general.md`
- `manual/molecular-dynamics.md`
- `manual/nudged-elastic-band-neb-method.md`
- `manual/how-to-perform.md`
- `manual/examples-and-keywords.md`
- `manual/parallel-calculation.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `work/input_example`
- `work/geoopt_example`
- `work/cellopt_example`

## Test references
- `work/input_example`
- `work/geoopt_example`
- `work/cellopt_example`

## Optional deeper inspection
- `source`

## Source entry points for unresolved issues
- `source/openmx.c`
- `source/Input_std.c`
- `source/Total_Energy.c`
- `source/Stress.c`
- `source/RestartFileDFT.c`
- `source/neb.c`
- `source/neb_run.c`
- `source/Runtest.c`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" source`).
