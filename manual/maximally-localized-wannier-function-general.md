<a id="SECTION000451000000000000000"></a>
## General

The following are descriptions on how to use OpenMX to generate maximally
localized Wannier function (MLWF) [[122](bibliography.md#mlwf1),[123](bibliography.md#mlwf2)].
Keywords and settings for controlling the calculations are explained.
The style of keywords are closely following those originally in OpenMX.
Throughout the section, a couple of results for silicon in the diamond
structure will be shown for convenience. The calculation can be traced
by openmx code with an input file 'Si.dat' in
'work/wf_example'. There is no additional post
processing code. After users may get the convergent result for the
conventional SCF process for the electronic structure calculation,
the following procedure explained below will be repeated by changing
a couple of parameters with the restart file until desired MLWFs
are obtained.

To acknowledge in any publications by using the functionality,
the citation of the reference [[77](bibliography.md#vbz)] would be appreciated:

**Switching on generating MLWFs**

<a id="2923"></a>
To switch on the calculation, a keyword
'Wannier.Func.Calc' should be
explicitly set as 'on'. Its default value is 'off'.

```text

  Wannier.Func.Calc        on         #default off
```

**Setting the number of target MLWFs**

<a id="2928"></a>
The number of target MLWFs should be given explicitly by setting
a keyword 'Wannier.Func.Num' and no default value for it.

```text

  Wannier.Func.Num       4         #no default
```

**Energy window for selecting Bloch states**

<a id="2935"></a>
<a id="2936"></a>
<a id="2937"></a>
<a id="2938"></a>
The MLWFs will be generated from a set of Bloch states, which are selected by
defining an energy window covering the eigenenergies of them.
Following Ref. [[123](bibliography.md#mlwf2)], two energy windows are introduced.
One is so-called outer window, defined by two keywords,
'Wannier.Outer.Window.Bottom'
and 'Wannier.Outer.Window.Top',
indicating the lower and upper boundaries, respectively.
The other one is inner window, which is specified by two similar key words,
'Wannier.Inner.Window.Bottom'
and 'Wannier.Inner.Window.Top'.
All these four values are given in the unit of eV relative to the Fermi level.
The inner window should be fully inside of the outer window. If the
two boundaries of inner window are equal to each other, it means inner
window is not defined and not used in calculation. There is no default
values for the outer window, while 0.0 is the default value for two boundaries
of inner window. One example is as following:

```text

  Wannier.Outer.Window.Bottom   -14.0   #lower boundary of outer window, no default value
  Wannier.Outer.Window.Top        0.0   #upper boundary of outer window, no default value
  Wannier.Inner.Window.Bottom     0.0   #lower boundary of inner window, default value 0.0
  Wannier.Inner.Window.Top        0.0   #upper boundary of outer window, default value 0.0
```

To set these two windows covering interested bands, it is usually to plot band
structure and/or density of states before the calculation of MLWFs.
If you want to restart the minimization of MLWFs by reading the overlap
matrix elements from files, the outer window should not be larger than that
used for calculating the stored overlap matrix. Either equal or smaller is
allowed. The inner window can be varied within the outer window as you like
when the restart calculation is performed. This would benefit the restarting
calculation or checking the dependence of MLWFs on the size of both the windows.
For the restarting calculation, please see also the section (7)
'Restart optimization without calculating overlap matrix'.

**Initial guess of MLWFs**

<a id="2942"></a>
User can choose whether to use initial guess of target MLWFs or not by
setting the keyword 'Wannier.Initial.Guess'
as 'on' or 'off'. Default value is 'on', which means we recommend user
to use an initial guess to improve the convergence or avoid local
minima during the minimization of spread function.

If the initial guess is required, a set of local functions with the same
number of target MLWFs should be defined. Bloch wave functions inside the
outer window will be projected on to them. Therefore, these local functions
are also called as projectors. The following steps are required to specify
a projector.

*A. Define local functions for projectors*

Since the pseudo-atomic orbitals are used for projectors, the specification of
them is the same as for the basis functions. An example setting, for
silicon in diamond structure, is as following:

```text

   Species.Number          2            

   <Definition.of.Atomic.Species 
     Si       Si7.0-s2p2d1    Si_CA19   
     proj1    Si5.5-s1p1d1f1  Si_CA19   
   Definition.of.Atomic.Species>
```

In this example, since we employ PAOs from Si as projectors, an additional specie
'proj1' is defined as shown above. Inside the pair keywords
'$<$Definition.of.Atomic.Species'
and 'Definition.of.Atomic.Species$>$',
in addition to the first line used for Si atoms, one species for the
projectors is defined. Its name is 'proj1' defined by 'Si5.5-s1p1d1f1' and
the pseudopotential 'Si_CA19'. In fact, the pseudopotential defined
in this line will not be used. It is given just for keeping the
consistency of inputting data structure. One can use any PAO as projector.
Also the use of only a single basis set is allowed for each l-component.
We strongly recommend user to specify 's1p1d1f1' in all cases to avoid
possible errors.

*B. Specify the orbital, central position and orientation of a projector*

<a id="2950"></a>
<a id="2951"></a>
Pair keywords '$<$Wannier.Initial.Projectos' and
'Wannier.Initial.Projectos$>$' will be used to specify the
projector name, local orbital function, center of local orbital,
and the local $z$-axis and $x$-axis for the orbital orientation.

An example setting is shown here:

```text

<Wannier.Initial.Projectors 
   proj1-sp3   0.250  0.250  0.250   -1.0 0.0 0.0    0.0  0.0 -1.0
   proj1-sp3   0.000  0.000  0.000    0.0 0.0 1.0    1.0  0.0  0.0
Wannier.Initial.Projectors>
```

Each line contains the following items.
For example, in the first line, the species name, 'proj1', is defined
in pairing keywords
'Definition.of.Atomic.Species'. '-' is used
to connect the projector name and the selected orbitals. 'sp3' means that the
sp3 hybridized orbitals of this species is used as the initial guess
of four target Wannier functions (see also Table 6 for all the possible
orbitals and their hybrids). The projectors consisting of hybridized
orbitals are centered at the position given
by the following 3 numbers, '0.25 0.25 0.25', which are given in
unit defined by keyword
'Wannier.Initial.Projectors.Unit'
(to be explained below). The next two sets of three numbers
define the $z$-axis and $x$-axis of the local coordinate system,
respectively, where each axis
is specified by the vector defined by three components in $xyz$-coordinate.
In this example, in the first line the local z-axis defined by '-1.0 0.0 0.0'
points to the opposite direction to the original $x$-axis, while
the local $x$-axis defined by '0.0 0.0 -1.0' points to the opposite
direction to the original $z$-axis. In the second line the local axes are
the same as the original coordinate system.

The orbital used as projector can be the original PAOs or any hybrid
of them. One must be aware that the total number of projectors
defined by 'sp3' is 4. Similarly, 'sp' and 'sp2' contain 2 and 3
projectors, respectively. A list of supported PAOs
and hybridizations among them can be found in Table [9](maximally-localized-wannier-function-general.md#table:WF-Projectors).
Any name other than those listed is not allowed.

<a id="2957"></a>
The projector can be centered anywhere inside the unit cell. To specify its location,
we can use the fractional (FRAC) coordinates relative to the unit cell vectors
or Cartesian coordinates in atomic unit (AU) or in angstrom (ANG).
The corresponding keyword is
'Wannier.Initial.Projectors.Unit'.

```text

   Wannier.Initial.Projectors.Unit     FRAC     #AU, ANG or FRAC
```

<a id="table:WF-Projectors"></a>
<a id="2961"></a>
<a id="tab1"></a>
| Orbital name | Number of included projector | Description |
| --- | --- | --- |
| s | 1 | $s$ orbital from PAOs |
| p | 3 | $p_x, p_y, p_z$ from PAOs |
| px | 1 | $p_x$ from PAOs |
| py | 1 | $p_y$ from PAOs |
| pz | 1 | $p_z$ from PAOs |
| d | 5 | $d_{z^2}, d_{x^2-y^2}, d_{xy}, d_{xz}, d_{yz}$ from PAOs |
| dz2 | 1 | $d_{z^2}$ from PAOs |
| dx2-y2 | 1 | $d_{x^2-y^2}$ from PAOs |
| dxy | 1 | $d_{xy}$ from PAOs |
| dxz | 1 | $d_{xy}$ from PAOs |
| dyz | 1 | $d_{xy}$ from PAOs |
| f | 7 | $f_{z^3}, f_{xz^2}, f_{yz^2}, f_{zx^2}, f_{xyz}, f_{x^3-3xy^2}, f_{3yx^2-y^3}$ from PAOs |
| fz3 | 1 | $f_{z^3}$ from PAOs |
| fxz2 | 1 | $f_{xz^2}$ from PAOs |
| fyz2 | 1 | $f_{yz^2}$ from PAOs |
| fzx2 | 1 | $f_{zx^2}$ from PAOs |
| fxyz | 1 | $f_{xyz}$ from PAOs |
| fx3-3xy2 | 1 | $f_{x^3-3xy^2}$ from PAOs |
| f3yx2-y3 | 1 | $f_{3yx^2-y^3}$ from PAOs |
| sp | 2 | Hybridization between s and px orbitals,
including
$\frac{1}{\sqrt 2 }(s + p_x)$ and
$\frac{1}{\sqrt 2 }(s - p_x)$ |
| sp2 | 3 | Hybridization among s, px, and py orbitals,
including
$\frac{1}{\sqrt 3 }s - \frac{1}{\sqrt 6 }p_x + \frac{1}{\sqrt 2 }p_y$,

$\frac{1}{\sqrt 3 }s - \frac{1}{\sqrt 6 }p_x - \frac{1}{\sqrt 2 }p_y$
and
$\frac{1}{\sqrt 3 }s + \frac{2}{\sqrt 6 }p_x$ |
| sp3 | 4 | Hybridization among s, px, py and pz orbitals:

$\frac{1}{\sqrt 2 }(s + p_x + p_y + p_z),
\frac{1}{\sqrt 2 }(s + p_x - p_y - p_z)$

$\frac{1}{\sqrt 2 }(s - p_x + p_y - p_z),
\quad
\frac{1}{\sqrt 2 }(s - p_x - p_y + p_z)$ |
| sp3dz2 | 5 | Hybridization among
$s, p_x, p_y, p_z$ and $d_{z^2}$ orbitals:

$\frac{1}{\sqrt 3 }s - \frac{1}{\sqrt 6 }p_x + \frac{1}{\sqrt 2 }p_y$,

$\frac{1}{\sqrt 3 }s - \frac{1}{\sqrt 6 }p_x + \frac{1}{\sqrt 2 }p_y,
\frac{1}{\sqrt 3 }s - \frac{2}{\sqrt 6 }p_x$

$\frac{1}{\sqrt 2 }p_z + \frac{1}{\sqrt 2 }d_{z^2},
- \frac{1}{\sqrt 2 }p_z + \frac{1}{\sqrt 2 }d_{z^2}$ |
| sp3deg | 6 | Hybridization among
$s, p_x, p_y, p_z$ and
$d_{z^2}, d_{x^2-y^2}$ orbitals:

$\frac{1}{\sqrt 6 }s - \frac{1}{\sqrt 2 }p_x - \frac{1}{\sqrt {12} }d_{z^2}
+ \frac{1}{2}d_{x^2-y^2}$,

$\frac{1}{\sqrt 6 }s
+ \frac{1}{\sqrt 2 }p_x - \frac{1}{\sqrt {12} }d_{z^2}
+ \frac{1}{2}d_{x^2-y^2},$

$\frac{1}{\sqrt 6 }s - \frac{1}{\sqrt 2 }p_y
- \frac{1}{\sqrt {12} }d_{z^2} - \frac{1}{2}d_{x^2-y^2},
$

$\frac{1}{\sqrt 6 }s + \frac{1}{\sqrt 2 }p_y
- \frac{1}{\sqrt {12} }d_{z^2} - \frac{1}{2}d_{x^2-y^2},
$

$\frac{1}{\sqrt 6 }s - \frac{1}{\sqrt 2 }p_z + \frac{1}{\sqrt 3 }d_{z^2},
\frac{1}{\sqrt 6 }s + \frac{1}{\sqrt 2 }p_z + \frac{1}{\sqrt 3 }d_{z^2}$ |

**K grid mesh and b vectors connecting neighboring k-points**

<a id="3107"></a>
<a id="3110"></a>
<a id="3112"></a>
The Monkhorst-Pack **k** grid mesh is defined by the keyword
'Wannier.Kgrid'.
There is no default setting for it. To use finite difference approach
for calculating k-space differentials, b vectors connecting
neighboring k points are searched shell by shell according to the
distance from a central **k** point. The maximum number of searched
shells is defined by keyword 'Wannier.MaxShells'.
The default value is 12 and it should be increased if failure in finding a set
of proper b vectors. The problem may happen in case of
a system having a large aspect ratio among unit vectors, and
in this case you will see an error message, while the value 12
works well in most cases.
A proper setting of 'Wannier.Kgrid'
will also help to
find b vectors, where the grid spacing by the
discretization for each reciprocal lattice vector should be nearly
equivalent to each other.

```text

   Wannier.MaxShells          12           # default value is 12. 
   Wannier.Kgrid           8  8  8         # no default value
```

**Minimizing spread of WF**

<a id="3119"></a>
<a id="3120"></a>
<a id="3121"></a>
For entangled band case [[123](bibliography.md#mlwf2)], two steps are needed to
find the MLWFs. The first step is to minimize the gauge
invariant part of spread function by disentangling the
non-isolated bands. The second step is the same as isolated
band case [[122](bibliography.md#mlwf1)]. The gauge dependent part is optimized
by unitary transformation of the selected Bloch wave functions
according to the gradient of spread function.
For the first step, three parameters are used to control
the self-consistence loop. They are
'Wannier.Dis.SCF.Max.Steps',
'Wannier.Dis.Conv.Criterion',
and 'Wannier.Dis.Mixing.Para'.
They are the maximum number of SCF loops, the convergence criterion,
and the parameter to control the mixing of input and output
subspace projectors, respectively.

```text

    Wannier.Dis.SCF.Max.Steps         2000         # default 200
    Wannier.Dis.Conv.Criterion        1e-12        # default 1e-8
    Wannier.Dis.Mixing.Para           0.5          # default value is 0.5
```

<a id="3124"></a>
<a id="3125"></a>
<a id="3126"></a>
<a id="3127"></a>
<a id="3128"></a>
<a id="3129"></a>
For the second step, three minimization methods are available.
One is a steepest decent (SD) method, and the second one is
a conjugate gradient (CG) method. The third one is a hybrid
method which uses the SD method firstly and then switches
to the CG method. The keyword
'Wannier.Minimizing.Scheme'
indicates which method to be used. '0', '1', and '2' mean
the simple SD method, the CG method, and hybrid method, respectively.
The step length for the SD method is set by the keyword
'Wannier.Minimizing.StepLength'.
In the CG method, a secant method is used to determine the optimized
step length. The maximum secant steps and initial step length
is specified by 'Wannier.Minimizing.Secant.Steps'
and 'Wannier.Minimizing.Secant.StepLength',
respectively.
The maximum number of minimization step and convergence criterion
are controlled by 'Wannier.Minimizing.Max.Steps' and
'Wannier.Minimizing.Conv.Criterion', respectively.

```text

   Wannier.Minimizing.Scheme             2     # default 0, 0=SD 1=CG 2=hybrid 
   Wannier.Minimizing.StepLength        2.0    # default 2.0
   Wannier.Minimizing.Secant.Steps       5     # default 5      
   Wannier.Minimizing.Secant.StepLength 2.0    # default 2.0
   Wannier.Minimizing.Conv.Criterion   1e-12   # default 1e-8
   Wannier.Minimizing.Max.Steps         200    # default 200
```

<a id="3132"></a>
In the hybrid minimization scheme, SD and CG have the same number of maximum
minimization steps as specified by
'Wannier.Minimizing.Max.Steps'.

**Restarting optimization without calculating overlap matrix**

<a id="3137"></a>
If the overlap matrix
$M_{mn}^{({\rm {\bf k}},{\rm {\bf b}})}$ has been
calculated and stored in a disk file, the keyword
'Wannier.Readin.Overlap.Matrix'
can be set as 'on' to restart
generating MLWF without calculating
$M_{mn}^{({\rm {\bf k}},{\rm {\bf b}})}$
again.

```text

    Wannier.Readin.Overlap.Matrix       off      # default is on
```

This can save the computational time since the calculation
of overlap matrix is time consuming.
The code will read the overlap matrix as well as the
eigenenergies and states from the disk file.
One should keep in mind that the outer window and k grid
should be the same as those used for calculating the stored
overlap matrix and eigenvalues.
The consistency will be checked in the code.
The inner window, initial guess of MLWF as well as the
convergence criteria can be
adjusted for restarting optimization.
If 'Wannier.Readin.Overlap.Matrix' is
set as 'off', the overlap matrix will be calculated and
automatically stored into a disk file. The file name is defined
by 'System.Name' with an file extension '.mmn'. The eigenenergies
and states are also stored in the disk file with extension '.eigen'.
