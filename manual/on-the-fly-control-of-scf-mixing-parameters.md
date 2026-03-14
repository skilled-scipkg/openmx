<a id="SECTION000143000000000000000"></a>
## On-the-fly control of SCF mixing parameters

During the SCF calculation, it is possible to change the following parameters for the SCF mixing:

```text

   scf.maxIter
   scf.Min.Mixing.Weight
   scf.Max.Mixing.Weight
   scf.Kerker.factor
   scf.Mixing.StartPulay
```

For example, when you specify the following two keywords in your input file as

```text

   System.CurrrentDirectory         ./    # default=./
   System.Name                      c60
```

then make a file whose name is 'c60_SCF_keywords' in the directory './', and write in it as

```text

   scf.maxIter                100
   scf.Min.Mixing.Weight      0.01
   scf.Max.Mixing.Weight      0.10
   scf.Kerker.factor          10.0
   scf.Mixing.StartPulay      30 
   scf.criterion              1.0e-6
```

OpenMX will try to read the file 'c60_SCF_keywords' at every SCF step, and show the following
message in the standard output, if the file is successfully read by OpenMX.

```text

   The keywords for SCF iteration are renewed by ./c60_SCF_keywords.
```

Also, if a minus value is given for the keyword 'scf.maxIter', then OpenMX will be terminated.
The on-the-fly control of SCF mixing parameters may be useful when large-scale calculations
are performed.

---
