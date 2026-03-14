<a id="SECTION000503000000000000000"></a>
## Examples and keywords

Two input files are provided as example:

- C2H4_NEB.dat
  Cycloaddition reaction of two ethylene molecules to cyclobutane
- Si8_NEB.dat
  Diffusion of an interstitial hydrogen atom in the diamond Si

The input file 'C2H4_NEB.dat' will be used to illustrate the NEB calculation
in the proceeding explanation.

**Providing two terminal structures**

The atomic coordinates of the precursor are specified in the input file by

```text

  <Atoms.SpeciesAndCoordinates
  1    C   -0.66829065594143    0.00000000101783   -2.19961193219289     2.0     2.0
  2    C    0.66817412917689   -0.00000000316062   -2.19961215251205     2.0     2.0
  3    H    1.24159214112072   -0.92942544650857   -2.19953308980064     0.5     0.5
  4    H    1.24159212192367    0.92942544733979   -2.19953308820323     0.5     0.5
  5    H   -1.24165800644131   -0.92944748269232   -2.19953309891389     0.5     0.5
  6    H   -1.24165801380425    0.92944749402510   -2.19953309747076     0.5     0.5
  7    C   -0.66829065113509    0.00000000341499    2.19961191775648     2.0     2.0
  8    C    0.66817411530651   -0.00000000006073    2.19961215383949     2.0     2.0
  9    H    1.24159211310925   -0.92942539308841    2.19953308889301     0.5     0.5
  10    H    1.24159212332935    0.92942539212392    2.19953308816332     0.5     0.5
  11    H   -1.24165799549343   -0.92944744948986    2.19953310195071     0.5     0.5
  12    H   -1.24165801426648    0.92944744880542    2.19953310162389     0.5     0.5
  Atoms.SpeciesAndCoordinates>
```

The atomic coordinates of the product are specified in the input file by

```text

  <NEB.Atoms.SpeciesAndCoordinates
  1    C   -0.77755846408657   -0.00000003553856   -0.77730141035137     2.0     2.0
  2    C    0.77681707294741   -0.00000002413166   -0.77729608216595     2.0     2.0
  3    H    1.23451821718817   -0.88763832172374   -1.23464057728123     0.5     0.5
  4    H    1.23451823170776    0.88763828275851   -1.23464059022330     0.5     0.5
  5    H   -1.23506432458023   -0.88767426830774   -1.23470899088096     0.5     0.5
  6    H   -1.23506425800395    0.88767424658723   -1.23470896874564     0.5     0.5
  7    C   -0.77755854665393    0.00000000908006    0.77730136931056     2.0     2.0
  8    C    0.77681705017323   -0.00000000970885    0.77729611199476     2.0     2.0
  9    H    1.23451826851556   -0.88763828740000    1.23464060936812     0.5     0.5
  10    H    1.23451821324627    0.88763830875131    1.23464061208483     0.5     0.5
  11    H   -1.23506431230451   -0.88767430754577    1.23470894717613     0.5     0.5
  12    H   -1.23506433587007    0.88767428525317    1.23470902573029     0.5     0.5
  NEB.Atoms.SpeciesAndCoordinates>
```

**Keywords for the NEB calculation**

<a id="3495"></a>
The NEB calculation can be performed by setting the keyword 'MD.Type' as

```text

  MD.Type                NEB
```

<a id="3499"></a>
The number of images in the path is given by

```text

  MD.NEB.Number.Images        8            # default=10
```

where the two terminals are excluded from the number of images.

<a id="3503"></a>
The spring constant is given by

```text

  MD.NEB.Spring.Const         0.1          # default=0.1(hartee/borh^2)
```

In most cases, the obtained path does not largely depend on the value.

<a id="3507"></a>
<a id="3508"></a>
<a id="3509"></a>
<a id="3510"></a>
The optimization of MEP is performed by a hybrid DIIS+BFGS scheme which is
controlled by the following keywords:

```text

  MD.Opt.DIIS.History           4          # default=7
  MD.Opt.StartDIIS             10          # default=5
  MD.maxIter                  100          # default=1
  MD.Opt.criterion         1.0e-4          # default=1.0e-4 (Hartree/Bohr)
```

The specification of these keywords are the same as for the geometry optimization.
So, see the section 'Geometry optimization' in the manual for the details.
Also, it is also possible to fix the atomic position by the keyword 'MD.Fixed.XYZ'.

**Execution of the NEB calculation**

One can perform the NEB calculation with the input file 'C2H4_NEB.dat' by

```text

  % mpirun np 16 openmx C2H4_NEB.dat
```

If the calculation is successfully completed, more than 24 files will be
generated. Some of them are listed below:

```text

  c2h4.neb.opt          history of optimization for finding MEP
  c2h4.neb.ene          total energy of each image             
  c2h4.neb.xyz          atomic coordinates of each image in XYZ format
  C2H4_NEB.dat#         input file for restarting. 
  C2H4_NBE.dat_0        input file for the precursor 
  C2H4_NBE.dat_1        input file for the image 1
  C2H4_NBE.dat_2        input file for the image 2  
  C2H4_NBE.dat_3        input file for the image 3
  C2H4_NBE.dat_4        input file for the image 4
  C2H4_NBE.dat_5        input file for the image 5
  C2H4_NBE.dat_6        input file for the image 6
  C2H4_NBE.dat_7        input file for the image 7
  C2H4_NBE.dat_8        input file for the image 8 
  C2H4_NBE.dat_9        input file for the product
  c2h4_0.out            output file for the precursor 
  c2h4_1.out            output file for the image 1
  c2h4_2.out            output file for the image 2
  c2h4_3.out            output file for the image 3
  c2h4_4.out            output file for the image 4
  c2h4_5.out            output file for the image 5
  c2h4_6.out            output file for the image 6
  c2h4_7.out            output file for the image 7
  c2h4_8.out            output file for the image 8
  c2h4_9.out            output file for the product
```

'c2h4.neb.opt' contains history of optimization for finding MEP
as shown in Fig. [53](example-of-test-calculation.md#fig:ESM2)(a). One can see the details
at the header of the file as follows:

```text

  ***********************************************************
  ***********************************************************
  History of optimization by the NEB method
  ***********************************************************
  ***********************************************************

  iter   SD_scaling     |Maximum force|   Maximum step        Norm        Sum of Total Energy of Images
  (Hartree/Bohr)        (Ang)       (Hartree/Bohr)       (Hartree)

  1       0.37794520       0.12552539       0.04583072       0.49503563      -223.77727271
  2       0.37794520       0.08684953       0.03163814       0.35379139      -223.85742175
  3       0.37794520       0.05494411       0.01922344       0.25668987      -223.89831309
  4       0.37794520       0.03790970       0.01234783       0.20282699      -223.92042217
  5       0.45353424       0.02936250       0.01326992       0.17349184      -223.93482686
  6       0.45353424       0.02588308       0.01169327       0.15249816      -223.94772371
  7       0.45353424       0.02303223       0.01039732       0.13836350      -223.95785384
  .....
  ...
  .
```

Also, 'c2h4.neb.ene' and 'c2h4.neb.xyz' can be used
to analyze the change of total energy as a function of
the distance (Bohr) from the precursor and the structural change as
shown in Fig. [57](examples-and-keywords.md#fig:NEB1)(b). The content of 'c2h4.neb.ene' is
as follows:

```text

  #
  # 1st column: index of images, where 0 and MD.NEB.Number.Images+1 are the terminals
  # 2nd column: Total energy (Hartree) of each image
  # 3rd column: distance (Bohr) between neighbors
  # 4th column: distance (Bohr) from the image of the index 0
  #
    0     -28.02185123       0.00000000       0.00000000       1.33646479
    1     -28.02178507       0.82118927       0.82118927       1.33567761
    2     -28.02140083       0.82112464       1.64231391       1.33523542
    3     -28.02029258       0.82111520       2.46342911       1.33463918
    4     -28.01779519       0.82113225       3.28456136       1.33375873
    5     -28.01261498       0.82135735       4.10591871       1.33262670
    6     -27.98761576       0.82169347       4.92761218       1.34184319
    7     -27.91797754       0.82218705       5.74979923       1.51281867
    8     -28.02565242       0.82256542       6.57236464       1.55582513
    9     -28.06263668       0.82263897       7.39500361       1.55437554
```

where the first column is a serial number of image, while 0 and 9 correspond to
the precursor and product, respectively. The second column is the total energy
of each image.
The third and fourth columns are interval (Bohr) between two neighboring images and
the distance (Bohr) from the precursor in geometrical phase space.

<a id="fig:NEB1"></a>
<a id="3532"></a>
| ![\includegraphics[width=16.5cm]{NEB1.eps}](assets/img398.png) |
| --- |

A file '*System.Name*.dat_#', where '*System.Name*' is 'System.Name' and '#' is a serial number for each image, is
also generated, since each calculation for each image is basically done
as an independent OpenMX calculation with a different input file.
A corresponding output file '*System.Name*_#.out' is also generated, which may be useful
to analyze how the electronic structure changes on MEP.

As well as the case of 'C2H4_NEB.dat', one can perform the NEB calculation by
'Si8_NEB.dat'. After the successful calculation, you may get the history of optimization
and change of total energy along MEP as shown in Fig. [58](examples-and-keywords.md#fig:NEB2).

<a id="fig:NEB2"></a>
<a id="3543"></a>
| ![\includegraphics[width=16.5cm]{NEB2.eps}](assets/img399.png) |
| --- |
