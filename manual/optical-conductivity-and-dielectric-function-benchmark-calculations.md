<a id="SECTION000604000000000000000"></a>
## Benchmark calculations

A couple of examples as benchmark calculations are shown below:

**Si**

The real part of dielectric function of Si bulk is shown for a series of k-grids in Fig. [81](optical-conductivity-and-dielectric-function-benchmark-calculations.md#fig:CDDF-Fig2).
We see that as increasing k-grid from
$10\times 10\times 10$ to
$100\times 100\times 100$,
the real part of dielectric function is getting converged.
It is found that we need to have a fine grid for the k-points to obtain a well converged result.
In Tables [14](optical-conductivity-and-dielectric-function-benchmark-calculations.md#table:CDDF-Table1) and [15](optical-conductivity-and-dielectric-function-benchmark-calculations.md#table:CDDF-Table2), we show the computational time and parallel efficiency
in the calculation of the conductivity and dielectric function for supercells of Si bulk.
The results suggest that it might be possible to treat systems including 1000 atoms if 1000 CPU cores are available.

<a id="fig:CDDF-Fig2"></a>
<a id="5287"></a>
| ![\includegraphics[width=17.0cm]{CDDF-Fig2.eps}](assets/img594.png) |
| --- |

<a id="table:CDDF-Table1"></a>
<a id="5297"></a>
|  | # of Si atoms | Supercell | Diagonalization | k-Grid | Total time (s)

(CPUs=128) | Total time (s)

(CPUs=256) | Total time (s)

(CPUs=512) | Total time (s)

(CPUs=1024) | Total time (s)

(CPUs=2048) |  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|  | Total time (s) |  |  |  |  |  |  |  |  |  |
|  | (CPUs=128) |  |  |  |  |  |  |  |  |  |
|  | Total time (s) |  |  |  |  |  |  |  |  |  |
|  | (CPUs=256) |  |  |  |  |  |  |  |  |  |
|  | Total time (s) |  |  |  |  |  |  |  |  |  |
|  | (CPUs=512) |  |  |  |  |  |  |  |  |  |
|  | Total time (s) |  |  |  |  |  |  |  |  |  |
|  | (CPUs=1024) |  |  |  |  |  |  |  |  |  |
|  | Total time (s) |  |  |  |  |  |  |  |  |  |
|  | (CPUs=2048) |  |  |  |  |  |  |  |  |  |
|  | 512 atoms | 4x4x4 | Cluster | 1x1x1 | 3367.16826 | 1755.60797 | 919.21912 | 464.27761 | 253.32210 |  |
|  |  | 4x4x4 | ScaLAPACK | 2x1x1 | 6819.30193 | 3499.51872 | 1838.64406 | 948.87978 | 513.79250 |  |
|  |  | 4x4x4 | Band | 2x2x2 | 15300.58350 | 10217.17765 | 5953.19907 | 3518.84650 | 1747.20171 |  |
|  | 1000 atoms | 5x5x5 | Cluster | 1x1x1 |  |  | 6900.35370 | 3511.85143 | 1778.33693 |  |
|  |  | 5x5x5 | ScaLAPACK | 2x1x1 |  |  | 12994.17818 | 6817.43990 | 3460.76787 |  |
|  |  | 5x5x5 | Band | 2x2x2 |  |  | 43676.20392 | 26055.12739 | 13318.14587 |  |

<a id="table:CDDF-Table2"></a>
<a id="5336"></a>
|  | # of CPUs | Total time of calculating

conductivity and dielectric function (s) | Ratio of

total time by # of CPUs

to total time by 128 CPUs |  |
| --- | --- | --- | --- | --- |
|  | Total time of calculating |  |  |  |
|  | conductivity and dielectric function (s) |  |  |  |
|  | Ratio of |  |  |  |
|  | total time by # of CPUs |  |  |  |
|  | to total time by 128 CPUs |  |  |  |
|  | 128 | 3367.16826 | 1.000 |  |
|  | 256 | 1755.60797 | 1.918 |  |
|  | 512 | 919.21912 | 3.663 |  |
|  | 1024 | 464.27761 | 7.252 |  |
|  | 2048 | 253.32210 | 13.292 |  |

**$\beta $-PVDF**

The real part of dielectric function of $\beta $-PVDF (polyvinylidene fluoride) is shown for a series of k-grids
in Fig. [82](optical-conductivity-and-dielectric-function-benchmark-calculations.md#fig:CDDF-Fig3). We see that the k-grid of
$6\times 9\times 21$ is required to get the convergent result.
In Tables [16](optical-conductivity-and-dielectric-function-benchmark-calculations.md#table:CDDF-Table3) and [17](optical-conductivity-and-dielectric-function-benchmark-calculations.md#table:CDDF-Table4), we show the computational time and parallel efficiency
in the calculation of the conductivity and dielectric function for supercells of $\beta $-PVDF.
It is confirmed that the parallel efficiency is reasonably good, and the elapsed time is less than one hour when
the CPU cores of 256 are used. In Fig. [83](optical-conductivity-and-dielectric-function-benchmark-calculations.md#fig:CDDF-Fig4), we show the $xx$, $yy$, and $zz$ components of
real part of dielectric function of $\beta $-PVDF for your reference.

<a id="fig:CDDF-Fig3"></a>
<a id="5428"></a>
| ![\includegraphics[width=14.0cm]{CDDF-Fig3.eps}](assets/img596.png) |
| --- |

<a id="table:CDDF-Table3"></a>
<a id="5363"></a>
|  | Diagonalization | k-Grid | Total time (s)

(CPUs=128) | Total time (s)

(CPUs=256) | Total time (s)

(CPUs=512) | Total time (s)

(CPUs=1024) | Total time (s)

(CPUs=2048) |  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
|  | Total time (s) |  |  |  |  |  |  |  |
|  | (CPUs=128) |  |  |  |  |  |  |  |
|  | Total time (s) |  |  |  |  |  |  |  |
|  | (CPUs=256) |  |  |  |  |  |  |  |
|  | Total time (s) |  |  |  |  |  |  |  |
|  | (CPUs=512) |  |  |  |  |  |  |  |
|  | Total time (s) |  |  |  |  |  |  |  |
|  | (CPUs=1024) |  |  |  |  |  |  |  |
|  | Total time (s) |  |  |  |  |  |  |  |
|  | (CPUs=2048) |  |  |  |  |  |  |  |
|  | Cluster | 1x1x1 | 4215.67238 | 2086.76841 | 1061.06835 | 565.92209 | 329.42010 |  |
|  | ScaLAPACK | 1x1x2 | 3330.66855 | 1711.98413 | 877.61705 | 599.73266 | 330.11080 |  |
|  | Band | 2x2x2 | 12854.63816 | 7244.26768 | 3591.33618 | 1866.03405 | 998.07756 |  |

<a id="table:CDDF-Table4"></a>
<a id="5402"></a>
|  | # of CPUs | Total time of calculating

conductivity and dielectric function (s) | Ratio of

total time by # of CPUs

to total time by 128 CPUs |  |
| --- | --- | --- | --- | --- |
|  | Total time of calculating |  |  |  |
|  | conductivity and dielectric function (s) |  |  |  |
|  | Ratio of |  |  |  |
|  | total time by # of CPUs |  |  |  |
|  | to total time by 128 CPUs |  |  |  |
|  | 128 | 4215.67238 | 1.000 |  |
|  | 256 | 2086.76841 | 2.020 |  |
|  | 512 | 1061.06835 | 3.973 |  |
|  | 1024 | 565.92209 | 7.449 |  |
|  | 2048 | 329.42010 | 12.797 |  |

<a id="fig:CDDF-Fig4"></a>
<a id="5429"></a>
| ![\includegraphics[width=14.0cm]{CDDF-Fig4.eps}](assets/img597.png) |
| --- |

**VO$_2$ in the R phase**

The real and imaginary parts of dielectric function of VO$_2$ in the R phase are shown for a series of k-grids
in Fig. [84](optical-conductivity-and-dielectric-function-benchmark-calculations.md#fig:CDDF-Fig5). We see that the k-grid of
$16\times 16\times 16$ is required to get the convergent result.
Tables [18](optical-conductivity-and-dielectric-function-benchmark-calculations.md#table:CDDF-Table5) and [19](optical-conductivity-and-dielectric-function-benchmark-calculations.md#table:CDDF-Table6) show the computational time and parallel efficiency
in the calculation of the conductivity and dielectric function for supercells of VO$_2$ in the R phase.
It is confirmed that the parallel efficiency is reasonably good, allowing us to treat large-scale systems
in an elapsed time of 1 hour.

<a id="fig:CDDF-Fig5"></a>
<a id="5440"></a>
| ![\includegraphics[width=17.0cm]{CDDF-Fig5.eps}](assets/img599.png) |
| --- |

<a id="table:CDDF-Table5"></a>
<a id="5445"></a>
|  | Diagonalization | k-Grid | Total time (s)

(CPUs=128) | Total time (s)

(CPUs=256) | Total time (s)

(CPUs=512) | Total time (s)

(CPUs=1024) | Total time (s)

(CPUs=2048) |  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
|  | Total time (s) |  |  |  |  |  |  |  |
|  | (CPUs=128) |  |  |  |  |  |  |  |
|  | Total time (s) |  |  |  |  |  |  |  |
|  | (CPUs=256) |  |  |  |  |  |  |  |
|  | Total time (s) |  |  |  |  |  |  |  |
|  | (CPUs=512) |  |  |  |  |  |  |  |
|  | Total time (s) |  |  |  |  |  |  |  |
|  | (CPUs=1024) |  |  |  |  |  |  |  |
|  | Total time (s) |  |  |  |  |  |  |  |
|  | (CPUs=2048) |  |  |  |  |  |  |  |
|  | Cluster | 1x1x1 | 5328.56778 | 2719.77511 | 1382.56556 | 704.32679 | 360.64294 |  |
|  | ScaLAPACK | 1x1x2 | 5276.74287 | 2755.58509 | 1395.48266 | 718.42770 | 368.24621 |  |
|  | Band | 2x2x2 | 21031.96431 | 10686.37446 | 5586.12815 | 2781.05698 | 1431.91243 |  |

<a id="table:CDDF-Table6"></a>
<a id="5484"></a>
|  | # of CPUs | Total time of calculating

conductivity and dielectric function (s) | Ratio of

total time by # of CPUs

to total time by 128 CPUs |  |
| --- | --- | --- | --- | --- |
|  | Total time of calculating |  |  |  |
|  | conductivity and dielectric function (s) |  |  |  |
|  | Ratio of |  |  |  |
|  | total time by # of CPUs |  |  |  |
|  | to total time by 128 CPUs |  |  |  |
|  | 128 | 5328.56778 | 1.000 |  |
|  | 256 | 2719.77511 | 1.959 |  |
|  | 512 | 1382.56556 | 3.854 |  |
|  | 1024 | 704.32679 | 7.565 |  |
|  | 2048 | 360.64294 | 14.775 |  |
