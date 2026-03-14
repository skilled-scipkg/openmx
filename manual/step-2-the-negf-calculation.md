<a id="SECTION000443000000000000000"></a>
## Step 2: The NEGF calculation

**A. Setting up Lead$\vert$Device$\vert$Lead**

You can set up the regions $L_0$, $C_0$, and $R_0$ in the structural
configuration shown in Fig. [39](electric-transport-calculations-general.md#fig:NEGF_system) in the following way:

<a id="2575"></a>
<a id="2576"></a>
The geometrical structure of the central region $C_0$ is specified by
the following keywords 'Atoms.Number'
and 'Atoms.SpeciesAndCoordinates':

```text

     Atoms.Number        18
     <Atoms.SpeciesAndCoordinates
       1  C  3.000  0.000  0.000  2.0 2.0
        .....
      18  C 28.500  0.000  0.000  2.0 2.0
     Atoms.SpeciesAndCoordinates>
```

<a id="2580"></a>
<a id="2581"></a>
The geometrical structure of the left lead region $L_0$ is specified by
the following keywords
'LeftLeadAtoms.Number'
and 'LeftLeadAtoms.SpeciesAndCoordinates':

```text

     LeftLeadAtoms.Number         3
     <LeftLeadAtoms.SpeciesAndCoordinates         
       1  C -1.500  0.000  0.000  2.0 2.0
       2  C  0.000  0.000  0.000  2.0 2.0
       3  C  1.500  0.000  0.000  2.0 2.0
     LeftLeadAtoms.SpeciesAndCoordinates>
```

<a id="2585"></a>
<a id="2586"></a>
The geometrical structure of the right lead region $R_0$ is specified by
the following keywords
'RightLeadAtoms.Number'
and 'RightLeadAtoms.SpeciesAndCoordinates'

```text

     RightLeadAtoms.Number        3
     <RightLeadAtoms.SpeciesAndCoordinates         
       1  C 30.000  0.000  0.000  2.0 2.0
       2  C 31.500  0.000  0.000  2.0 2.0
       3  C 33.000  0.000  0.000  2.0 2.0
     RightLeadAtoms.SpeciesAndCoordinates>
```

This is the case of carbon chain which is demonstrated in the previous subsection.
The central region $C_0$ is formed by 18 carbon atoms, and the left and right
regions $L_0$ and $R_0$ contains three carbon atoms, respectively, where every bond
length is 1.5 Å. Following the geometrical specification of device and leads,
OpenMX will construct an extended central region
$C (\equiv L_0\vert C_0\vert R_0)$ as
shown in Fig. [39](electric-transport-calculations-general.md#fig:NEGF_system).
The Green function for the extended central region $C$ is self-consistently determined
in order to take account of relaxation of electronic structure around
the interface between the central region $C_0$ and the region $L_0(R_0)$.
In addition, we impose two conditions so that the central Green function
can be calculated in the NEGF method [[73](bibliography.md#Ozaki_NEGF)]:

1. The localized basis orbitals $\phi$ in the region $C_0$ overlap with those in the regions $L_0$ and $R_0$, but do not overlap with those in the regions $L_1$ and $R_1$.
2. The localized basis orbitals $\phi$ in the $L_i$ ($R_i$) region has no overlap with basis orbitals in the cells beyond the nearest neighboring cells $L_{i-1}$ ($R_{i-1}$) and $L_{i+1}$ ($R_{i+1}$).

In our implementation the basis functions are strictly localized in
real space because of the generation of basis orbitals by a confinement
scheme [[41](bibliography.md#Ozaki1),[42](bibliography.md#Ozaki2)].
Therefore, once the localized basis orbitals with specific
cutoff radii are chosen for each region, the two conditions
can be always satisfied by just adjusting the size of the unit cells
for $L_i$ and $R_i$.

Although the specification of unit cells for the regions $L_0$, $C_0$,
and $R_0$ is not required, it should be noted that some periodicity is
implicitly assumed. The construction of infinite leads is made by
employing the unit cells used in the band structure calculations by the step 1,
and the informations are stored in a file '*NEGF.filename.hks*'. Also, due to the structural
configuration shown in Fig. [39](electric-transport-calculations-general.md#fig:NEGF_system), the unit vectors on the **bc**-plane
for the left and right leads should be consistent. Thus, the unit vector
on the **bc**-plane for the extended central region $C$ is implicitly assumed
to be same as that of the leads. Within the structural limitation, you can
set up the structural configuration.

The unit in the specification of the geometrical structure can be given by

```text

    Atoms.SpeciesAndCoordinates.Unit   Ang # Ang|AU
```

In the NEGF calculation, either 'Ang' or 'AU' for
'Atoms.SpeciesAndCoordinates.Unit'
is supported, but 'FRAC' is not.

How OpenMX analyzes the geometrical structure can be confirmed by
the standard output as shown below:

```text

   <TRAN_Calc_GridBound>

   *******************************************************
   The extended cell consists of Left0-Center-Right0.
   The cells of left and right reads are connected as.
   ...|Left2|Left1|Left0-Center-Right0|Right1|Right2...

   Each atom in the extended cell is assigned as follows:
   where '12' and '2' mean that they are in 'Left0', and
   '12' has overlap with atoms in the Left1,
   and '13' and '3' mean that they are in 'Right0', and
   '13' has overlap with atoms in the 'Right1', and also
   '1' means atom in the 'Center'.
   ********************************************************

   Atom1  = 12 Atom2  =  2 Atom3  =  1 Atom4  =  1 Atom5  =  1 Atom6  =  1 Atom7  =  1
   Atom8  =  1 Atom9  =  1 Atom10 =  1 Atom11 =  1 Atom12 =  1 Atom13 =  1 Atom14 =  1
   Atom15 =  1 Atom16 =  1 Atom17 =  1 Atom18 =  1 Atom19 =  1 Atom20 =  1 Atom21 =  3
   Atom22 = 13
```

The atoms in the extended cell consisting of
$L_0\vert C_0\vert R_0$ are
assigned by the numbers, where
'12' and '2' mean that they are in $L_0$, and
'12' has overlap with atoms in $L_1$,
and '13' and '3' mean that they are in $R_0$, and
'13' has overlap with atoms in $R_1$, and also
'1' means atom in $C_0$. By checking the analysis you may confirm whether
the structure is properly constructed or not.

**B. Keywords**

<a id="2610"></a>
The NEGF calculation of the step 2 is performed by the keyword
'scf.EigenvalueSolver':

```text

    scf.EigenvalueSolver       NEGF
```

For the NEGF calculation the following keywords are newly added.

```text

    NEGF.filename.hks.l     lead-chain.hks
    NEGF.filename.hks.r     lead-chain.hks

    NEGF.Num.Poles             100       # defalut=150
    NEGF.scf.Kgrid             1 1       # defalut=1 1

    NEGF.bias.voltage          0.0       # default=0.0 (eV)
    NEGF.bias.neq.im.energy    0.01      # default=0.01 (eV)
    NEGF.bias.neq.energy.step  0.02      # default=0.02 (eV)
```

An explanation for each keyword is given below.

```text

    NEGF.filename.hks.l     lead-chain.hks
    NEGF.filename.hks.r     lead-chain.hks
```

The files containing information of leads are specified by
the above two keywords, where 'NEGF.filename.hks.l'
and 'NEGF.filename.hks.r'
are for the left and right leads, respectively.

```text

    NEGF.Num.Poles             100       # defalut=150
```

The equilibrium density matrix is evaluated by a contour integration
method [[73](bibliography.md#Ozaki_NEGF),[74](bibliography.md#Ozaki_FD)].
The number of poles used in the method is specified by
the keyword 'NEGF.Num.Poles'.

```text

    NEGF.scf.Kgrid             1 1       # defalut=1 1
```

The numbers of **k**-points to discretize the reciprocal vectors

${\bf\tilde{b}}$ and
${\bf\tilde{c}}$ are specified by the keyword
'NEGF.scf.Kgrid'.
Since no periodicity is assumed along the **a**-axis,
you do not need to specify that for the **a**-axis.

<a id="2636"></a>

```text

    NEGF.scf.Iter.Band          6        # defalut=6
```

It would be better to use the conventional diagonalization method for a few SCF steps
in the initial SCF iterations by assuming a periodicity along the **a**-axis as well as
**b**- and **c**-axes. The procedure is effective to avoid an erratic charge distribution
which is a serious problem in the self-consistent NEGF method. The number of first SCF steps
for which the conventional diagonalization method is applied is controlled by the keyword 'NEGF.scf.Iter.Band'.
Up to and including the SCF steps specified by 'NEGF.scf.Iter.Band', the conventional diagonalization method
is used and then onward, the solver is switched from the conventional method to the NEGF method.
The default is 6.

```text

    NEGF.bias.voltage          0.0       # default=0.0 (eV)
```

The source-drain bias voltage applied to the left and right leads is
specified by the keyword 'NEGF.bias.voltage'
in units of eV, corresponding
to Volt. Noting that only the difference between applied bias voltages
has physical meaning, you only have to give a single value as the source-drain bias
voltage.

```text

    NEGF.bias.neq.im.energy    0.01      # default=0.01 (eV)
    NEGF.bias.neq.energy.step  0.02      # default=0.02 (eV)
```

When a finite source-drain bias voltage is applied, a part of the density matrix
is contributed by the non-equilibrium Green function.
Since the non-equilibrium Green function is not analytic in general in the complex
plane, the contour integration method used for the equilibrium Green function
cannot be applied. Thus, in the current implementation the non-equilibrium
Green function is evaluated on the real axis with a small imaginary part using
a simple rectangular quadrature scheme. Then, the imaginary part is given by
the keyword 'NEGF.bias.neq.im.energy'
and the step width is given by
the keyword 'NEGF.bias.neq.energy.step'
in units of eV. In most cases,
the default values are sufficient, while the detailed analysis of the convergence
property can be found in Ref. [[73](bibliography.md#Ozaki_NEGF)]. How many energy points on the
real axis are used for the evaluation of the non-equilibrium Green function
can be confirmed in the standard output and the file '*System.Name*.out'.
In case of 'NEGF-Chain.dat',
if the bias voltage of 0.5 V is applied, you will see in the standard output
that the energy points of 120 are allocated for the calculation as follows:

```text

   Intrinsic chemical potential (eV) of the leads
     Left lead:  -7.752843837400
     Right lead: -7.752843837400
     add voltage =  0.0000 (eV) to the  left lead: new ChemP (eV):  -7.7528
     add voltage =  0.5000 (eV) to the right lead: new ChemP (eV):  -7.2528

   Parameters for the integration of the non-equilibrium part
     lower bound:           -8.706843837400 (eV)
     upper bound:           -6.298843837400 (eV)
     energy step:            0.020000000000 (eV)
     number of steps:           120
```

The total number of energy points where the Green function is evaluated is given
by the sum of the number of poles and the number of energy points on the real axis
determined by the two keywords 'NEGF.bias.neq.im.energy'
and
'NEGF.bias.neq.energy.step',
and you should notice that the computational time
is proportional to the total number of energy points.

```text

    NEGF.Poisson.Solver       FD     # FD|FFT, default=FD
```

In the NEGF method, the electrostatic potential is calculated by either a finite difference plus
two dimensional FFT (FD) [[73](bibliography.md#Ozaki_NEGF)] or three dimensional FFT (FFT) [[75](bibliography.md#Brandbyge)].
The choice of the Poisson solver is specified by the keyword 'NEGF.Poisson.Solver'.
Both the methods provide similar electrostatic potentials for non-polar systems, while
the difference can be large for polar systems. The former is a proper choice in a sense that the eletrostatic
potential at the boundaries between the leads and the central region should be the same as that in the calculations
of the step 1 for the leads, while the SCF convergence seems to be rather easily obtained by the latter.
The default is FD.

**C. SCF criterion**

<a id="2665"></a>
In the NEGF method, the SCF criterion given by the keyword
'scf.criterion' is applied to the residual norm
between the input and output charge densities 'NormRD', while in the other
cases 'dUele' is monitored. See also the keyword 'NEGF.scf.Iter.Band'.

**D. Gate bias voltage**

In our implementation, the gate voltage $V_{\rm g}(x)$ is treated by adding
an electric potential defined by

<a id="eq:c1-56"></a>
| $\displaystyle V_{\rm g}(x) =
V_{\rm g}^{(0)} \exp\left[-\left(\frac{x-x_{\rm c}}{d}\right)^{8}\right],$ |  |  |  |
| --- | --- | --- | --- |

where
$V_{\rm g}^{(0)}$ is a constant value corresponding to the gate voltage,
and is specified by the keyword 'NEGF.gate.voltage'
as follows:

```text

      NEGF.gate.voltage   1.0    # default=0.0 (in eV)
```

$x_{c}$ the center of the region $C_0$, and $d$ the length of
the unit vector along **a**-axis for the region $C_0$. Due to the form
of the equation, the applied gate voltage affects mainly the region
$C_0$ in the central region $C$.
The electric potential may resemble the potential produced by the image
charges [[76](bibliography.md#Liang)].

**E. Density of States (DOS)**

In the NEGF calculation, the density of states can be calculated by
setting the following keywords:

```text

    Dos.fileout                 on              # on|off, default=off
    NEGF.Dos.energyrange     -15.0 25.0 5.0e-3  #default=-10.0 10.0 5.0e-3 (eV)
    NEGF.Dos.energy.div        200              # default=200
    NEGF.Dos.Kgrid             1 1              # default=1 1
```

When you want to calculate DOS, the keyword 'Dos.fileout'
should be set to 'on' as usual.
Also, the energy range where DOS is calculated is given by
the keyword 'NEGF.Dos.energyrange',
where the first and second numbers correspond
to the lower and upper bounds, and the third number is an imaginary number
used for smearing out DOS. The energy range specified by
'NEGF.Dos.energyrange'
is divided by the number specified by the keyword
'NEGF.Dos.energy.div'.
The numbers of **k**-points to discretize the reciprocal vectors

${\bf\tilde{b}}$ and
${\bf\tilde{c}}$ are specified by the keyword
'NEGF.Dos.Kgrid'.
The set of numbers given by 'NEGF.Dos.Kgrid' can be set larger than
that by 'NEGF.scf.Kgrid' to increase computational accuracy.
After the NEGF calculation with these parameters, you will find two files
'*System.Name*.Dos.val' and '*System.Name*.Dos.vec', and can analyze those by the same procedure
as usual. Also, it should be noted that the origin of energy is set to
the chemical potential of the **left** lead.
