# openmx source map: Simulation Workflows

Use this map only after the manual/example route is exhausted.

## Fast navigation
- `rg -n "scf\\.restart|MD\\.Type|MD\\.Opt|MD\\.NEB" source/Input_std.c`
- `rg -n "NEB|restart|Geometry_Opt|NVT_|Cell_Opt" source/MD_pac.c source/neb.c source/RestartFileDFT.c`

## Suggested source entry points
- `source/openmx.c` | `main()` dispatches normal runs and special runtime modes
- `source/Input_std.c` | parses restart, MD, optimizer, and NEB keywords
- `source/MD_pac.c` | `MD_pac()` plus geometry, MD, and cell-optimization integrators
- `source/Total_Energy.c` | SCF and relaxation diagnostics
- `source/Stress.c` | stress tensor and cell-optimization behavior
- `source/RestartFileDFT.c` | restart-file read/write path
- `source/neb.c` | `neb()`, generated input files, and `.neb.*` outputs
- `source/neb_run.c` | per-image runtime path inside NEB
- `source/Runtest.c` | harness for the shipped workflow examples
