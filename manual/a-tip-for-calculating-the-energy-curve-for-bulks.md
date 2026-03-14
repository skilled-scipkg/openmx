<a id="SECTION000132000000000000000"></a>
## A tip for calculating the energy curve for bulks

<a id="761"></a>
When the energy curve for bulk system is calculated as a function
of the lattice parameter, a sudden change of the number of real space grids
is a serious problem which produces an erratic discontinuity
on the energy curve. In fact, we see the discontinuity
in cases of 200 and 290 (Ryd) in Fig. [6](a-tip-for-calculating-the-energy-curve-for-bulks.md#fig:FeE) when the cutoff energy
is fixed. The discontinuity occurs at the lattice parameter where
the number of grids changes. To avoid the discontinuity on the energy
curve, a keyword 'scf.Ngrid' is available.

```text

    scf.Ngrid     32 32 32    # n1, n2, and n3 for a-, b-, and c-axes
```

When the number of grids is explicitly specified by the keyword,
the axis is discretized by the number without depending on
the keyword 'scf.energycutoff'.
We see in Fig. [6](a-tip-for-calculating-the-energy-curve-for-bulks.md#fig:FeE) that the fixed grids with
$32\times 32\times 32$ gives a smooth curve,
while the discontinuity is not so serious even in the cases of 'scf.energycutoff'.

<a id="fig:FeE"></a>
<a id="771"></a>
| ![\includegraphics[width=11.5cm]{FeE.eps}](assets/img116.png) |
| --- |
