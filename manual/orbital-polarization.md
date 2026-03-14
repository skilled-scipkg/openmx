<a id="SECTION000381300000000000000"></a>
### Orbital polarization

The DFT+$U$ functional possesses multiple minima in the degree of freedom of the orbital occupation,
leading to that the SCF calculation tends to be
trapped to some local minimum. To find the ground state with an orbital polarization, a way of enhancing
explicitly the orbital polarization is available by the following switch:

```text

  For collinear cases

  <Atoms.SpeciesAndCoordinates   # Unit=AU
    1 Ni 0.0     0.0     0.0     10.0 6.0  on
    2 Ni 3.94955 3.94955 0.0     6.0  10.0 on
    3 O  3.94955 0.0     0.0     3.0  3.0  on
    4 O  3.94955 3.94955 3.94955 3.0  3.0  on
  Atoms.SpeciesAndCoordinates>

  For noncollinear cases

  <Atoms.SpeciesAndCoordinates   # Unit=AU
    1 Ni 0.0     0.0     0.0     10.0 6.0  40.0 10.0 0 on
    2 Ni 3.94955 3.94955 0.0     6.0  10.0 40.0 10.0 0 on
    3 O  3.94955 0.0     0.0     3.0  3.0  10.0 40.0 0 on
    4 O  3.94955 3.94955 3.94955 3.0  3.0  10.0 40.0 0 on
  Atoms.SpeciesAndCoordinates>
```

The specification of each column can be found in the section `Non-collinear DFT'.
Since the enhancement treatment for the orbital polarization is performed on each atom, you have to set the switch
for all the atoms in the specification of atomic coordinates as given above. The enhancement for the atoms switched
on is applied during the first few self-consistent (SC) steps, then no more enhancement are required during the
subsequent SC steps. It is also emphasized that the enhancement does not always give the ground state,
and that it can work badly in some case (see Ref. [[20](bibliography.md#Han2)] for the details).
Also, we do not recommend turning on orbital polarization when using `scf.dc.Type=cFLL` and `cAMF`.

---
