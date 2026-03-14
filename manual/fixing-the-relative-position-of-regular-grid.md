<a id="SECTION000133000000000000000"></a>
## Fixing the relative position of regular grid

OpenMX Ver. 3.9 uses the regular real space grid for the evaluation of
Hamiltonian matrix elements associated with the Hartree potential by the difference
charge density and exchange-correlation potential, and solution of Poisson's equation.
Thus, the total energy depends on the relative position between atomic coordinates
and the regular grid. When one calculates an interaction energy or energy curve
as a function of atomic coordinates, it is quite important to keep the relative
position in all the calculations required for the evaluation of the interaction energy.
In the calculation for one of the structures,
you will find 'Grid_Origin' in the standard output which gives $x$-, $y$-,
and $z$-components of the origin of the regular grid as:

```text

       Grid_Origin  xxx  yyy  zzz
```

Then, in order to keep the relative position, you have to include the following keyword
'scf.fixed.grid' in your input file
for all the systems in the calculations
required for the evaluation of the interaction energy:

```text

      scf.fixed.grid  xxx  yyy  zzz
```

where 'xxx yyy zzz' is the coordinate of the origin you got in the calculation
for one of the structures. The procedure largely suppresses the numerical error
involved in the use of the regular grid.
In addition, as discussed in the previous subsection
'A tip for calculating the energy curve for bulks', the number of grids should
be fixed by the keyword 'scf.Ngrid' when the lattice parameters are also changed
in the evaluation of interaction energy.
