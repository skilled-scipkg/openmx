<a id="SECTION000602000000000000000"></a>
## Si case

Let us illustrate the calculation using an input file 'Si2_k50x50x50.dat' stored in the directory 'work'.
The input file is for a calculation of Si bulk including 2 atoms in the unit cell, where
$10\times 10\times 10$ k-points
and
$50\times 50\times 50$ k-points are used for the SCF calculation and the calculation of conductivity, respectively.
One can perform the calculation as

```text

   % mpirun -np 112 ./openmx Si2_k50x50x50.dat
```

After finishing the SCF calculation normally, the relevant calculation
'$<$Optical calculation start$>$' starts as shown in the standard output below:

```text

  ******************* MD= 1  SCF=17 *******************
  <Poisson>  Poisson's equation using FFT...
  <Set_Hamiltonian>  Hamiltonian matrix for VNA+dVH+Vxc...
  <Band>  Solving the eigenvalue problem...
   KGrids1:  -0.45000  -0.35000  -0.25000  -0.15000  -0.05000   0.05000   0.15000 ....
   KGrids2:  -0.45000  -0.35000  -0.25000  -0.15000  -0.05000   0.05000   0.15000 ....
   KGrids3:  -0.45000  -0.35000  -0.25000  -0.15000  -0.05000   0.05000   0.15000 ....
  <Band_DFT>  Eigen, time=0.028573
  <Band_DFT>  DM, time=0.024604
      1   Si  MulP   2.0000  2.0000 sum   4.0000
      2   Si  MulP   2.0000  2.0000 sum   4.0000
   Sum of MulP: up   =     4.00000 down          =     4.00000
                total=     8.00000 ideal(neutral)=     8.00000
  <DFT>  Total Spin Moment (muB) =  0.000000000000
  <DFT>  Mixing_weight= 0.020000000000
  <DFT>  Uele   =   -2.418066179485  dUele     =   0.000000000118
  <DFT>  NormRD =    0.000000000011  Criterion =   0.000000001000

  <Optical calculation start>
   CDDF.KGrids1:  -0.49000  -0.47000  -0.45000  -0.43000  -0.41000  -0.39000  -0.37000 ....
   CDDF.KGrids2:  -0.49000  -0.47000  -0.45000  -0.43000  -0.41000  -0.39000  -0.37000 ....
   CDDF.KGrids3:  -0.49000  -0.47000  -0.45000  -0.43000  -0.41000  -0.39000  -0.37000 ....
  <Optical calculations end, time=24.31524 (s)>
  <MD= 1>  Force calculation
    Force calculation #1
    Force calculation #2
    Force calculation #3
    Force calculation #4
    Force calculation #5
  <MD= 1>  Total Energy
    Force calculation #6
    ....
    ...
```

In this case, it is found from the standard output that the computational time of the relevant calculation is about 24 second.
After all the calculations finish, you obtain the following output files relevant to the functionality:

```text

   Si2_k50x50x50.cd_re                 real part of optical conductivity tensor
   Si2_k50x50x50.cd_im                 imaginary part of optical conductivity tensor
   Si2_k50x50x50.df_re                 real part of dielectric function tensor
   Si2_k50x50x50.df_im                 imaginary part of dielectric function tensor
   Si2_k50x50x50.absorption            absorption tensor
   Si2_k50x50x50.extinction            extinction tensor   
   Si2_k50x50x50.transmission          transmission tensor 
   Si2_k50x50x50.reflection            reflection tensor    
   Si2_k50x50x50.refractive_index      refractive index tensor
```

<a id="fig:CDDF-Fig1"></a>
<a id="6455"></a>
| ![\includegraphics[width=16.6cm]{CDDF-Fig1.eps}](assets/img589.png) |
| --- |

The format of each file can be found in the header part of the file, where the unit for each physical quantity is also provided.
For example, 'Si2_k50x50x50.cd_re' storing the real part of optical conductivity tensor $\sigma$ can be seen as shown below:

```text

# conductivity tensor (real part) , unit = Siemens/meter = Mho/meter = 1/(Ohm*meter)
# index: energy-grid=1, xx=2, xy=3, xz=4, yx=5, yy=6, yz=7, zx=8, zy=9, zz=10, trace=11
#energy-grid(eV)     xx            xy            xz            yx            yy            yz            zx            zy            zz   (xx+yy+zz)/3
  0.00000  16877.3220211  -227.5621843  -227.5697597  -227.5625069  16877.3919038  -227.5042335  -227.5702078  -227.5041190  16877.3911375  16877.3683541
  0.00100  16877.3325817  -227.5625199  -227.5700960  -227.5628426  16877.4024628  -227.5045682  -227.5705442  -227.5044537  16877.4016971  16877.3789139
  0.00200  16877.3431423  -227.5628556  -227.5704323  -227.5631782  16877.4130218  -227.5049028  -227.5708805  -227.5047883  16877.4122567  16877.3894736
  0.00300  16877.3602570  -227.5634100  -227.5709878  -227.5637327  16877.4301338  -227.5054554  -227.5714360  -227.5053409  16877.4293698  16877.4065869
  0.00400  16877.3839257  -227.5641832  -227.5717624  -227.5645058  16877.4537989  -227.5062261  -227.5722106  -227.5061116  16877.4530363  16877.4302536
  ......
  ...
```

The first column is the photon energy (eV), and from the second columns onward, the components of tensor such as $\sigma _{xx}$ and $\sigma_{xy}$
are stored. In the last column the average value of the diagonal components $\sigma _{xx}$, $\sigma_{yy}$, and $\sigma_{zz}$ is given.
The other output files also follow the same format as in 'Si2_k50x50x50.cd_re'.
By plotting the first column as horizontal axis and the second column as vertical axis of
'Si2_k50x50x50.cd_re', 'Si2_k50x50x50.cd_im', 'Si2_k50x50x50.df_re', and 'Si2_k50x50x50.df_im',
one can obtain the optical conductivity $\sigma _{xx}$ and dielectric function
$\varepsilon _{xx}$
as shown in Fig. [80](optical-conductivity-and-dielectric-function-si-case.md#fig:CDDF-Fig1).
