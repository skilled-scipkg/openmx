<a id="SECTION000272000000000000000"></a>
## Combination of the O(N) and conventional schemes

<a id="1651"></a>
<a id="1652"></a>
<a id="1653"></a>
Although the O($N$) methods can treat large-scale systems consisting of more than 1000 atoms,
a serious problem is that information about wave functions is lost in the O($N$) methods implemented in OpenMX.
A simple way of obtaining wave functions and the corresponding eigenvalues for the large-scale systems is firstly
to employ the O($N$) methods to obtain a self-consistent charge density, and then
is to just once diagonalize using the conventional diagonalization method
under the self-consistent charge density to obtain full wave functions.
As an illustration of this procedure, we show a large-scale calculation of
a multiply connected carbon nanotube (MCCN) consisting of 564 carbon atoms.
First, the SCF calculation of a MCCN was performed using the O($N$) Krylov subspace method
and 16 CPU cores of a 2.6 GHz Xeon, where C5.0-s2p1 (basis function),
130 Ryd (scf.energycutoff), 1.0e-7 (scf.criterion),
6.5 Å (orderN.HoppingRanges), 'orderN.KrylovH.order=400',
and RMM-DIISK (mixing scheme) were used. The input file is 'MCCN.dat' in the directory 'work'.
Figure [26](combination-of-the-o-n-and-conventional-schemes.md#fig:mccn-SCF) shows the norm of residual charge density in Fourier space as
a function of SCF steps. We see that 56 SCF steps is enough to
obtain convergent charge density for the system, where the
computational time was about seven minutes.
After that, the following keywords were set in

```text

    scf.maxIter                1
    scf.EigenvalueSolver    Band
    scf.Kgrid              1 1 1  
    scf.restart               on
    MO.fileout                on
    num.HOMOs                  2
    num.LUMOs                  2
    MO.Nkpoint                 1
    <MO.kpoint
      0.0  0.0  0.0
    MO.kpoint>
```

<a id="fig:mccn-SCF"></a>
<a id="1661"></a>
| ![\includegraphics[width=11.0cm]{mccn-SCF.eps}](assets/img185.png) |
| --- |

Then we calculated the same system in order to obtain wave functions
using 16 CPU cores of a 2.6 GHz Xeon machine, where the computational time
was about 2 minutes.
Figure [27](combination-of-the-o-n-and-conventional-schemes.md#fig:mccn_mo) shows isosurface maps of the HOMO and LUMO ($\Gamma $-point)
of MCCN calculated by the above procedure.
Although the difference between the O($N$) method and the conventional
diagonalization scheme in the computational time is not significant in
this example, the procedure will be useful for larger system including
more than several thousands atoms.

<a id="fig:mccn_mo"></a>
<a id="1669"></a>
| ![\includegraphics[width=10.0cm]{mccn_mo.eps}](assets/img186.png) |
| --- |
