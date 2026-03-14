<a id="SECTION000411000000000000000"></a>
## Zeeman term for spin magnetic moment

The Zeeman term for spin magnetic moment is available as an interaction
with a uniform magnetic field by the following keywords:

```text

      scf.NC.Zeeman.Spin           on        # on|off, default=off
      scf.NC.Mag.Field.Spin       100.0      # default=0.0(Tesla)
```

When you include the Zeeman term for spin magnetic moment, switch on the keyword
'scf.NC.Zeeman.Spin'.
The magnitude of the uniform magnetic field can be specified
by the keyword 'scf.NC.Mag.Field.Spin'
in units of Tesla.
Moreover, we extend the scheme as a constraint scheme in which the direction of
the magnetic field can be different from each atomic site atom by atom.
Then, the direction of magnetic field for spin magnetic moment can be controlled,
for example, by the keyword:
'Atoms.SpeciesAndCoordinates'

```text

  <Atoms.SpeciesAndCoordinates           
   1  Sc  0.000  0.000  0.000   6.6 4.4  10.0 50.0  160.0 20.0  1  on
   2  Sc  2.000  0.000  0.000   6.6 4.4  80.0 50.0  160.0 20.0  1  on
  Atoms.SpeciesAndCoordinates>
```

The 8th and 9th columns give the Euler angles, $\theta$ and $\phi$, in order to specify
the magnetic field for spin magnetic moment. The 12th column is a switch to the constraint.
'1' means that the constraint is applied, and '0' no constraint.
Since for each atomic site a different direction of the magnetic field can be applied,
this scheme provides a way of studying non-collinear spin configuration. It is noted that the
keyword 'scf.NC.Zeeman.Spin'
and the keyword 'scf.Constraint.NC.Spin'
are mutually exclusive.
Therefore, when 'scf.NC.Zeeman.Spin' is 'on',
the keyword 'scf.Constraint.NC.Spin'
must be switched off as follows:

```text

      scf.Constraint.NC.Spin       off       # on|off, default=off
```

Although the Zeeman term and the constraint scheme for spin orientation can be regarded
as ways for controlling the spin orientation, it is noted that the magnitude of spin magnetic
moment by the Zeeman term tends to be enhanced unlike the constraint scheme.
