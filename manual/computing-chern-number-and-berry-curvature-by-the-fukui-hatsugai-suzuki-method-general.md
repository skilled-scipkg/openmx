<a id="SECTION000561000000000000000"></a>
## General

In OpenMX Ver. 3.9, a post-processing code 'calB' is supported to calculate the Chern number
and Berry curvature of bands using overlap matrix elements between Kohn-Sham orbitals at
neighboring k-points by the Fukui-Hatsugai-Suzuki method [[81](bibliography.md#FHS2005),[85](bibliography.md#Sawahata-notes2016)].
The functionality is compatible with only the non-collinear calculations.
To acknowledge in any publications by using the functionality,
the citation of the reference [[84](bibliography.md#Sawahata2018)] would be appreciated.

The Chern number is a topological invariant being an integer number,
which characterizes the topology of bands for any materials.
In systems having a finite Chern number $C$, the anomalous Hall conductivity defined by

| $\displaystyle \sigma_{xy} = -\frac{e^2}{h}C\ (C=1,2,3,\cdots)$ |  |  |  |
| --- | --- | --- | --- |

is induced.
Using the Berry curvature

${\bf F}_{n}=\nabla\times{\bf A}_{n},\ {\bf A}_{n}=-i\langle u_{n{\bf k}}\vert\frac{\partial}{\partial{\bf k}}\vert u_{n{\bf k}}\rangle$,
the Chern number is defined as

| $\displaystyle {\displaystyle C = \frac{1}{2\pi}\sum_{n}^{\rm occ.}\int F_{nz}dk^2}$ |  |  |  |
| --- | --- | --- | --- |

In the Fukui-Hatsugai-Suzuki method [[81](bibliography.md#FHS2005)], the overlap matrix $U$ defined by

| $\displaystyle U_{\Delta {\bf k}}({\bf k}) =\det \langle u_{n}({\bf k})\vert u_{m}({\bf k}+\Delta {\bf k})\rangle$ |  |  |  |
| --- | --- | --- | --- |

plays a central role to calculate the Berry connection
${\bf A}({\bf k})$ and Berry curvature $F({\bf k})$,
which are defined by

|  |  | $\displaystyle {\bf A}({\bf k}) = {\rm Im}\log U_{\Delta {\bf k}}({\bf k}),$ |  |
| --- | --- | --- | --- |
|  |  | $\displaystyle F({\bf k}) = {\rm Im}\log U_{\Delta k_{1}}({\bf k})U_{\Delta k_{2...
...k_{1})U^{-1}_{\Delta k_{1}}({\bf k}+\Delta k_{2})U^{-1}_{\Delta k_{2}}({\bf k})$ |  |

<a id="fig:Chern-Fig1"></a>
<a id="4543"></a>
| ![\includegraphics[width=9.0cm]{Chern-Fig1.eps}](assets/img457.png) |
| --- |

As shown in Fig. [73](computing-chern-number-and-berry-curvature-by-the-fukui-hatsugai-suzuki-method-general.md#fig:Chern-Fig1), the Berry curvature can be calculated in each 'plaquette'
(plaquette means meshed area in Brillouin zone) on a regular mesh
introduced in the first Brillouin zone by the following formula:

| $\displaystyle F({\bf k})={\rm Im}\log U_{12}U_{23}U_{34}U_{41}$ |  |  |  |
| --- | --- | --- | --- |

By summing up all the contributions of the contour integrals for the Berry curvature, one can
calculate the Chern number as

| $\displaystyle C = \frac{1}{2\pi}{\displaystyle \sum_{\bf k}^{\rm BZ} F({\bf k})}$ |  |  |  |
| --- | --- | --- | --- |
