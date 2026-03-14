<a id="SECTION000382100000000000000"></a>
### Varying the ratio of two Slater integrals ($F^4/F^2$)

The general DFT+$U$ scheme by setting `scf.DFTU.Type=2` requires the generation of
Coulomb interaction tensor using two input values, $U$ and $J$. This can be done
by the combinations of Slater integrals (
$F^0, F^2, F^4,...$) and Racah-Wigner coefficients
assuming atomic sphericity. For $d$-orbitals in the standard DFT+$U$ scheme, $F^4/F^2$ ratio
should be specified, and $F^4/F^2=0.625$ is the usual choice. This ratio is, however,
valid only in the atomic environment and deviates from it in the solid.
Users can manually choose the ratio for their own purposes by the following keyword:

```text

  scf.Slater.Ratio                 0.75	   # default=0.625
```

---
