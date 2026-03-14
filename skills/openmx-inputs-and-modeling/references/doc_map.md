# openmx documentation map: Inputs and Modeling

Use these docs before inspecting parser or solver sources.

## Manual entry points
- `manual/input-file.md` | overall input structure and required blocks
- `manual/input-file-keywords.md` | exact keyword spelling and defaults
- `manual/specification-of-a-directory-storing-pao-and-vps-files.md` | `DATA.PATH` and database lookup
- `manual/basis-sets.md` | choosing PAO families and levels
- `manual/basis-sets-general.md` | basis-block structure and conventions
- `manual/pseudopotentials.md` | VPS selection and naming
- `manual/functional.md` | XC, spin, and solver-level functional choices
- `manual/dft-plus-u-methods.md` | DFT+U overview
- `manual/choice-of-dft-plus-u-scheme-simplified-or-general.md` | simplified vs general DFT+U
- `manual/choice-of-the-double-counting.md` | double-counting options
- `manual/convergence.md` | input-level convergence knobs
- `manual/an-example-methane-molecule.md` | smallest fully worked input

## Shipped example roots
- `work/input_example/Methane.dat` | minimal cluster input
- `work/input_example/GaAs.dat` | periodic bulk input
- `work/ml_example/FeO+U.dat` | DFT+U example with existing fixture
- `work/negf_example/Lead-Chain.dat` | transport lead input structure
- `work/unfolding_example/SiC_Primitive.dat` | periodic reference-cell input
