---
name: openmx-examples-and-tutorials
description: This skill should be used when users ask about examples and tutorials in openmx; it prioritizes documentation references and then source inspection only for unresolved details.
---

# openmx: Examples and Tutorials

## High-Signal Playbook
- Route conditions:
  Use this skill when the fastest path is to clone the closest shipped example and then hand off to the more specific topic skill.
  Route back to the topic skills once the right example family is identified and the question becomes about build, input design, workflow control, analysis, or theory details.
- Triage questions:
  Which workflow is closest: ground-state SCF, relaxation, NEB, NEGF, MLWF, CDDF, NBO, or post-processing?
  Do you need the smallest possible example, or the closest physics to the target system?
  Are you copying an input block, or reproducing a full multi-step run?
  Which shipped `.out`, `.std`, or reference result file can you compare against immediately?
- Canonical workflow:
  1. Pick the smallest shipped example that exercises the desired feature.
  2. Reuse its directory structure and only change the minimum system-specific blocks at first.
  3. Run the example from `work/` with the same execution pattern shown in the manual.
  4. Compare the generated outputs against the shipped `.out` or reference result files before making the setup more ambitious.
  5. Once the example is selected, switch to the more specific skill for detailed troubleshooting or physics decisions.
- Minimal working example:
```text
cd work
mpirun -np 1 ./openmx input_example/Methane.dat > methane.std
mpirun -np 16 ./openmx C2H4_NEB.dat > c2h4-neb.std
```
```text
cd work/negf_example
mpirun -np 8 ../openmx Lead-Chain.dat > lead-chain.std
mpirun -np 8 ../openmx NEGF-Chain.dat > negf-chain.std
```
- Pitfalls/fixes:
  Start from the closest shipped example file, not from a manual snippet copied in isolation.
  Keep `DATA.PATH` and any relative helper-file paths consistent with the working directory you actually use.
  NEGF, MLWF, and CDDF examples often require a sequence of runs; do not judge them from a single input file alone.
  The root `work/` directory contains several standalone tutorial inputs that are not inside the example subdirectories.
- Validation checks:
  Generated filenames and key sections of `.out` files should match the shipped example outputs.
  Regression-style examples should be comparable to the shipped `runtest*.result*` files in the corresponding example directory.
  For NEB and transport examples, validate the expected intermediate files before moving on to analysis.

## Primary documentation references
- `manual/test-calculation.md`
- `manual/examples-and-keywords.md`
- `manual/examples-of-the-input-files.md`
- `manual/examples-for-generating-mlwfs.md`
- `manual/example-of-test-calculation.md`
- `manual/electric-transport-calculations-examples.md`
- `manual/absolute-binding-energies-of-core-levels-xps-core-level-energies-examples.md`

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
- `work/negf_example`
- `work/wf_example`
- `work/cddf_example`
- `work/unfolding_example`
- `work/nbo_example`
- `work/C2H4_NEB.dat`
- `work/Si8_NEB.dat`
- `work/Si-Wannier90.dat`
- `work/Si_BoltzTraP.dat`

## Test references
- `work/cddf_example`
- `work/input_example`
- `work/negf_example`
- `work/wf_example`
- `work/geoopt_example`
- `work/cellopt_example`

## Optional deeper inspection
- `source`

## Source entry points for unresolved issues
- `source/Runtest.c`
- `source/openmx.c`
- `source/neb.c`
- `source/TRAN_DFT.c`
- `source/Generate_Wannier.c`
- `source/Calc_optical.c`
- `source/BandDispersion.c`
- `source/Set_CoreHoleMatrix.c`
- `source/MTRAN_EigenChannel.c`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" source`).
