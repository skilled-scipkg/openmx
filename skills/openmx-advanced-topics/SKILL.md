---
name: openmx-advanced-topics
description: This skill should be used when users ask about advanced and specialized topics in openmx; it prioritizes documentation references and then source inspection only for unresolved details.
---

# openmx: Advanced and Specialized Topics

## High-Signal Playbook
- Route conditions:
  Use this skill for narrow manual topics that no longer deserve standalone skills: DFT+U variants, non-collinear extras, JX config, Voronoi/Zeeman/orbital-moment analysis, NEGF step-2 and transmission details, known problems, and other specialist add-ons.
  Route broad build/input/run questions back to the enriched core skills once the request stops being niche.
- Triage questions:
  Which exact micro-topic is it?
  Is the user asking for a keyword block, an example directory, or implementation behavior?
  Does the topic depend on an existing SCF/NEGF/MLWF run?
  Is the question really about a known problem or about a base workflow that belongs elsewhere?
  Is a single source file enough, or is the manual answer already complete?
- Canonical workflow:
  1. Identify the exact collapsed route in the list below and open that manual page first.
  2. Reuse the smallest documented keyword block or shipped example rather than re-explaining the whole package.
  3. If behavior remains unclear, inspect the targeted source entry point from `references/source_map.md`.
  4. If the topic expands into a full build/input/run workflow, switch back to the corresponding core skill.
  5. Keep answers path-heavy and specific; this skill exists to avoid opening many docs.
- Minimal working example:
```text
scf.Hubbard.U              on
scf.SpinPolarization       on
scf.DFTU.Type              2
scf.dc.Type                cFLL
```
```text
Voronoi.charge             on
scf.NC.Mag.Field.Spin      100.0
MD.applied.pressure        10.0
```
- Pitfalls/fixes:
  DFT+U requires `scf.SpinPolarization on` or `nc`; leaving spin off is an invalid setup.
  Dense metallic/magnetic systems can hit both known-problem classes at once: overcomplete basis and slow SCF mixing.
  `cFLL` and `cAMF` in the general DFT+U form change how spin-density XC is treated during SCF; do not compare them casually with simplified Dudarev settings.
  Transmission/current-density questions still depend on a successful NEGF step-2 device calculation.
  JX config issues usually come from the config file, not from the SCF input itself; inspect `jx_config.c` only after reading the doc.
  Zeeman and orbital-moment analysis are meaningful only in the spin-aware workflows that generate the relevant terms in `*.out`.
- Convergence/validation checks:
  DFT+U runs should print the `DFT+U Type and DC` banner before the SCF loop and occupations in `*.out`.
  Voronoi analysis should emit `*.VC`; orbital-moment analysis should emit `*.OM`.
  NEGF current-density workflows should produce the documented `.xsf` or transmission analysis outputs.
  Known-problem fixes should change observable behavior, not only suppress warnings.

## Collapsed topic routes
- DFT+U scheme choice -> `manual/choice-of-dft-plus-u-scheme-simplified-or-general.md`; source: `source/Occupation_Number_LDA_U.c`
- Double-counting choice -> `manual/choice-of-the-double-counting.md`; source: `source/Occupation_Number_LDA_U.c`
- Conventional pseudopotentials -> `manual/conventional-pseudopotentials.md`; source: `source/Input_std.c`
- Electric transport overview -> `manual/electric-transport-calculations-general.md`; source: `source/Band_DFT_Col_NEGF.c`
- Many-k-point jobs -> `manual/for-calculations-with-lots-of-k-points.md`; source: `source/Cluster_DFT_Col.c`
- LCAO coefficients -> `manual/lcao-coefficients.md`; source: `source/read_scfout.c`
- Non-collinear DFT -> `manual/non-collinear-dft.md`; source: `source/Cluster_DFT_NonCol.c`
- On-the-fly SCF mixing -> `manual/on-the-fly-control-of-scf-mixing-parameters.md`; source: `source/Mixing_DM.c`, `source/Kerker_Mixing_Rhok.c`
- Optimization of enthalpy -> `manual/optimization-of-enthalpy.md`; source: `source/Stress.c`
- Orbital magnetic moment -> `manual/orbital-magnetic-moment.md`; source: `source/Orbital_Moment.c`
- Orbital optimization -> `manual/orbital-optimization.md`; source: `source/Cluster_DFT_OptOrb.c`
- JX config preparation -> `manual/preparation-of-config-file-for-jx.md`; source: `source/jx_config.c`
- Real-space charge/spin current density -> `manual/real-space-charge-spin-current-density.md`; source: `source/TRAN_Calc_CurrentDensity.c`
- Spin-spiral calculations -> `manual/spin-spiral-calculations.md`; source: `source/kSpin.c`
- NEGF step 2 -> `manual/step-2-the-negf-calculation.md`; source: `source/Band_DFT_Col_NEGF.c`
- Transmission/current/conductance -> `manual/transmission-total-current-and-conductance.md`; source: `source/TRAN_Calc_OneTransmission.c`
- Known problems -> `manual/known-problems.md`; source: `source/Input_std.c`, `source/Mixing_DM.c`
- Voronoi charge -> `manual/voronoi-charge.md`; source: `source/Voronoi_Charge.c`
- Zeeman term for orbital moment -> `manual/zeeman-term-for-orbital-magnetic-moment.md`; source: `source/Orbital_Moment.c`
- Zeeman term for spin moment -> `manual/zeeman-term-for-spin-magnetic-moment.md`; source: `source/kSpin.c`

## Primary documentation references
- `manual/index.md`
- `manual/README.md`
- `manual/user-defined-initial-path.md`
- `manual/stm-image-by-the-tersoff-hamann-scheme.md`
- `manual/step-1-the-calculations-for-leads.md`
- `manual/fixing-the-relative-position-of-regular-grid.md`
- `manual/energy-vs-lattice-constant.md`
- `manual/ef-bfgs-rf-and-diis-optimizations.md`
- `manual/converting-the-file-format-md2axsf.md`
- `manual/constraint-dft-for-non-collinear-spin-orientation.md`
- `manual/virtual-atom-with-fractional-nuclear-charge.md`
- `manual/varying-the-ratio-of-two-slater-integrals-f-4-f-2.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `work`
- `work/input_example`
- `work/negf_example`
- `work/unfolding_example`

## Test references
- `work/input_example`
- `work/large_example`
- `work/large2_example`
- `work/large3_example`
- `work/negf_example`
- `work/wf_example`
- `work/cddf_example`

## Optional deeper inspection
- `source`

## Source entry points for unresolved issues
- `source/Occupation_Number_LDA_U.c`
- `source/Cluster_DFT_NonCol.c`
- `source/Mixing_DM.c`
- `source/Kerker_Mixing_Rhok.c`
- `source/Orbital_Moment.c`
- `source/Voronoi_Charge.c`
- `source/jx_config.c`
- `source/TRAN_Calc_CurrentDensity.c`
- `source/Band_DFT_Col_NEGF.c`
- `source/TRAN_Calc_OneTransmission.c`
- `source/kSpin.c`
- `source/read_scfout.c`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" source`).
