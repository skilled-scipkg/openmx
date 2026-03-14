# openmx documentation map: Simulation Workflows

Use these docs before opening runtime sources.

## Manual entry points
- `manual/test-calculation.md` | smallest fixed-geometry SCF run
- `manual/convergence.md` | SCF convergence control
- `manual/restarting-general.md` | restart prerequisites and behavior
- `manual/input-file-for-the-restart-calculation.md` | restart-specific input handling
- `manual/geometry-optimization.md` | atomic relaxation modes
- `manual/variable-cell-optimization.md` | cell optimization controls
- `manual/molecular-dynamics.md` | MD modes and expected outputs
- `manual/nudged-elastic-band-neb-method.md` | NEB workflow
- `manual/examples-and-keywords.md` | NEB keywords and expected files
- `manual/parallel-calculation.md` | NEB image grouping for memory/load balance

## Shipped example roots
- `work/input_example/Methane.dat` | fixed-geometry SCF baseline
- `work/geoopt_example/Methane_BFGS.dat` | small geometry-optimization input
- `work/cellopt_example/Cdia-OptC1.dat` | variable-cell optimization input
- `work/C2H4_NEB.dat` | NEB tutorial input
- `work/Si8_NEB.dat` | second NEB tutorial input

## Validation fixtures
- `work/geoopt_example/Methane_BFGS.out` | reference relaxation output shape
- `work/cellopt_example/Cdia-OptC1.out` | reference cell-optimization output shape
