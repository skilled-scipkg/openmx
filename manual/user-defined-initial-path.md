<a id="SECTION000505000000000000000"></a>
## User defined initial path

As default, the initial path connecting the precursor and the product
is a straight line connecting them. However, in some cases the geometrical
structure of images generated on the straight line can be very erratic
so that distance between atoms can be too close to each other.
In this case, one should explicitly provide the atomic coordinates of images.
The user defined initial path can be provided by the same way as for the
restarting. Then, one has to provide atomic coordinates for each image
by the following keywords:

```text

  <NEB1.Atoms.SpeciesAndCoordinates
  1   Si   -0.12960866043083    0.13490502997627   -0.12924862991035     2.0     2.0
  2   Si   -0.40252421446808    5.19664433048606    4.91248322056082     2.0     2.0
  ...
  NEB1.Atoms.SpeciesAndCoordinates>

  <NEB2.Atoms.SpeciesAndCoordinates
  1   Si   -0.08436294149342   -0.02173837971883   -0.08374099211565     2.0     2.0
  2   Si   -0.33677725120015    5.10216241168093    5.01087499461541     2.0     2.0
  ...
  NEB2.Atoms.SpeciesAndCoordinates>
```

<a id="3552"></a>
For all the images of which number is given by 'MD.NEB.Number.Images',
the atomic coordinates need to be provided.
Also, it is required for a keyword to be switched on as

```text

  scf.restart     on
```

---
