<a id="SECTION000152000000000000000"></a>
## Extrapolation scheme during MD and geometry optimization

<a id="946"></a>
In the geometry optimization and molecular dynamics simulations, the
restart files generated at the previous steps are automatically utilized
at the next step to accelerate the convergence using
an extrapolation scheme [[60](bibliography.md#Arias),[61](bibliography.md#Alfe)]. In the extrapolation scheme,
the number of previous MD or geometry optimization steps can be controlled by
a keyword:

```text

   scf.ExtCharge.History      2        # default=2
```

From a series of benchmark calculations, 'scf.ExtCharge.History' of 2 works well
and a larger number tends to be numerically unstable. So, we recommend for users
to use the default setting of 2.

---
