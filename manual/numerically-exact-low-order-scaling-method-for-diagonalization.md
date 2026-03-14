<a id="SECTION000470000000000000000"></a>
# Numerically exact low-order scaling method for diagonalization

<a id="3295"></a>
A numerically exact low-order scaling method is supported for large-scale calculations [[124](bibliography.md#Ozaki_Low)].
The computational effort of the method scales as O(
$N({\rm log}N)^2$), O($N^2$), and O($N^{7/3}$)
for one, two, and three dimensional systems, respectively, where $N$ is the number of basis functions.
Unlike O($N$) methods developed so far the approach is a numerically exact alternative to conventional
O($N^3$) diagonalization schemes in spite of the low-order scaling, and can be applicable to
not only insulating but also metallic systems in a single framework. The well separated data
structure is suitable for the massively parallel computation as shown in Fig. [47](maximally-localized-wannier-function-analysis.md#fig:Wannier_Si).
However, the advantage of the method can be obtained
only when a large number of CPU cores are used for parallelization, since the prefactor of computational
efforts can be large. When you calculate low-dimensional large-scale systems using a large number of
CPU cores, the method can be a proper choice. To choose the method for diagonzalization, you can specify
the keyword 'scf.EigenvalueSolver' as

```text

  scf.EigenvalueSolver     cluster2
```

The method is supported only for colliear DFT calculations of cluster systems or periodic systems with
the $\Gamma $ point for the Brillouin zone sampling.

<a id="fig:LO_Para"></a>
<a id="3303"></a>
| ![\includegraphics[width=11.0cm]{LO_Para.eps}](assets/img373.png) |
| --- |

As well as the total energy calculation, the force calculation by the low-order scaling method
is supported. Thus, it is possible to perform geometry optimization.
However, calculations of density of states and wave functions are not supported yet.
The number of poles in the contour integration [[74](bibliography.md#Ozaki_FD)] is controlled by a keyword:

```text

  scf.Npoles.ON2              90
```

The number of poles to achieve convergence does not depend on the size of system [[124](bibliography.md#Ozaki_Low)],
but depends on the spectrum radius of system. If the electronic temperature more 300 K is used,
the use of 100 poles is enough to get sufficient convergence for the total energy and forces.
As an illustration, we show a calculation by the numerically exact low-order scaling method
using an input file 'C60_LO.dat' stored in the directory 'work'.

```text

  % mpirun -np 8 openmx C60_LO.dat
```

As shown in Table [10](numerically-exact-low-order-scaling-method-for-diagonalization.md#table:Low-order-scaling), the total energy by the low-order scaling method
is equivalent to that by the conventional method within double precision, while
the computational time is much longer than that of the conventional method for such a
small system. We expect that the crossing point between the low-order scaling
and the conventional methods with respect to computational time is located at around 300 atoms
when using more than 100 cores for the parallel computation, although it depends on
the dimensionality of system.

<a id="table:Low-order-scaling"></a>
<a id="table:Low-order-scaling"></a>
| Method
Total energy (Hartree)
Computational time (sec.)

Low-order
-343.896238929370
69.759

Conventional
-343.896238929326
2.784 |  |  |
| --- | --- | --- |
| Method | Total energy (Hartree) | Computational time (sec.) |
| Low-order | -343.896238929370 | 69.759 |
| Conventional | -343.896238929326 | 2.784 |
