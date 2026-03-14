<a id="SECTION000333000000000000000"></a>
## Electro-static potential fitting

For small molecular systems, the electro-static potential (ESP) fitting
method [[109](bibliography.md#Singh),[110](bibliography.md#Chirlian),[111](bibliography.md#Besler)] is useful to determine an effective
charge of each atom, while the ESP fitting method cannot be applied
for large molecules and bulk systems, since there are not enough
sampling points for atoms far from surface areas in the ESP fitting method.
In the ESP fitting method an effective net point charge on each atom
is determined by a least square method with constraints so that
the sum of the electro-static potential by effective point charges
can reproduce electro-static potential calculated by the DFT calculation
as much as possible.
The ESP fitting charge is calculated by the following
two steps:

**(1) SCF calculation**

After finishing a usual SCF calculation, you have two output files:

```text

    System.Name.out
    System.Name.vhart.cube
```

There is no additional keyword to generate the two files which
are default output files by the SCF calculation, while
the keyword 'level.of.fileout' should be 1 or 2.

**(2) ESP fitting charge**

Let us compile a program code for calculating the ESP fitting charge.
Move to the directory 'source' and then compile as follows:

```text

    % make esp
```

When the compilation is completed normally, then you can find
an executable file 'esp' in the directory 'work'.
The ESP fitting charge can be calculated from two files
'*System.Name*.out' and '*System.Name*.vhart.cube' using the program 'esp'. For example,
you can calculate them for a methane molecule shown in
the Section 'Input file' as follows:

```text

    % ./esp met -c 0 -s 1.4 2.0
```

Then, it is enough to specify the file name without the file extension,
however, two files 'met.out' and 'met.vhart.cube' must exist
in the directory 'work'. The options '-c' and '-s' are key parameters
to specify a constraint and scale factors. You can find the following
statement in the header part of a source code 'esp.c':

```text

   -c      constraint parameter 
           '-c 0' means charge conservation 
           '-c 1' means charge and dipole moment conservation  
   -s      scale factors for vdw radius
           '-s 1.4 2.0' means that 1.4 and 2.0 are 1st and 2nd scale factors
```

In the ESP fitting method, we support two constraints, charge conservation
and, charge and dipole moment conservation. Although the latter can reproduce
charge and dipole moment calculated by the DFT calculation, it seems that
the introduction of the dipole moment conservation gives often physically
unacceptable point charges especially for a relatively large molecule.
Thus, we would like to recommend the former constraint.
The sampling points are given by the grids in real space between two
shells of the first and second scale factors times
van der Waals radii [[112](bibliography.md#WebElements)]. In the above example, 1.4 and 2.0
correspond to the first and second scale factors.
The calculated result appears in the standard output (your display) as
follows:

```text

 % ./esp met -c 0 -s 1.4 2.0

******************************************************************
******************************************************************
 esp: effective charges by a ESP fitting method
 Copyright (C), 2004, Taisuke Ozaki 
 This is free software, and you are welcome to         
 redistribute it under the constitution of the GNU-GPL.
******************************************************************
******************************************************************

Constraint: charge 
Scale factors for vdw radius    1.40000    2.00000
Number of grids in a van der Waals shell = 28464
Volume per grid =    0.0235870615 (Bohr^3)
Success

  Atom=   1  Fitting Effective Charge= -0.93558216739
  Atom=   2  Fitting Effective Charge=  0.23389552572
  Atom=   3  Fitting Effective Charge=  0.23389569182
  Atom=   4  Fitting Effective Charge=  0.23389535126
  Atom=   5  Fitting Effective Charge=  0.23389559858

  Magnitude of dipole moment    0.0000015089 (Debye)
  Component x y z     0.0000003114   -0.0000002455   -0.0000014558
RMS between the given ESP and fitting charges (Hartree/Bohr^3)= 0.096515449505
```
