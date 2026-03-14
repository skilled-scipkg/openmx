<a id="SECTION000504000000000000000"></a>
## Restarting the NEB calculation

It often happens that the convergence is not achieved even after the maximum
optimization step. In such a case, one has to continue the optimization as
a new job starting from the last optimization step in the previous job.
A file '*System.Name*.dat#' is generated after every optimization step. The file contains
a series of atomic coordinates for images in the last step.
One can restart the optimization using a file '*System.Name*.dat#'.

---
