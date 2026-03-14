---
name: openmx-build-and-install
description: This skill should be used when users ask about build and install in openmx; it prioritizes documentation references and then source inspection only for unresolved details.
---

# openmx: Build and Install

## High-Signal Playbook
- Route conditions:
  Use this skill for compiler/library setup, `source/makefile` edits, MPI/OpenMP variants, `make` targets, and post-install smoke tests.
  Route scheduler/scaling questions to `openmx-parallel-hpc` and developer helper binaries such as `analysis_example` or `example_mpi_spawn` to `openmx-api-and-scripting`.
- Triage questions:
  Which compiler/MPI stack is available?
  Are FFTW3, ScaLAPACK/BLACS, and MKL or equivalent installed?
  Do you need plain MPI or MPI/OpenMP hybrid?
  Is OpenMP unavailable, requiring `-Dnoomp`?
  Do you only need `openmx`, or also helper codes from `make all` or `make jx`?
  Which smoke test do you need: `Methane.dat`, `-runtest`, `-runtestNEGF`, `-runtestWF`, or `-runtestCDDF`?
- Canonical workflow:
  1. Start in `source/` and edit `makefile` so `CC`, `FC`, and `LIB` match the local MPI/compiler/library stack.
  2. Prefer the MPI build path; the manual states the serial version is not supported in OpenMX 3.9.
  3. Add OpenMP flags to both `CC` and `FC` for hybrid builds; add `-Dnoomp` only when OpenMP is unavailable.
  4. Link FFTW3 plus ScaLAPACK/BLACS or MKL; most install failures are link-line problems.
  5. Run `make install`; it copies `openmx` into `work/`. Use `make all` for helper tools and `make jx` when exchange-coupling workflows are needed.
  6. Smoke-test in `work/` with `Methane.dat`, then run the smallest relevant built-in runtest.
  7. Escalate to `openmx-parallel-hpc` if the target job is large enough that `-runtestL`, `-runtestL2`, or `-runtestL3` matters more than install syntax.
- Minimal working example:
```text
cd source
# edit makefile
CC = mpicc -O3 -fopenmp -I/usr/local/fftw3/include -I/$MKLROOT/include
FC = mpif90 -O3 -fopenmp -I/$MKLROOT/include
LIB = -L/usr/local/fftw3/lib -lfftw3 ...

make install
cd ../work
mpirun -np 1 openmx Methane.dat > met.std
mpirun -np 8 openmx -runtest
```
- Pitfalls/fixes:
  Serial OpenMX 3.9 is unsupported; do not route users toward a serial-only build.
  Link errors such as `cannot find -lifcore`, `-lpgf90`, or `-lgfortran` mean the Fortran runtime path must be added explicitly to `LIB`.
  Missing ScaLAPACK/BLACS is the most common failure mode; the docs recommend MKL link lines when possible.
  FFTW3 must be present in both include and library search paths.
  `make install` places `openmx` in `work/`, not `source/`.
  `make all` is for helper/post-processing binaries; it is not required for a minimal SCF run.
  Use `mpicc -compile-info` or `mpicc -help` to discover the wrapped compiler and implied libraries before guessing flags.
- Convergence/validation checks:
  The `openmx` executable exists in `work/` after `make install`.
  `mpirun -np 1 openmx Methane.dat` produces `met.out`, `met.std`, and `met_rst/`.
  The `-runtest` driver writes `runtest.result` in `work/`; acceptable installs match the reference within the last seven digits.
  Use feature-specific checks only when that feature matters: `-runtestNEGF`, `-runtestWF`, `-runtestCDDF`.

## Primary documentation references
- `manual/installation.md`
- `manual/serial-version.md`
- `manual/mpi-version.md`
- `manual/mpi-openmp-version.md`
- `manual/options-for-make.md`
- `manual/tips-for-installation.md`
- `manual/installation-fftw3.md`
- `manual/compilation-of-jx.md`
- `manual/test-calculation.md`
- `manual/automatic-running-test.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `work/input_example`

## Test references
- `work/input_example`
- `work/large_example`
- `work/large2_example`
- `work/large3_example`
- `work/negf_example`
- `work/wf_example`
- `work/cddf_example`

## Optional deeper inspection
- `source`

## Source entry points for unresolved issues
- `source/makefile`
- `source/openmx.c`
- `source/Runtest.c`
- `source/test_mpi.c`
- `source/test_openmp.c`
- `source/example_mpi_spawn.c`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" source`).
