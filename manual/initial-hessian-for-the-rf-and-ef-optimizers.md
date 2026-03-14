<a id="SECTION000163000000000000000"></a>
## Initial Hessian for the RF and EF optimizers

Two sorts of the initial approximate Hessian for the RF and EF optimizers in the geometry optimization
are available in OpenMX Ver. 3.9, which can be specified by the following keyword:

```text

   MD.Opt.Init.Hessian        Schlegel      # Schlegel|iden, default=Schlegel
```

The defaut is 'Schlegel' which was proposed by Schlegel [[66](bibliography.md#Schlegel)], and estimates the initial Hessian
using a simple model consisting of bond stretching, angle bending, and torsion, while only the bond stretching term
is taken into account in the implementation of OpenMX Ver. 3.9.
The other is 'iden' which starts from the identity matrix for the approximate Hessian.
In both the cases, the initial Hessian is updated every geometry optimization step by
the Broyden-Fletcher-Goldfarb-Shanno (BFGS) method [[65](bibliography.md#BFGS)].
It is noted that 'Schlegel' is not supported for the optimizers of 'BFGS' and 'DIIS'.
In general, the method of Schlegel provides a faster convergence in the optimization compared to the initial
approximate Hessian of the identity matrix. Thus, one should use 'Schlegel' being default as a first choice.
In Fig. [11](initial-hessian-for-the-rf-and-ef-optimizers.md#fig:Comp_Hess_GeoOpt) a comparison between 'Schlegel' and 'iden' is shown during the geometry
optimization using the EF method. It can be seen that the EF method with 'Schlegel' is faster than 'iden'
in most cases including molecules and bulks.

<a id="fig:Comp_Hess_GeoOpt"></a>
<a id="6251"></a>
| ![\includegraphics[width=9.0cm]{Comp_Hess_GeoOpt.eps}](assets/img130.png) |
| --- |
