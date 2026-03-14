# openmx source map: Theory and Methods

Use this map only after the manual/example route is exhausted.

## Fast navigation
- `rg -n "NEGF|Lead|Tran" source/Band_DFT_Col_NEGF.c source/TRAN_DFT.c source/MTRAN_EigenChannel.c`
- `rg -n "Wannier|CDDF|optical|unfold" source/Generate_Wannier.c source/Calc_optical.c source/Unfolding_Bands.c`

## Suggested source entry points
- `source/Band_DFT_Col_NEGF.c` | `Band_DFT_Col_NEGF()` performs the NEGF step-2 device SCF
- `source/TRAN_DFT.c` | `TRAN_DFT()` and related helpers implement transport SCF
- `source/MTRAN_EigenChannel.c` | `MTRAN_EigenChannel()` and `MTRAN_EigenChannel_NC()` implement step-3 eigenchannels
- `source/TRAN_Calc_CurrentDensity.c` | transport current-density accumulation
- `source/Generate_Wannier.c` | `Generate_Wannier()` and `Wannier()` implement MLWF generation
- `source/Calc_optical.c` | optical/CDDF accumulation and output
- `source/Unfolding_Bands.c` | `Unfolding_Bands()` and mapping helpers
- `source/Divide_Conquer.c` | divide-conquer method implementation
- `source/Krylov.c` | Krylov method implementation
