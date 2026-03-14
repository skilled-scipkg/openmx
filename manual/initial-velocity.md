<a id="SECTION000186000000000000000"></a>
## Initial velocity

<a id="1190"></a>
For molecular dynamics simulations, it is possible to provide the initial
velocity of each atom by the following keyword:

```text

  <MD.Init.Velocity
   1    3000.000  0.0  0.0
   2   -3000.000  0.0  0.0
  MD.Init.Velocity>
```

The example is for a system consisting of two atoms. If you have $N$ atoms,
then you have to provide $N$ rows in this specification.
The 1st column is the same sequential number to specify atom as in the
specification of the keyword
'Atoms.SpeciesAndCoordinates'.
The 2nd, 3rd, and 4th columns are $x$-, $y$-, and $z$-components of the velocity
of each atom, respectively. The unit of the velocity is m/s.
The keyword 'MD.Init.Velocity'
is compatible with the keyword 'MD.Fixed.XYZ'.

---
