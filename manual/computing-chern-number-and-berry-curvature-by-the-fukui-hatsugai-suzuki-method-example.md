<a id="SECTION000562000000000000000"></a>
## Example

As an example, we show in Fig. [74](computing-chern-number-and-berry-curvature-by-the-fukui-hatsugai-suzuki-method-example.md#fig:Chern-Fig2) the Berry curvature of graphene.
Since the absolute magnitude of Berry curvature is approximately proportional to the square of inverse of bandgap,
the large Berry curvature can be seen around K and K' points, where the massive Dirac point appears
if we include spin-orbit interaction.

Let us illustrate how the calculation can be performed by using an input file 'Graphene-Chern.dat'
stored in the directory 'work'.

<a id="4568"></a>
**SCF calculation**

When you perform the SCF calculation for graphene using an input file 'Graphene-Chern.dat' stored
in the directory 'work', you need to switch on the keyword 'HS.fileout' as

```text

    HS.fileout      on      #on|off, default=off
```

After finishing the SCF calculation normally, we may obtain an out file 'Graphene-Chern.scfout'.

**Calculation of Chern number and Berry curvature**

Then, you can proceed for the calculation of the Chern number of Berry curvature using
a post-processing code 'calB.c'. The compilation of the code can be done in the director 'source' as

```text

    % make calB
```

After the compilation is successfuly, you obtain the executable file 'calB'.
Then, please copy it to the directory 'work', and execute it as follows:

```text

    % ./calB graphene.scfout
 or
    % ./calB graphene.scfout < calB.in > calB.out
 or
    % mpirun -np 4 ./calB graphene.scfout < calB.in > calB.out
```

**Parameters for calB**

The input file 'calB.in' needs to be prepared as follows:

```text

   1
   0
   0 0 1
   100 100
```

In the following we explain parameters for the calculation.

- In the first line, you need to specify whether the sum of the Berry curvature of all the bands is calculated, or the Berry curvature is calculated for a disentangled bands. If the former is selected, please set '1', while for the latter please set '0'. The latter setting is valid only if a set of bands are fully disentangled.
- In the second line, you need to specify how many bands are taken into account for the calculations, which are counted from the lowest band. If you specify '0', all the valence bands will be taken into account.
- In the third line, we specify planes to be calculated in the reciprocal space. For example, '0 0 1' corresponds to the specification of the $k_{3}=0$ plane.
- In the fourth line, you need to specify the number of mesh. In the example of graphene, the plane specified by the third line is discretized by a mesh of 100$\times $100.

**Output files**

After the calculation by 'calB', the following files are generated.

- BerryC*.dat
  The file stores the calculated Berry curvature and Chern number, where the '*' behind 'BerryC'
  in the file name is the number of bands to be included.
  In the example of graphene, '*' is 8.
  The unit of Berry curvature is Å$^{-2}$. The part of 'BerryC8.dat' for the graphene case is shown below:
  ```text

     #Mesh Number:100*100
     #Band Number:8
     #ChernNumber = 0.000000
     #k1          k2           F (ang-2)
     0.005000 0.005000 -1.59799534e-05
     0.015000 0.005000 1.94455630e-05
     0.025000 0.005000 3.58476883e-05
     ....
     ..
  ```
  Using gnuplot, one can visualize the data as
  ```text

      % splot "BerryC8.dat" w l
  ```
  Figure [74](computing-chern-number-and-berry-curvature-by-the-fukui-hatsugai-suzuki-method-example.md#fig:Chern-Fig2) shows the Berry curvature on the plane at $k_{3}=0$.
- temporal_12345.input
  This is a copy of input file, which was used for the SCF calculation, reconstructed from the scfout file.

<a id="fig:Chern-Fig2"></a>
<a id="4601"></a>
| ![\includegraphics[width=13.0cm]{Chern-Fig2.eps}](assets/img462.png) |
| --- |
