<a id="SECTION000533000000000000000"></a>
## The origin of the reference unit cell

<a id="3794"></a>
If you take a close look at Eq. (17) in Ref. [[142](bibliography.md#Chi-Cheng-Lee2013)], you may notice that
the relabelling requires the two mapping rules, i.e.,
$R\to R+r_{0}(M)$ and $M\to m'(M)$,
where $R$ and $r_{0}(M)$ are the lattice vectors of the supercell and the reference cells,
respectively, and $M$ and $m'(M)$ are a symbolic atomic orbital index, respectively.
We have already given the keyword 'Unfolding.Map' which actually gives the mapping rule
in relabelling $M\to m'(M)$.
In this subsection, we explain how the relabelling
$R\to R+r_{0}(M)$ is taken into account.
The relabelling
$R\to R+r_{0}(M)$ depends on how the reference unit cell is placed relative
to the atomic coordinates in real space, which is equivalent to the choice of the origin
of the reference unit cell.
The choice of the origin can be insensitive to the unfolded weights,
because the mapping rule in relabelling $M\to m'(M)$ does not change in most cases.
However, the mapping rule may vary depending on the choice of the origin
in subtle cases such as surfaces and largely distorted structures.
As default, OpenMX will try to estimate an origin using the following two rules.
The first rule is that no more than one atom labeled by the same identification number
in the keyword 'Unfolding.Map' can be assigned in each reference cell.
The multiple assignment of atoms labeled by the same identification number to
a reference cell may happen in a largely distorted structure.
OpenMX will automatically try to avoid such a situation.
The second rule is that the origin of the reference cell is determined by minimizing
the total number of the reference lattices that the number of atoms allocated
by the rellabelling is non-zero. Since a system with surfaces represented by the supercell
approach has vacuum region between the slabs, the total number of the reference lattices
having non-zero allocated atoms may vary depending on the choice of origin.
OpenMX will automatically try to minimize the total number of the reference lattices
having non-zero allocated atoms.
Applying the two rules may satisfy requirement for most of users,
however, you may want to control the origin by yourself. For this purpose,
the following keyword is available:

```text

  <Unfolding.ReferenceOrigin
    0.1 0.2 0.3
  Unfolding.ReferenceOrigin>
```

where the unit is defined by the keyword 'Atoms.UnitVectors.Unit'.
