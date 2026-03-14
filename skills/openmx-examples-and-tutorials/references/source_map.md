# openmx source map: Examples and Tutorials

Use this map only after the manual/example route is exhausted.

## Fast navigation
- `rg -n "runtest|maketest|example" source/Runtest.c source/openmx.c`
- `rg -n "NEB|Wannier|CDDF|TRAN|NBO" source/neb.c source/Generate_Wannier.c source/Calc_optical.c source/TRAN_DFT.c source/NBO_Cluster.c`

## Suggested source entry points
- `source/Runtest.c` | `Runtest()` and `run_main()` know the reference example suites
- `source/openmx.c` | user-facing CLI entry used by every example
- `source/neb.c` | NEB example driver
- `source/TRAN_DFT.c` | transport example core
- `source/Generate_Wannier.c` | MLWF example core
- `source/Calc_optical.c` | CDDF example core
- `source/BandDispersion.c` | band/spin-texture example utility
- `source/Set_CoreHoleMatrix.c` | core-hole/XPS example logic
- `source/NBO_Cluster.c` | small-system NBO example logic
- `source/MTRAN_EigenChannel.c` | transport eigenchannel example logic
