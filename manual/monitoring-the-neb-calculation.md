<a id="SECTION000506000000000000000"></a>
## Monitoring the NEB calculation

In the NEB calculation, the standard output will display only that
for the image 1, and those for the other images will not be displayed.
However, there is no guarantee that the SCF iteration converges for
all the images. In order to monitor the SCF convergence for all
the images, temporary files can be checked by users.
In the NEB calculation, an input file is generated for each image,
whose name is '*System.Name*.dat_#', where '#' runs from 0 to MD.NEB.Number.Images+1,
and `system.name' is modified as the original system.name_#.
So, one can check the SCF convergence by monitoring a file 'system.name_#.DFTSCF',
whether it converges or not.

---
