<a id="SECTION000481000000000000000"></a>
## General

The effective screening medium (ESM) method is a first-principles computational
method for charged or biased systems consisting of a slab [[125](bibliography.md#Otani06),[126](bibliography.md#Sugino07),[127](bibliography.md#Otani08),[128](bibliography.md#Ohwaki11)].
In this method,
a 2-dimensional periodic and 1-dimensional optional boundary conditions are imposed
on a model cell (Fig. [52](effective-screening-medium-method-general.md#fig:ESM1)(a)), and the Poisson's equation is solved under those set of
boundary conditions by using the Green's function method. An isolated slab,
charged slab, and a slab under a uniform electric field can be treated by
introducing the following combinations of semi-infinite media (ESMs).

- (a) Isolated slab: vacuum (relative permittivity $\varepsilon=1$) + vacuum
- (b) Charged slab: vacuum + ideal metal (relative permittivity
$\varepsilon=\infty$)
- (c) Slab under an electric filed: ideal metal + ideal metal

Here *slab* means a system consisting of molecules spaced out 2-dimensionally
as well as a slab generally used as a surface model. An isolated slab model can be
used for investigations of a polarized substrate, and charged slab model is applicable
to a simulation of an electrode surface. A slab model under an electric filed sandwiched
between two ideal-metal media would be appropriate for a material located in a metal capacitor.
In OpenMX, a unit cell used in an ESM-method calculation is constructed as follows
(see Fig. [52](effective-screening-medium-method-general.md#fig:ESM1)(a)):

<a id="fig:ESM1"></a>
<a id="3347"></a>
| ![\includegraphics[width=10.0cm]{ESM1.eps}](assets/img376.png) |
| --- |

1. The **a**-axis of the cell is perpendicular to the **b**-**c** plane and is parallel to the x-axis.
2. Two periodic boundary conditions are set in $y$- and $z$-axis directions
3. ESMs are placed at the cell-boundaries ($x = 0$ and $a$).
4. The origin of the $x$-axis is set at the cell boundary.
5. A fractional coordinate for x-axis is designated between 0 and 1.

A calculation based on the ESM-method can be performed by the following keyword:

```text

  ESM.switch             on3      # off, on1=v|v|v, on2=m|v|m, on3=v|v|m, on4=on2+EF
  ESM.buffer.range       4.5      # default=10.0 (ang),
```

where on1, on2, on3, and on4 represent combinations of ESMs, 'vacuum + vacuum', 'ideal metal + ideal metal',
'vacuum + ideal metal', and 'ideal metal + ideal metal under an electric field',
respectively. The keyword 'ESM.buffer.range' indicates the width of an exclusive region for
atoms with ESM (unit is Å), which is necessary in order to prevent overlaps between wave
functions and ESM.

<a id="3360"></a>
<a id="3365"></a>
<a id="3366"></a>
<a id="3370"></a>
1. ESM.switch = on1:
  Both ESM (I) and (II) are semi-infinite vacuum media. In this case, note that
  the total charge of a calculation system should be neutral.
  The keyword 'scf.system.charge' should be set to zero.
2. ESM.switch = on2:
  Both ESM (I) and (II) are semi-infinite ideal-metal media. One can deal
  with charged systems. The keyword 'scf.system.charge' can be set to a finite value.
3. ESM.switch = on3:
  ESM (I) and (II) are a semi-infinite vacuum and ideal metal medium,
  respectively. One can deal with charged systems. The keyword 'scf.system.charge'
  can be set to be a finite value.
4. ESM.switch = on4:
  <a id="3360"></a>
  An electric field is imposed on the system with the same combination of ESMs to 'on2'.
  By using the following keyword, one can impose a uniform electric field on a calculation system;
  ```text

    ESM.potential.diff        1.0      # default=0.0 (eV),
  ```
  where you can specify a potential difference between two semi-infinite ideal-metal media
  with reference to the bottom ideal metal (unit is eV). The electric filed is determined
  by the length of the cell, a, and the potential difference.
5. In case of MD calculations with the ESM method:
  <a id="3365"></a>
  <a id="3366"></a>
  One can perform MD calculations of solid surface-liquid interface systems
  with any combinations of ESMs. A surface-model slab and a liquid region
  should be located as shown in Fig. [52](effective-screening-medium-method-general.md#fig:ESM1)(b).
  In order to restrict liquid molecules
  within a given region, an cubic barrier potential can be introduced by
  using the following keyword (see Fig. [52](effective-screening-medium-method-general.md#fig:ESM1)(b)):
  ```text

    ESM.wall.position        6.0      # default=10.0 (ang)
    ESM.wall.height        100.0      # default=100.0 (eV),
  ```
  where 'ESM.wall.position' denotes the distance between the upper edge
  of the cell and the origin of the barrier potential, $a-x_b$, and 'ESM.wall.height'
  is the height of the potential (value of potential energy) at $x=x_b+1.0$ (Å).
  It is also recommended to fix positions of atoms on the bottom of a surface-model slab
  during the MD run.
6. Choice of the axis to be treated by ESM method
  <a id="3370"></a>
  As shown in Fig. [52](effective-screening-medium-method-general.md#fig:ESM1)(a), we assume in the manual that the treatment by the ESM method is applied to
  the $x$-axis. However, the choice of the axis to be treated by ESM method can be changed by the keyword 'ESM.direction' as
  ```text

    ESM.direction            x         # x|y|z, default=x
  ```
  The default direction is the $x$-axis as shown in Fig. [52](effective-screening-medium-method-general.md#fig:ESM1)(a).
