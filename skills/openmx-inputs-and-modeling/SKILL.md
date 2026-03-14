---
name: openmx-inputs-and-modeling
description: This skill should be used when users ask about inputs and modeling in openmx; it prioritizes documentation references and then source inspection only for unresolved details.
---

# openmx: Inputs and Modeling

## High-Signal Playbook
- Route conditions:
  Use this skill for input syntax, `DATA.PATH`, species/basis/VPS setup, cell and coordinate blocks, XC/spin choices, and DFT+U decisions.
  Route SCF/restart/relaxation execution details to `openmx-simulation-workflows`, and route MLWF/NEGF/CDDF/unfolding specifics to `openmx-theory-and-methods`.
- Triage questions:
  Is the system a cluster, periodic bulk, slab, or transport device?
  Which database and `DATA.PATH` are available?
  Which basis level and pseudopotentials are acceptable for cost vs accuracy?
  Is the run non-magnetic, collinear spin, or non-collinear?
  Do you need plain LDA/GGA or DFT+U?
  What k-point density and cutoff are acceptable?
  Is the target insulating or metallic?
- Canonical workflow:
  1. Start from the closest shipped `.dat` file in `work/input_example` or another example directory.
  2. Set `System.Name`, `System.CurrrentDirectory`, and `DATA.PATH` first so outputs and PAO/VPS lookup are deterministic.
  3. Define species with explicit PAO and VPS names in `<Definition.of.Atomic.Species>`.
  4. Define coordinates and, for periodic cases, `Atoms.UnitVectors`; for clusters, the cell can be omitted and OpenMX can pad automatically.
  5. Choose `scf.XcType`, `scf.SpinPolarization`, `scf.EigenvalueSolver`, `scf.Kgrid`, `scf.energycutoff`, and mixing controls.
  6. For DFT+U, enable `scf.Hubbard.U`, choose simplified vs general (`scf.DFTU.Type`), then add `U`, `J`, and `scf.dc.Type` only when the general form is intended.
  7. Run a cheap SCF first, inspect `.out`, then tighten basis, k-grid, and convergence knobs only after the model is behaving sensibly.
- Minimal working example:
```text
System.CurrrentDirectory   ./
System.Name                Methane
DATA.PATH                  ../DFT_DATA19
Species.Number             2
<Definition.of.Atomic.Species
 H   H5.0-s1      H_PBE19
 C   C5.0-s1p1    C_PBE19
Definition.of.Atomic.Species>
Atoms.Number               5
Atoms.SpeciesAndCoordinates.Unit  Ang
<Atoms.SpeciesAndCoordinates
 1 C  0.000000  0.000000  0.000000  2.0 2.0
 2 H -0.889981 -0.629312  0.000000  0.5 0.5
Atoms.SpeciesAndCoordinates>
scf.XcType                 GGA-PBE
scf.SpinPolarization       off
scf.energycutoff           120.0
scf.Kgrid                  1 1 1
scf.Mixing.Type            rmm-diis
scf.criterion              1.0e-10
```
```text
scf.Hubbard.U              on
scf.SpinPolarization       on
scf.DFTU.Type              2
scf.dc.Type                cFLL
```
- Pitfalls/fixes:
  `DATA.PATH` must point to `DFT_DATA19`; wrong paths fail before physics becomes relevant.
  The initial up/down charges in `Atoms.SpeciesAndCoordinates` must sum to the valence electron count in the chosen `.vps`.
  Dense fcc/hcp/bcc systems can show overcomplete-basis pathologies; reduce the basis level or switch `scf.ProExpn.VNA off` and raise the grid cutoff.
  `scf.SpinPolarization` must be `on` or `nc` for any DFT+U calculation.
  `scf.DFTU.Type=1` reads only `U`; `scf.DFTU.Type=2` is the form that uses `J` and explicit `scf.dc.Type`.
  Metallic or small-gap systems usually need Kerker-family mixing, larger `scf.Mixing.History`, and a higher `scf.ElectronicTemperature`.
  MLWF, CDDF, and NEGF keywords are not substitutes for a sane ground-state input; finish the base model first.
- Convergence/validation checks:
  `scf.energycutoff` of 150-200 Ry is the usual starting range, but subtle energy differences can require more than 300 Ry.
  Converge basis level, k-grid, and smearing/electronic temperature against the observable you actually care about.
  For charge sloshing, try `scf.Mixing.History 30-50`, `scf.Mixing.StartPulay 10-30`, `scf.Mixing.EveryPulay 1`, and tune `scf.Kerker.factor`.
  Validate that total energy, forces, and occupations are stable under small basis/k-grid changes before moving to expensive workflows.

## Primary documentation references
- `manual/input-file.md`
- `manual/input-file-keywords.md`
- `manual/basis-sets.md`
- `manual/basis-sets-general.md`
- `manual/pseudopotentials.md`
- `manual/conventional-pseudopotentials.md`
- `manual/functional.md`
- `manual/dft-plus-u-methods.md`
- `manual/choice-of-dft-plus-u-scheme-simplified-or-general.md`
- `manual/choice-of-the-double-counting.md`
- `manual/convergence.md`
- `manual/scf-convergence-general.md`
- `manual/an-example-methane-molecule.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `work/input_example`
- `work/wf_example`

## Test references
- `work/input_example`

## Optional deeper inspection
- `source`

## Source entry points for unresolved issues
- `source/Input_std.c`
- `source/openmx_common.h`
- `source/SetPara_DFT.c`
- `source/Occupation_Number_LDA_U.c`
- `source/Cluster_DFT_Col.c`
- `source/Cluster_DFT_NonCol.c`
- `source/Band_DFT_Col.c`
- `source/Band_DFT_NonCol.c`
- `source/RestartFileDFT.c`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" source`).
