<a id="SECTION000507000000000000000"></a>
## Parallel calculation

In the NEB calculation, the setting for the parallelization will
be automatically done depending on the number of processes and threads.
However, it would be better to provide a proper number of processes for
the MPI parallelization which can be divisible by the number of images
given by 'MD.NEB.Number.Images', in order to achieve a good load balance
in the MPI parallelization. It is noted that the number of processes for the MPI
parallelization can exceed the number of atoms.
The hybrid parallelization by MPI/OpenMP is also supported.

Although the default parallelization scheme works well in most cases,
a memory shortage can be a serious problem when a small number of the MPI
processes is used for large-scale systems. In the default MPI parallelization,
the images are preferentially parallelized at first. When the number of MPI processes exceeds
the number of images, the calculation of each image starts to be parallelized,
where the memory usage starts to be parallelized as well.
In this case, users may encounter a segmentation fault due to the memory shortage
if many CPU cores are not available. To avoid such a situation, the following
keyword is available.

```text

  MD.NEB.Parallel.Number    3
```

In this example, the calculations of every three images are parallelized at once where
the MPI processes are classified to three groups and utilized for the parallelization
of each image among the three images. In order to complete the calculations of all the images,
the grouped calculations are repeated by floor[(the number of images)/(MD.NEB.Parallel.Number)] times.
The scheme may be useful for the NEB calculation of a large-scale system.
If the keyword is not specified in your input file, the default parallelization scheme is employed.
