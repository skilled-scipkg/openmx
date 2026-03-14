# openmx source map: Advanced and Specialized Topics

Use this map only after the manual/example route is exhausted.

## Fast navigation
- `rg -n "DFTU|dc\\.Type|Hubbard|Slater" source/Occupation_Number_LDA_U.c`
- `rg -n "Voronoi|Orbital|Zeeman|Generalized\\.Bloch|jx" source/Voronoi_Charge.c source/Orbital_Moment.c source/jx_config.c source/jx.c source/kSpin.c`

## Suggested source entry points
- `source/Occupation_Number_LDA_U.c` | DFT+U occupations and double-counting behavior
- `source/Cluster_DFT_NonCol.c` | non-collinear and spin-aware ground-state path
- `source/Mixing_DM.c` | baseline density-mixing control
- `source/Kerker_Mixing_Rhok.c` | Kerker-family mixing adjustments
- `source/Cluster_DFT_OptOrb.c` | orbital-optimization-specific flow
- `source/Stress.c` | pressure and enthalpy-coupled behavior
- `source/Orbital_Moment.c` | orbital moment and orbital Zeeman handling
- `source/Voronoi_Charge.c` | Voronoi charge analysis
- `source/jx_config.c` | `read_jx_config()` parses the JX config file
- `source/jx.c` | `main()` ties `.scfout` and config parsing into the JX executable
- `source/Band_DFT_Col_NEGF.c` | NEGF step-2 device solver
- `source/TRAN_Calc_OneTransmission.c` | transmission and conductance evaluation
- `source/TRAN_Calc_CurrentDensity.c` | charge/spin current-density evaluation
- `source/kSpin.c` | `main()` plus BandDispersion/FermiLoop/GridCalc/MulPOnly modes
- `source/read_scfout.c` | `.scfout` reader used by several advanced utilities
- `source/Input_std.c` | fallback for niche keyword parsing
