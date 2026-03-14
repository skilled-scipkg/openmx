<a id="SECTION000332000000000000000"></a>
## Voronoi charge

Voronoi charge of each atom is calculated by integrating electron and
spin densities in a Voronoi polyhedron. The Voronoi polyhedron
is constructed from smeared surfaces which are defined by a Fuzzy cell
partitioning method [[69](bibliography.md#Becke)].
It should be noted that this Voronoi analysis gives often
overestimated or underestimated charge, since Voronoi polyhedron
is determined by only the structure without taking account of atomic radius.
If you want to calculate Voronoi charge, specify the following keyword
'Voronoi.charge' in your input file:

```text

     Voronoi.charge      on       # on|off, default = off
```

In case of a methane molecule, the following Voronoi charges are output
to '*System.Name*.out'.

```text

***********************************************************
***********************************************************
                     Voronoi charges                       
***********************************************************
***********************************************************

  Sum of Voronoi charges for up    =  4.000000290723
  Sum of Voronoi charges for down  =  4.000000290723
  Sum of Voronoi charges for total =  8.000000581446

  Total spin magnetic moment (muB) by Voronoi charges  =  0.000000000000

                     Up spin      Down spin     Sum           Diff       Voronoi Volume (Ang.^3)
       Atom=   1   1.129270484  1.129270484   2.258540969   0.000000000   2.355421391
       Atom=   2   0.717682452  0.717682452   1.435364903   0.000000000  62.245579466
       Atom=   3   0.717682452  0.717682452   1.435364903   0.000000000  62.245579466
       Atom=   4   0.717682452  0.717682452   1.435364903   0.000000000  62.245579466
       Atom=   5   0.717682451  0.717682451   1.435364903   0.000000000  62.245579466
```

Clearly, we see that carbon atom (Atom=1) and hydrogen atoms (Atom=2-5) are charged
positively and negatively, respectively, which apparently contradicts a usual chemical sense.
However, the Voronoi analysis could be a useful and complementary information
for a bulk system with a closed pack structure. Also, the Voronoi volume being
a supplemental information will be useful to analyze local structure for bulk systems.

---
