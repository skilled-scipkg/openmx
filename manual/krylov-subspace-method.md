<a id="SECTION000243000000000000000"></a>
## Krylov subspace method

<a id="1531"></a>
The DC method is robust and accurate for a wide variety of systems.
However, the size of truncated clusters to obtain an accurate result tends
to be large for metallic systems as shown in Fig. [18](divide-conquer-method.md#fig:DC_Error). A way of reducing
the computational efforts is to map the original vector space defined
by the truncated cluster into a Krylov subspace of which dimension
is smaller than that of the original space [[43](bibliography.md#Ozaki3)].
The Krylov subspace method is available by

```text

     scf.EigenvalueSolver       Krylov
```

Basically, the accuracy and efficiency are controlled by the following
two keywords:

```text

    orderN.HoppingRanges         6.0
    orderN.KrylovH.order         400
```

The keyword 'orderN.HoppingRanges'
defines the radius of a sphere centered on each atom in the same sense as
that in the DC method.
The dimension of the Krylov subspace of Hamiltonian in each truncated cluster
is given by 'orderN.KrylovH.order'.
Moreover, the Krylov subspace method can be precisely tuned by
the following keywords:

<a id="1548"></a>
<a id="1550"></a>
<a id="1551"></a>
<a id="1552"></a>
<a id="1554"></a>
<a id="1555"></a>
<a id="1556"></a>
<a id="1557"></a>
<a id="1559"></a>
<a id="1560"></a>
- orderN.Exact.Inverse.S on$\vert$ off, default=on
  <a id="1550"></a>
  <a id="1551"></a>
  In case of 'orderN.Exact.Inverse.S=on',
  the inverse of overlap
  matrix for each truncated cluster is exactly evaluated.
  Otherwise, see the next keyword 'orderN.KrylovS.order'.
- orderN.KrylovS.order 1200, default=orderN.KrylovH.order$\times 4$
  <a id="1555"></a>
  <a id="1556"></a>
  In case of 'orderN.Exact.Inverse.S=off',
  the inverse is approximated
  by a Krylov subspace method for the inverse, where the dimension of
  the Krylov subspace of overlap matrix in each truncated cluster is
  given by the keyword 'orderN.KrylovS.order'.
- orderN.Recalc.Buffer on$\vert$ off, default=on
  <a id="1559"></a>
  In case of 'orderN.Recalc.Buffer=on', the buffer matrix is recalculated
  at every SCF step. Otherwise, the buffer matrix is calculated at
  the first SCF step, and fixed at the subsequent SCF steps.
- orderN.Expand.Core on$\vert$ off, default=on
  In case of 'orderN.Expand.Core=on', the core region
  is defined by atoms within a sphere with radius of
  $1.2\times r_{\rm min}$, where
  $r_{\rm min}$ is the distance between the central atom and the nearest atom.
  The core region defines a set of vectors used for the first step in the generation
  of the Krylov subspace for each truncated cluster.
  In case of 'orderN.Expand.Core=off', the central atom is considered
  as the core region. The default is 'on'.

<a id="1565"></a>
<a id="1566"></a>
It is better to switch on 'orderN.Exact.Inverse.S'
and 'orderN.Expand.Core'
as the covalency increases, while the opposite could becomes better
in simple metallic systems.
In Fig. [23](krylov-subspace-method.md#fig:Compare_Krylov) the absolute error in the total energy calculated by the
Krylov and DC methods are shown for a wide variety of materials.
It is found that in comparison with the DC method, the Krylov subspace
method is more efficient especially for metallic systems,
and that the efficiency become comparable as the covalency
and ionicity in the electronic structure increase.

<a id="fig:Compare_Krylov"></a>
<a id="1544"></a>
| ![\includegraphics[width=10.0cm]{Compare_Krylov.eps}](assets/img179.png) |
| --- |

It is also noted that the O($N$) Krylov subspace method is well parallelized to realize
large-scale calculations.
The most efficient parallelization for the O($N$) Krylov subspace method can be realized
by using the same number of MPI processes as that of atoms together with OpenMP threads.
Figure [24](krylov-subspace-method.md#fig:Parallel_Krylov) shows that a system consisting of a hundred thousand
atoms can be treated on a massively parallel computer [[44](bibliography.md#Duy1),[45](bibliography.md#Duy2)], where
the diamond structure consisting of 131072 carbon atoms is considered as a benchmark system.

<a id="fig:Parallel_Krylov"></a>
<a id="1574"></a>
| ![\includegraphics[width=13.0cm]{Parallel_Krylov.eps}](assets/img180.png) |
| --- |
