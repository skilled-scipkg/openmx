<a id="SECTION000161000000000000000"></a>
## Steepest decent optimization

An example of the geometry optimization is illustrated in this Section.
As an initial structure, let us consider the methane molecule given
in the Section 'Input file', but the $x$-coordinate of the carbon atom
of the methane molecule is moved to 0.3 Å as follows:

```text

   <Atoms.SpeciesAndCoordinates
     1   C      0.300000    0.000000    0.000000     2.0  2.0 
     2   H     -0.889981   -0.629312    0.000000     0.5  0.5
     3   H      0.000000    0.629312   -0.889981     0.5  0.5
     4   H      0.000000    0.629312    0.889981     0.5  0.5
     5   H      0.889981   -0.629312    0.000000     0.5  0.5
   Atoms.SpeciesAndCoordinates>
```

Then, a keyword 'MD.type' is specified as 'Opt', and set to 200
for a keyword 'MD.maxIter'. The 'Opt' is based on a simple steepest
decent method with a variable prefactor.
Figure 8 (a) shows the convergence history of the norm of the maximum
force on atom as a function of the number of the optimization steps.
We see that the norm of the maximum force on atom converges after the structure
overshot the stationary point because of change of the prefactor.
Using 'Methane2.dat' in the directory 'work', you can trace the calculation.
As well as the case of the methane molecule, a similar behavior can be seen for
the silicon diamond as shown in Fig. [9](steepest-decent-optimization.md#fig:GeoOpt1)(b).

<a id="fig:GeoOpt1"></a>
<a id="965"></a>
| ![\includegraphics[width=12.0cm]{GeoOpt1.eps}](assets/img128.png) |
| --- |
