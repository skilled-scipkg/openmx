# openmx documentation map: Theory and Methods

Use these docs before inspecting advanced-method sources.

## Manual entry points
- `manual/electric-transport-calculations.md` | end-to-end NEGF workflow
- `manual/step-1-the-calculations-for-leads.md` | NEGF lead setup
- `manual/step-2-the-negf-calculation.md` | NEGF device setup
- `manual/step-3-the-transmission-current-density-and-eigenchannel.md` | NEGF post-analysis routes
- `manual/automatic-running-test-of-negf.md` | NEGF verification path
- `manual/maximally-localized-wannier-function.md` | MLWF workflow
- `manual/maximally-localized-wannier-function-output-files.md` | MLWF output files and restart caveats
- `manual/interface-with-wannier90.md` | Wannier90 handoff
- `manual/automatic-running-test-of-mlwf.md` | MLWF verification path
- `manual/optical-conductivity-and-dielectric-function.md` | CDDF workflow
- `manual/optical-conductivity-and-dielectric-function-automatic-running-test.md` | CDDF verification path
- `manual/unfolding-of-band-structures.md` | unfolding workflow
- `manual/divide-conquer-method.md` | divide-conquer method overview
- `manual/krylov-subspace-method.md` | Krylov method overview

## Shipped example roots
- `work/negf_example/Lead-Chain.dat` | smallest NEGF lead input
- `work/negf_example/NEGF-Chain.dat` | smallest NEGF device input
- `work/wf_example/Si.dat` | compact MLWF example
- `work/cddf_example/Si2_k10x10x10.dat` | compact CDDF example
- `work/unfolding_example/SiC_C_SP_V.dat` | unfolding example with spectral-weight post-processing
- `work/Si-Wannier90.dat` | direct interface-to-Wannier90 input

## Validation fixtures
- `work/negf_example/runtestNEGF.result` | NEGF regression reference
- `work/cddf_example/runtestCDDF.result` | CDDF regression reference
- `work/wf_example/Si.out` | MLWF output shape reference
