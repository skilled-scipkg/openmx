<a id="SECTION000442000000000000000"></a>
## Step 1: The calculations for leads

<a id="2549"></a>
<a id="2550"></a>
The calculation of the step 1 is the conventional band structure calculation
to construct information of the lead except for adding the following
two keywords 'NEGF.output_hks' and
'NEGF.filename.hks':

```text

    NEGF.output_hks    on
    NEGF.filename.hks  lead-chain.hks
```

The calculated results such as Hamiltonian matrix elements,
charge distribution, and difference Hartree potential are stored in
a file specified by the keyword 'NEGF.filename.hks'.
In this case,
a file 'lead-chain.hks' is generated. The file '*NEGF.filename.hks*' is used in the
calculation of the step 2.
Since the electronic transport is assumed to be along the **a**-axis
in the current implementation, you have to set the **a**-axis for
the direction of electronic transport in the band structure calculation.
However, you do not need rotate your structure. All you have to do is
to change the specification of the lattice vectors. For example,
if you want to specify a vector (0.0, 0.0, 10.0) as the **a**-axis in the
following lattice vectors:

```text

      <Atoms.UnitVectors                     
        3.0  0.0  0.0
        0.0  3.0  0.0
        0.0  0.0 10.0
      Atoms.UnitVectors>
```

you only have to specify as follows:

```text

      <Atoms.UnitVectors                     
        0.0  0.0 10.0
        3.0  0.0  0.0
        0.0  3.0  0.0
      Atoms.UnitVectors>
```

Then, the direction of (0.0, 0.0, 10.0) becomes the direction of electronic transport.
As shown in the above example, when you change the order of the lattice vectors,
please make sure that the keyword 'scf.Kgrid' has to be changed as well.

In the calculation of the step 2, the semi-infiniteness of the leads is taken into
account by using the surface Green function which allows us to treat
the semi-infiniteness without introducing any discretization.
Thus, it would be better to use a large number of **k**-points
along the **a**-axis
to keep the consistency between the steps 1 and 2 with respect to
treatment of the semi-infiniteness of the **a**-axis.
Also it is noted that the number of **k**-points for the **bc**-plane should
be consistent in the steps 1 and 2.
