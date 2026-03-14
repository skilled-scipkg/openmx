# openmx source map: Inputs and Modeling

Use this map only after the manual/example route is exhausted.

## Fast navigation
- `rg -n "DATA.PATH|Definition.of.Atomic.Species|scf\\.XcType|scf\\.SpinPolarization|scf\\.Hubbard\\.U" source/Input_std.c`
- `rg -n "DFTU|dc\\.Type|Hubbard" source/Occupation_Number_LDA_U.c source/SetPara_DFT.c`

## Suggested source entry points
- `source/readfile.c` | low-level file reader used before keyword dispatch
- `source/Input_std.c` | keyword parser and block dispatch for the main input file
- `source/openmx_common.h` | shared parsed-state variables and global switches
- `source/SetPara_DFT.c` | translates parsed input into solver settings
- `source/Occupation_Number_LDA_U.c` | DFT+U occupations and double-counting behavior
- `source/Cluster_DFT_Col.c` | cluster workflow after input parsing
- `source/Cluster_DFT_NonCol.c` | non-collinear input consequences
- `source/Band_DFT_Col.c` | periodic/band workflow after input parsing
- `source/TRAN_Input_std.c` | transport-specific input parsing
- `source/RestartFileDFT.c` | restart interactions with modified inputs
