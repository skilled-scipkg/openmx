---
name: openmx-theory-and-methods
description: This skill should be used when users ask about theory and methods in openmx; it prioritizes documentation references and then source inspection only for unresolved details.
---

# openmx: Theory and Methods

## High-Signal Playbook
- Route conditions:
  Use this skill for advanced workflows that sit on top of a converged ground-state model: NEGF, MLWF, optical conductivity/CDDF, unfolding, and related method choices.
  Route plain input syntax to `openmx-inputs-and-modeling`, ordinary SCF/relaxation execution to `openmx-simulation-workflows`, and developer/export interfaces to `openmx-api-and-scripting`.
- Triage questions:
  Which method is intended: NEGF, MLWF, CDDF, unfolding, or another advanced formalism?
  Is there already a converged ground-state or lead calculation to restart from?
  Is the job collinear, non-collinear, or spin-orbit coupled?
  Which example directory is closest to the target system?
  Do you need built-in verification before trusting the method on a new system?
  Are you validating physics from raw outputs, or only trying to generate the expected files?
- Canonical workflow:
  1. Start from the shipped example directory closest to the method: `work/negf_example`, `work/wf_example`, `work/cddf_example`, or `work/unfolding_example`.
  2. For NEGF, run the lead calculations first so `NEGF.filename.hks*` files exist, then run the device with `scf.EigenvalueSolver NEGF`.
  3. For MLWF, converge the parent SCF/band calculation first, then enable `Wannier.Func.Calc` and define windows and projectors.
  4. For optical conductivity, keep the parent SCF/band setup sane, then add `CDDF.start on` plus an explicit optical k-grid and energy window.
  5. For unfolding, run the supercell SCF and then supply `Unfolding.ReferenceVectors` and a complete `Unfolding.Map`.
  6. Before scaling up, use the built-in verification paths: `-runtestNEGF`, `-runtestWF`, or `-runtestCDDF`.
  7. Validate against the method-specific output files, not only the absence of runtime errors.
- Minimal working example:
```text
# lead SCF
NEGF.output_hks           on
NEGF.filename.hks         lead-chain.hks

# device SCF
NEGF.filename.hks.l       lead-chain.hks
NEGF.filename.hks.r       lead-chain.hks
scf.EigenvalueSolver      NEGF
NEGF.tran.Analysis        on
NEGF.tran.Channel         on
```
```text
Wannier.Func.Calc         on
Wannier.Func.Num          8
Wannier.Outer.Window.Bottom  -14.0
Wannier.Outer.Window.Top      11.0
Wannier.Initial.Guess     on
CDDF.start                on
CDDF.Kgrid                10 10 10
```
- Pitfalls/fixes:
  NEGF step 2 depends on step 1 outputs; missing or mismatched `.hks` files are setup errors, not solver bugs.
  `LeftLeadAtoms` and `RightLeadAtoms` in the device input must stay consistent with the lead calculations.
  MLWF runs are much easier to converge with an initial projector guess; the docs recommend using one.
  On MLWF restart, the outer window cannot exceed the window used when the stored overlap matrix was generated.
  Some manual prose pluralizes the CDDF example directory; in this checkout the usable path is `work/cddf_example`.
  Unfolding requires a complete atom mapping for the supercell; missing or inconsistent group labels invalidate the spectral weights.
  CDDF validation is looser than SCF/NEGF/MLWF: the built-in threshold is a dielectric-function difference below `0.1`, not last-seven-digit agreement.
- Convergence/validation checks:
  The `-runtestNEGF` driver should write `runtestNEGF.result` in `work/` with lead/device energy-force-current differences within the last seven digits.
  The `-runtestWF` driver should write `runtestWF.result` in `work/` with spread and `Omega` differences within the last seven digits.
  The `-runtestCDDF` driver should write `runtestCDDF.result` in `work/` with the documented `0.1` tolerance or better.
  MLWF convergence is signaled by the spread-function monitor and files such as `.Wannier_Band`, `.mlwf*`, `.mmn`, `.amn`, `.eigen`, and `.HWR`.
  Unfolding should emit `.unfold_tot*`, `.unfold_orb*`, and plot-example files that are consistent with the reference primitive-cell bands.

## Primary documentation references
- `manual/electric-transport-calculations.md`
- `manual/automatic-running-test-of-negf.md`
- `manual/maximally-localized-wannier-function.md`
- `manual/automatic-running-test-of-mlwf.md`
- `manual/optical-conductivity-and-dielectric-function.md`
- `manual/optical-conductivity-and-dielectric-function-automatic-running-test.md`
- `manual/unfolding-of-band-structures.md`
- `manual/dft-plus-u-methods.md`
- `manual/divide-conquer-method.md`
- `manual/krylov-subspace-method.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `work/negf_example`
- `work/wf_example`
- `work/cddf_example`
- `work/unfolding_example`

## Test references
- `work/cddf_example`
- `work/negf_example`
- `work/wf_example`

## Optional deeper inspection
- `source`

## Source entry points for unresolved issues
- `source/Band_DFT_Col_NEGF.c`
- `source/TRAN_DFT.c`
- `source/MTRAN_EigenChannel.c`
- `source/TRAN_Calc_CurrentDensity.c`
- `source/Generate_Wannier.c`
- `source/Calc_optical.c`
- `source/Unfolding_Bands.c`
- `source/Divide_Conquer.c`
- `source/Krylov.c`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" source`).
