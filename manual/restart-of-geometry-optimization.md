<a id="SECTION000165000000000000000"></a>
## Restart of geometry optimization

If the first trial for geometry optimization does not reach a convergent result,
one can restart the geometry optimization using an input file '*System.Name*.dat#' which
is generated at every geometry optimization step for the restart calculation
with the final structure. In such a case, it is better to restart the optimization
with the approximate Hessian matrix calculated in the first trial to accelerate
the convergence.
In OpenMX Ver. 3.9, the approximate Hessian matrix is also saved every geometry
optimization step, and is reused when the restart is performed by '*System.Name*.dat#'.
Thus, even if the geometry optimization is intermittently repeated by subsequent job submission,
the number of iterations for the geometry optimization step is the same as that in the single
submission. The functionality may be useful when users optimize large-scale systems using
computational systems in common use for which the wall time is set for each job.

---
