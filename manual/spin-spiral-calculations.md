<a id="SECTION000550000000000000000"></a>
# Spin spiral calculations

<a id="4432"></a>
<a id="4433"></a>
<a id="4434"></a>
Spin spiral calculations are supported for the non-collinear DFT without spin orbit coupling (SOC),
which is based on the generalized Bloch theorem [[79](bibliography.md#Prayitno2018),[80](bibliography.md#Prayitno2019),[86](bibliography.md#Sandratskii1998),[87](bibliography.md#Garcia2004)].
It should be noted that the inclusion of SOC is not compatible with the functionality, since
the SOC violates the spiral symmetry imposed by the generalized Bloch theorem.
To acknowledge in any publications by using the functionality,
the citation of the reference [[79](bibliography.md#Prayitno2018),[80](bibliography.md#Prayitno2019)] would be appreciated.
To do the calculations, the following options are first set respectively

```text

   scf.SpinPolarization        NC        # On|Off|NC
   scf.Generalized.Bloch       on        # On|Off, default=off
   scf.SpinOrbit.Coupling      off       # On|Off, default=off
```

In the spiral structure there are two quantities to determine the spiral configuration which
should be paid attention. The first one is the cone angle. Since the spiral structure is
of two different kinds, i.e., the conical spiral ($0<\theta<90$) and the flat spiral ($\theta=90$),
where $\theta$ is the cone angle, $\theta$ should then be specified for the magnetic atoms.
In OpenMX, the cone angle $\theta$ is defined as the orientation for the spin magnetic moment
as shown in Fig. [71](spin-spiral-calculations.md#fig:SpinSpiral-Fig1)(a).
You can find how to specify the cone (Euler) angle in section of [34](non-collinear-dft.md#sec:Non-collinear_DFT) 'Non-collinear DFT'.
For example, the cone (Euler) angle can be specified as follows:

```text

   <Atoms.SpeciesAndCoordinates
    1  Fe  0.0    0.0    0.0     10.0    6.0   90.0   0.0   0.0   0.0  1 off
   Atoms.SpeciesAndCoordinates>
```

In the example above, the flat spiral will be achieved by setting $\theta=90$ degree as written
in the 8th column. In addition, you can also specify the initial angle of $\varphi$ as described
in the 9th column.
For fixing the cone angle, the constraint scheme is also available
as explained in section of [38](constraint-dft-for-non-collinear-spin-orientation.md#sec:Constraint_DFT_for_non-collinear_spin_orientation)
'Constraint DFT for non-collinear spin orientation'.

<a id="fig:SpinSpiral-Fig1"></a>
<a id="6421"></a>
| ![\includegraphics[width=17.5cm]{SpinSpiral-Fig1.eps}](assets/img440.png) |
| --- |

<a id="4456"></a>
The second one is the spiral vector **q** specified by

```text

   Spin.Spiral.Vector   0.0  0.0  0.0    # q1 q2 q3
```

In the above format, the spiral vector is specified by the fractional coordinates spanned by
the reciprocal lattice vectors. The first, second, and third columns denote
the components of spiral vector for the reciprocal vectors
$\tilde{\bf a}_1$,
$\tilde{\bf a}_2$,
and
$\tilde{\bf a}_3$, respectively. Then, the spin angle at atomic site $i$ is given by

| $\displaystyle M_i=M_i\{\cos({\bf q}\cdot {\bf R}_i+\varphi_0) \sin(\theta_i)+\sin({\bf q}\cdot {\bf R}_i+\varphi_0))\sin(\theta_i)+\cos(\theta_i)\}.$ |  |  |  |
| --- | --- | --- | --- |

With the translation by the lattice vectors, the spin angle at each atomic site is rotated according to the equation.

As an example of the spiral calculation, the spiral ground state of the fcc Fe is provided
in Fig. [72](spin-spiral-calculations.md#fig:SpinSpiral-Fig2).
We observe that the spiral ground state occurs at (0, 0, 0.6) and (0.2, 0, 1) defined in
Cartesian coordinates in units of $2\pi/a$. Indeed, using LCPAO method, the spiral calculation
needs the appropriate settings, such as the number of k points, number of orbitals, cutoff radius,
and cutoff energy for reaching the convergence and reliable result, a similar discussion can be
found in Ref. [[87](bibliography.md#Garcia2004)]. You can try to set those parameters to compare all of the results.
In addition, although there are some available mixing schemes specified by the keywords
'scf.Mixing.Type', we strongly recommend RMM-DIISH as your choice.
As an experience, this option can reach the convergence much faster than other choices
for all tested systems, the detail explanations can be found in Sec. [13](scf-convergence.md#sec:SCF-convergence) 'SCF convergence'.

<a id="fig:SpinSpiral-Fig2"></a>
<a id="6422"></a>
| ![\includegraphics[width=7.5cm]{SpinSpiral-Fig2.eps}](assets/img447.png) |
| --- |
