# openmx source map: Analysis and Output

Use this map only after the manual/example route is exhausted.

## Fast navigation
- `rg -n "cube|xsf|Band|Dos|OutData" source/OutData.c source/OutData_Binary.c source/DosMain.c`
- `rg -n "Voronoi|Mulliken|Population|Transmission|Channel" source/Mulliken_Charge.c source/Voronoi_Charge.c source/TRAN_Main_Analysis.c source/MTRAN_EigenChannel.c`

## Suggested source entry points
- `source/OutData.c` | `OutData()` plus cube/xsf/text output helpers
- `source/OutData_Binary.c` | `OutData_Binary()` for binary output mode
- `source/DosMain.c` | DOS and projected-DOS post-processing
- `source/BandDispersion.c` | standalone band-dispersion utility main program
- `source/Mulliken_Charge.c` | Mulliken charge and magnetic-moment analysis
- `source/Voronoi_Charge.c` | Voronoi charge integration
- `source/NBO_Cluster.c` | `Calc_NAO_Cluster()` for cluster-style natural population analysis
- `source/NBO_Krylov.c` | `Calc_NAO_Krylov()` and `Calc_NBO()` for large-system NBO analysis
- `source/TRAN_Main_Analysis.c` | transmission/current/conductance post-processing
- `source/MTRAN_EigenChannel.c` | eigenchannel calculation and output
- `source/TRAN_Channel_Output.c` | eigenchannel LCAO and cube-file writers
- `source/intensity_map.c` | standalone unfolded-spectral-weight intensity-map utility
- `source/bin2txt.c` | standalone converter for binary cube/xsf/grid output
- `source/MX_TRAP.sh` | BoltzTraP bridge script
