<a id="SECTION000212000000000000000"></a>
## For calculations with lots of k-points

Since the calculation of density of states (DOS) of a large-scale system
with lots of k-points requires a considerable memory size, the post-processing
code 'DosMain' for generating the partial and total DOS tends to suffer from
a segmentation fault. For such a case, a Gaussian DOS scheme is available in
which the partial DOS is calculated by the Gaussian broadening method in the
OpenMX on-the fly calculation and the information of wave functions is not
stored in the file '*System.Name*.Dos.vec'. Since this scheme does not require a large
sized memory, it can be used to calculate DOS of large-scale systems.
Then, you can specify the following keywords in your input file as

```text

     DosGauss.fileout      on       # default=off, on|off
     DosGauss.Num.Mesh    200       # default=200
     DosGauss.Width       0.2       # default=0.2 (eV)
```

When you use the scheme, please specify 'on' for the keyword
'DosGauss.fileout'.
The keyword 'DosGauss.Num.Mesh' gives the number of partitioning for
the energy range specified by the keyword 'Dos.Erange'.
The keyword 'DosGauss.Width' gives a parameter $a$, which is the width of
the Gaussian defined by
$\exp( -(E/a)^2 )$.
The keyword 'DosGauss.fileout'
and the keyword 'Dos.fileout' are mutually exclusive.
Therefore, when you use the scheme, the keyword 'Dos.fileout' must be 'off' as follows:

```text

     Dos.fileout          off       # on|off, default=off
```

Also, the following two keywords are valid for both
the keywords 'Dos.fileout'
and 'DosGauss.file'.

```text

     Dos.Erange       -20.0  20.0   # default=-20 20 
     Dos.Kgrid           5 5 5      # default=Kgrid1 Kgrid2 Kgrid3
```

It should be noted that the keyword 'DosGauss.fileout'
generates only the Gaussian
broadening DOS, which means that DOS by the tetrahedron method cannot be calculated
by the keyword 'DosGauss.fileout'.
After the OpenMX calculation with these keywords,
the procedure for 'DosMain' is the same as in the conventional scheme.
