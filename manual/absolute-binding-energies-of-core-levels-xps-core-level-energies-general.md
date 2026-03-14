<a id="SECTION000581000000000000000"></a>
## General

OpenMX supports a general method to calculate absolute binding energies of core levels in metals and
insulators, based on a penalty functional and an exact Coulomb cutoff method in the framework of density
functional theory [[88](bibliography.md#Ozaki_XPS2017)]. With the method the spurious interaction of core holes between
supercells is avoided by the exact Coulomb cutoff method, while the variational penalty functional
enables us to treat multiple splittings due to chemical shift, spin-orbit coupling, and exchange
interaction on equal footing. It has been demonstrated that the absolute binding energies of core
levels for both metals and insulators are calculated by the proposed method in a mean absolute (relative)
error of 0.4 eV (0.16%) for eight cases compared to experimental values measured with x-ray photoemission
spectroscopy (XPS) within a generalized gradient approximation to the exchange-correlation functional.

By considering the energy conservation for the excitation process in the XPS measurements as schematically
shown in Fig. [78](absolute-binding-energies-of-core-levels-xps-core-level-energies-general.md#fig:XPS-Fig1), the absolute binding energies of core levels in gaseous and bulk systems
are respectively given by [[88](bibliography.md#Ozaki_XPS2017)]

<a id="eq:XPS-Eq1"></a>
<a id="eq:XPS-Eq2"></a>
| $\displaystyle E^{\rm (gas)}_{\rm b}$ | $\textstyle =$ | $\displaystyle E^{(0)}_{\rm f}(N-1) - E^{(0)}_{\rm i}(N),$ | (12) |
| --- | --- | --- | --- |
| $\displaystyle E^{\rm (bulk)}_{\rm b}$ | $\textstyle =$ | $\displaystyle E^{(0)}_{\rm f}(N-1) - E^{(0)}_{\rm i}(N) + \mu_0,$ | (13) |

where
$E^{(0)}_{\rm i}(N)$ and
$E^{(0)}_{\rm f}(N-1)$ are the total energies of the initial state
with $(N-1)$-electrons and the final state with $N$-electrons, respectively, calculated by DFT, and
$\mu_0$ is the chemical potential which is obtained from the initial state calculation.

$E^{(0)}_{\rm f}(N-1)$ is evaluated by the method proposed in Ref. [[88](bibliography.md#Ozaki_XPS2017)].
while
$E^{(0)}_{\rm i}(N)$ is calculated by the conventional band structure calculation.

<a id="fig:XPS-Fig1"></a>
<a id="4907"></a>
| ![\includegraphics[width=17.0cm]{XPS-Fig1.eps}](assets/XPS-Fig1.png) |
| --- |

Although Eq. ([13](absolute-binding-energies-of-core-levels-xps-core-level-energies-general.md#eq:XPS-Eq2)) is applicable to both gapped and metallic systems,
it should be noted that for metals Eq. ([12](absolute-binding-energies-of-core-levels-xps-core-level-energies-general.md#eq:XPS-Eq1)) can be transformed using
the Janak theorem [[89](bibliography.md#Janak1978)] as

<a id="eq:XPS-Eq3"></a>
| $\displaystyle E^{\rm (metal)}_{\rm b} = E^{(0)}_{\rm f}(N) - E^{(0)}_{\rm i}(N),$ |  |  | (14) |
| --- | --- | --- | --- |

For the final state one can calculate the total energy of the system with $N$ electrons
instead of the system with $(N-1)$ electrons. The expression well matches to our intutive understanding
that a perfect screeing takes place in metallic systems after the creation of core hole.
