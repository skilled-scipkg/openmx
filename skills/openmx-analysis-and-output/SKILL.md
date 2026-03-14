---
name: openmx-analysis-and-output
description: This skill should be used when users ask about analysis and output in openmx; it prioritizes documentation references and then source inspection only for unresolved details.
---

# openmx: Analysis and Output

## High-Signal Playbook
- Route conditions:
  Use this skill for interpreting OpenMX output files, generating derived analysis files, and running shipped post-processing utilities such as `DosMain`, `kSpin`, `bin2txt`, `intensity_map`, and the BoltzTraP bridge.
  Route ground-state model setup to `openmx-inputs-and-modeling`, NEGF/MLWF/CDDF method setup to `openmx-theory-and-methods`, and `.scfout` developer interfaces to `openmx-api-and-scripting`.
- Triage questions:
  Which artifact do you need: SCF/MD output, DOS/bands, cube/xsf data, NEGF step-3 analysis, NBO/Voronoi charges, or a downstream-tool export?
  Do you already have the prerequisite SCF, NEGF, unfolding, or MLWF run?
  Is there a shipped example with the same output type?
  Do you need a quick visualization file, a text table for plotting, or a regression-style numerical check?
- Canonical workflow:
  1. Start from the relevant manual page and the closest shipped example in `references/doc_map.md`.
  2. Confirm the parent calculation emitted the required artifact before launching any helper tool.
  3. Build the helper executable from `source/` only when needed, then run it from `work/` beside the data files.
  4. Validate the produced files against the manual's expected filenames and the shipped example outputs.
  5. If the file content still disagrees with the documentation, inspect the targeted implementation file from `references/source_map.md`.
- Minimal working example:
```text
Band.dispersion            on
Dos.fileout                on
level.of.fileout           1
Band.Nkpath                5
<Band.kpath
  15 0.0 0.0 0.0  1.0 0.0 0.0  G X
Band.kpath>
```
```text
cd source
make bin2txt intensity_map kSpin BandDispersion
cd ../work
./bin2txt System.bin
./kSpin Au111Surface_BD.dat
./intensity_map sic_c_sp_v.unfold_totup -c 3 -k 0.1 -e 0.1 -l -10 -u 6 > sic-intmap.txt
sh MX_TRAP.sh
```
- Pitfalls/fixes:
  `DosMain`, `BandDispersion`, and `kSpin` are post-processing tools; they depend on files emitted by a completed parent run.
  `OutData.bin.flag on` reduces I/O cost, but you still need `bin2txt.c` to recover human-readable cube/xsf/grid data.
  The `Au111Surface_*.dat` files in `work/` already contain the extra keywords expected by `kSpin`; copy those instead of inventing new post-processing inputs.
  NEGF transmission/current/eigenchannel analysis requires the step-2 transport data to exist first.
  `MX_TRAP.sh` is interactive and should be run inside `work/` after the relevant `.out` file exists.
- Validation checks:
  Band and DOS workflows should create `System.Name.Band`, `System.Name.Dos.val`, and `System.Name.Dos.vec`.
  Real-space output should create the `.cube`, `.xsf`, or binary variants documented in `manual/output-files.md`.
  BoltzTraP conversion should create a directory named after the system containing `.energy`, `.struct`, and `.intrans`.
  NBO and Voronoi analysis should appear in the standard output or `System.Name.out`.
  Unfolding intensity-map generation should create a text mesh file that can be plotted directly with gnuplot.

## Primary documentation references
- `manual/output-files.md`
- `manual/visualization.md`
- `manual/band-calculation.md`
- `manual/band-dispersion.md`
- `manual/density-of-states.md`
- `manual/natural-population-analysis.md`
- `manual/charge-analysis.md`
- `manual/mulliken-charge.md`
- `manual/analysis-of-difference-charge-density-induced-by-the-interaction.md`
- `manual/intensity-map-of-unfolded-spectral-weight.md`
- `manual/output-of-large-sized-files-in-binary-mode.md`
- `manual/analysis-of-memory-usage.md`
- `manual/periodic-system-under-zero-bias.md`
- `manual/interface-with-boltztrap.md`
- `manual/analysis-of-spin-texture-in-the-k-space.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `work/input_example`
- `work/nbo_example`
- `work/unfolding_example`
- `work/negf_example`
- `work/Si_BoltzTraP.dat`
- `work/Au111Surface_BD.dat`
- `work/Au111Surface_FL.dat`
- `work/Au111Surface_GC.dat`
- `work/Au111Surface_MO.dat`

## Test references
- `work/cddf_example`
- `work/input_example`
- `work/negf_example`
- `work/nbo_example`

## Optional deeper inspection
- `source`

## Source entry points for unresolved issues
- `source/OutData.c`
- `source/OutData_Binary.c`
- `source/DosMain.c`
- `source/BandDispersion.c`
- `source/Mulliken_Charge.c`
- `source/Voronoi_Charge.c`
- `source/NBO_Cluster.c`
- `source/NBO_Krylov.c`
- `source/TRAN_Main_Analysis.c`
- `source/MTRAN_EigenChannel.c`
- `source/TRAN_Channel_Output.c`
- `source/intensity_map.c`
- `source/bin2txt.c`
- `source/MX_TRAP.sh`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" source`).
