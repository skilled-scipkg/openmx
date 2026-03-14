<a id="SECTION000571000000000000000"></a>
## General

The $Z_{2}$ invariant of the system can be calculated with a method based on the Berry phase formalism
proposed by Fukui and Hatsugai [[81](bibliography.md#FHS2005),[82](bibliography.md#Feng2012)].
The functionality is compatible with only the non-collinear calculations.
Also, magnetic systems cannot be treated by the current implementation.
To acknowledge in any publications by using the functionality,
the citation of the reference [[84](bibliography.md#Sawahata2018)] would be appreciated.

The $Z_{2}$ invariant is a topological invariant number being 0 or 1, which is defined
on time reversal symmetric non-magnetic systems.
$Z_{2}=1$ and $Z_{2}=0$ correspond to topological and trivial insulators, respectively.
The $Z_{2}$ invariant is defined as

| $\displaystyle Z_{2} = \frac{1}{2\pi}{\displaystyle \sum_{n}^{\rm occ.}\left(\in...
...rtial B} {\bf A}_{n}\cdot d{\bf k}-\int_{B} F_{nz} dk^2\right)}\ ({\rm mod}\ 2)$ |  |  |  |
| --- | --- | --- | --- |

where
${\bf A}_{n}=-i\langle u_{n{\bf k}}\vert\frac{\partial}{\partial{\bf k}}\vert u_{n{\bf k}}\rangle$
is called Berry connection, and
${\bf F}_{n}=\nabla\times{\bf A}_{n}$ is called Berry curvature.
The integration range
$B=[-\frac{{\bf G}_{1}}{2},\frac{{\bf G}_{1}}{2}]\otimes[0,\frac{{\bf G}_{2}}{2}]$
is enough to consider only the half of Brillouin zone.
This is because the system has the time-reversal symmetry, and thereby the topological invariant
is defined on the half of Brillouin zone.
For performing the integration, we use the overlap matrix $U$, proposed by Fukui, Hatsugai, and Suzuki
[[81](bibliography.md#FHS2005),[82](bibliography.md#Feng2012)],
defined by
$U_{\Delta {\bf k}} = \det\langle u_{n}({\bf k})\vert u_{m}({\bf k}+\Delta {\bf k})\rangle$,
and calculate the Berry connection and Berry curvature on every 'plaquette',
which means meshed area in the Brillouin zone, as

| $\displaystyle A_{ab}$ | $\textstyle =$ | $\displaystyle {\rm Im}\log U_{ab},$ |  |
| --- | --- | --- | --- |
| $\displaystyle F$ | $\textstyle =$ | $\displaystyle {\rm Im}\log U_{12}U_{23}U_{34}U_{41}.$ |  |

Then, the integer-valued field $n(=0,\pm1)$ on every plaquette can be calculated by the following formula;

| $\displaystyle n({\bf k}) = \frac{1}{2\pi}(A_{12}+A_{23}+A_{31}+A_{41}-F)$ |  |  |  |
| --- | --- | --- | --- |

By summing up all the $n$ on the half Brillouin zone, and considering the modulo 2 of the summed value,
we can obtain the $Z_{2}$ invariant. It should be noted that the $Z_{2}$ invariant is gauge independent,
but the value of each $n$ is gauge dependent, which may vary depending on computational environment,
compiler optimization level, and a tiny difference in the electronic structure.
The details of computing ${\bf A}$ and $F$ is explained in Section of "Chern number and Berry curvature".
Please refer it.
Since the calculation of the $Z_{2}$ invariant is carried out by the contour integral
on the half of Brillouin zone, it depends on arbitrariness of wave function's gauges.
Therefore, we have to fix the gauges on the boundary of half Brillouin zone.
As shown in Fig. [75](computing-z-2-invariant-by-the-fukui-hatsugai-method-general.md#fig:Z2-Fig1), we consider the following three kinds of gauge fix on the boundary:

**Translational symmetry (red parts)**

| $\displaystyle \vert u_{n}({\bf k}+\frac{{\bf G}_{1}}{2})\rangle=e^{i{\bf G}_{1}\cdot{\bf r}}\vert u_{n}({\bf k}-\frac{{\bf G}_{1}}{2})\rangle$ |  |  |  |
| --- | --- | --- | --- |

**Time-reversal symmetry (blue parts)**

| $\displaystyle \vert u_{n}({\bf k})\rangle=\Theta\vert u_{n}(-{\bf k})\rangle
=\...
...ngle\vert\alpha\rangle
-\vert u^{*\alpha}_{n}(-{\bf k})\rangle\vert\beta\rangle$ |  |  |  |
| --- | --- | --- | --- |

**Kramars degenerates (yellow points)**

| $\displaystyle \vert u_{2n}({\bf k})\rangle=\Theta\vert u_{2n-1}(-{\bf k})\rangle$ |  |  |  |
| --- | --- | --- | --- |

In this calcuation, the eigenvalue problems are solved on the half of integration interval,
in other words, the quarter of Brillouin zone as shown in Fig. [75](computing-z-2-invariant-by-the-fukui-hatsugai-method-general.md#fig:Z2-Fig1).

<a id="fig:Z2-Fig1"></a>
<a id="4721"></a>
| ![\includegraphics[width=8.0cm]{Z2-Fig1.eps}](assets/img481.png) |
| --- |

When we perform the integrals on the other area,
we generate wave functions by fixing wavefunction's gauges
on the symmetrically corresponding plaquette, and perform the integral.

In case of the three dimensional system, the Brillouin zone has six time-reversal invariant planes,
$k_n=0$,
$k_n=\frac{{\bf G}_{n}}{2}$($n=1,2,3$).
Thus, six $Z_{2}$ invariants (
$x_{0},x_{\pi},y_{0},y_{\pi},z_{0},z_{\pi}$)
can be defined as shown in Fig. [76](computing-z-2-invariant-by-the-fukui-hatsugai-method-general.md#fig:Z2-Fig2).
Note that these invariants satisfy the following equation:

| $\displaystyle x_{0}+x_{\pi} = y_{0}+y_{\pi} = z_{0}+z_{\pi}\ ({\rm mod}\ 2)$ |  |  |  |
| --- | --- | --- | --- |

Therefore, only four invariants become independent parameters.
Based on the fact, the $Z_{2}$ invariant in 3D system is defined as

| $\displaystyle Z_{2} = (\nu_{0}, \nu_{1}, \nu_{2}, \nu_{3})=(x_{0}+x_{\pi}, x_{\pi}, y_{\pi}, z_{\pi})$ |  |  |  |
| --- | --- | --- | --- |

Especially, the system of $\nu_{0}=1$ is called strong topological insulator
because the $Z_{2}=1$ state appears on all the direction in the Brillouin zone.

<a id="fig:Z2-Fig2"></a>
<a id="6446"></a>
| ![\includegraphics[width=12.0cm]{Z2-Fig2.eps}](assets/img489.png) |
| --- |
