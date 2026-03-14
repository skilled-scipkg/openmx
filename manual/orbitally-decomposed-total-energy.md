<a id="SECTION000220000000000000000"></a>
# Orbitally decomposed total energy

<a id="1331"></a>
OpenMX Ver. 3.9 provides a useful tool which decomposes the total energy into each contribution
associated with each basis function, where the decomposition is performed based on projection
onto basis functions [[68](bibliography.md#EnergyDecomposition)].
To calculate the orbitally decomposed total energy,
you only have to include the following keyword:

```text

    Energy.Decomposition      on        # on|off, default=off
```

Let us illustrate the energy decomposition by performing a total energy calculation of a methane molecule.
The calculation as an example can be performed as follows:

```text

     % mpirun -np 5 openmx Methane_ED.dat > met_ed.std &
```

where the input file 'Methane_ED.dat' can be found in the directory 'work'.
After finishing the calculation, you may obtain 'met_ed.out'. The part of the file is shown below:

```text

*************************************************************************
*************************************************************************
            Decomposed energies in Hartree unit

   Utot = Utot(up) + Utot(dn)
        = Ukin(up) + Ukin(dn) + Uv(up) + Uv(dn)
        + Ucon(up)+ Ucon(dn) + Ucore+UH0 + Uvdw

   Uele = Ukin(up) + Ukin(dn) + Uv(up) + Uv(dn)
   Ucon arizes from a constant potential added in the formalism

           up: up spin state, dn: down spin state
*************************************************************************
*************************************************************************

  Total energy (Hartree) = -8.216132481346387

  Decomposed.energies.(Hartree).with.respect.to.atom

                 Utot              Utot(up)    Utot(dn)    Ukin(up)    Ukin(dn)    Uv(up)     ....
     1    C     -6.132295762765   -3.066148   -3.066148    2.076016    2.076016   -2.957459   ....
     2    H     -0.520959186503   -0.260480   -0.260480    0.300675    0.300675   -0.499086   ....
     3    H     -0.520959174111   -0.260480   -0.260480    0.300675    0.300675   -0.499086   ....
     4    H     -0.520959173764   -0.260480   -0.260480    0.300675    0.300675   -0.499086   ....
     5    H     -0.520959184204   -0.260480   -0.260480    0.300675    0.300675   -0.499086   ....

  Decomposed.energies.(Hartree).with.respect.to.atomic.orbital

    1    C          Utot        Utot(up)    Utot(dn)    Ukin(up)    Ukin(dn)    Uv(up)      
            multiple
  none             -4.483770   -2.241885   -2.241885    0.000000    0.000000    0.000000      .... 
  s           0    -0.675699   -0.337849   -0.337849    0.203145    0.203145   -0.556473      .... 
  s           1     0.003690    0.001845    0.001845    0.036240    0.036240   -0.034310      .... 
  px          0    -0.325884   -0.162942   -0.162942    0.496144    0.496144   -0.673031      .... 
  py          0    -0.325912   -0.162956   -0.162956    0.496166    0.496166   -0.673068      .... 
  pz          0    -0.325884   -0.162942   -0.162942    0.496144    0.496144   -0.673031      .... 
  px          1     0.005096    0.002548    0.002548    0.107318    0.107318   -0.104552      .... 
  ...
  ..
  .
```

It is found that the total energy is exactly decomposed to atomic and orbital contributions.
The energy decomposition method will be useful to analyze how local distortion such as impurities
and vacancies affects the energy stability/instability for the neighbors. It is also anticipated
that the orbital decomposition of the total energy allows us to analyze physical mechanism
for a wide variety of phenomena. However, the release of the functionality can be still regarded
as experimental one. We may develop and modify the functionality in the near future.
