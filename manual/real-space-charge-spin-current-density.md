<a id="SECTION000444200000000000000"></a>
### Real-space charge/spin current density

<a id="2758"></a>
In the step 3, real-space charge/spin current density is
calculated optionally.
The relevant keyword for the calculation is as follows:

```text

NEGF.tran.CurrentDensity   on        #  default on
```

- `NEGF.tran.CurrentDensity`
  If `NEGF.tran.CurrentDensity` is set to `on`,
  the real-space current density is calculated.

In the calculation of the current density, `openmx` makes the following standard output:

```text

Start Calculation of the currentdensity

  Spin #0
    Sum of current in real space [a.u.] 
      Left(ideal) :    -9.10585e-06
      Right(ideal):    -9.10583e-06
      Left(truncated ):    -8.66971e-06
      Right(truncated):    -8.69926e-06
  Spin #1
    Sum of current in real space [a.u.] 
      Left(ideal) :    -4.54540e-08
      Right(ideal):    -4.54544e-08
      Left(truncated ):    -4.19469e-08
      Right(truncated):    -4.27460e-08

Output: Currentdensity
  Charge-current density along a-axis: ./negf-8zgnr-0.3.curden1.cube
  Spin-current density along a-axis: ./negf-8zgnr-0.3.scurden1.cube
  Charge-current density: ./negf-8zgnr-0.3.curden.xsf
  Spin-current density: ./negf-8zgnr-0.3.scurden.xsf
  Voronoi Charge-current density: ./negf-8zgnr-0.3.curden_atom.xsf
  Voronoi Spin-current density: ./negf-8zgnr-0.3.scurden_atom.xsf
```

In this case, 6 files:

`negf-8zgnr-0.3.curden.xsf`, `negf-8zgnr-0.3.scurden.xsf`,

`negf-8zgnr-0.3.curden1.cube`, `negf-8zgnr-0.3.scurden1.cube`,

`negf-8zgnr-0.3.curden_atom.xsf`, `negf-8zgnr-0.3.scurden_atom.xsf`,

are generated.
These files contain the following quantities:

- *System.Name*`.curden.xsf`, *System.Name*`.scurden.xsf`
  These files contain the charge and the spin current densities, respectively,
  on the real space grid. They can be visualized using 'Display$\to $Forces' in XCrySDen.
- *System.Name*`.curden1.cube`, *System.Name*`.scurden1.cube`
  These files contain the **a**-component of the charge and the spin current densities, respectively,
  on real space grid. They can be visualized using VESTA, XCrySDen, and so on.
- *System.Name*`.curden_atom.xsf`, *System.Name*`.scurden_atom.xsf`
  These files contain the charge and the spin current density respectively
  averaged in Voronoi polyhedra of each atom.
  They can be visualized using 'Display$\to $Forces' in XCrySDen.

<a id="2774"></a>
(Experimentally) When you set

```text

    NEGF.OffDiagonalCurrent   on        #  default off
```

in an input file for the calculation with the non-collinear magnetism,
the following files are outputted.

- *System.Name*`.odcurden_r.xsf`, *System.Name*`.odcurden_i.xsf`
- *System.Name*`.odcurden1_r.cube`, *System.Name*`.odcurden1_i.cube`
- *System.Name*`.odcurden_atom_r.xsf`, *System.Name*`.odcurden_atom_i.xsf`

These files contain the spin off-diagonal component of the current density.
Since this quantity becomes generally a complex number,
the real part and the imaginary part of that is output separately.
As an example, we show in Fig. [42](real-space-charge-spin-current-density.md#fig:CurDensity) the currentdensity in the 8-zigzag graphene nanoribbon with
an antiferromagnetic junction under a finite bias voltage of 0.3 V.
In the vicinity of boundaries, that shows an unphysical behavior
because the basis set is not treated correctly in these regions.
If you want to calculate more precisely the current density in these regions,
please make a supercell larger.

<a id="fig:CurDensity"></a>
<a id="6331"></a>
| ![\includegraphics[width=14.0cm]{CurDensity.eps}](assets/img297.png) |
| --- |
