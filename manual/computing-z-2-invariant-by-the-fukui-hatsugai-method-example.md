<a id="SECTION000572000000000000000"></a>
## Example

As an example, let us calculate a $Z_{2}$ invariant of a 3D topological
insulator Bi$_2$Se$_3$ [[83](bibliography.md#Kato2015)].

<a id="4778"></a>
**SCF calculation**

You can perform the SCF calculation using 'Bi2Se3-Z2.dat' stored in the directory 'work'
with the following keyword:

```text

    HS.fileout      on      #on|off, default=off
```

After finishing the SCF calculation normally, the out file 'Bi2Se3-Z2.scfout' is generated.

**Calculation of Z$_2$ invariant**

Before computing the $Z_{2}$ invariant by using the code 'Z2FH.c', please
compile the code in directory 'source' as

```text

    % make Z2FH
```

After the compilation, you may obtain the excutable file 'Z2FH' in the directory 'work'.
Then, let us move on the calculation of the Z$_2$ invariant as

```text

   % ./Z2FH Bi2Se3-Z2.scfout
 or
   % ./Z2FH Bi2Se3-Z2.scfout < Z2FH.in > Z2FH.out
 or
   % mpirun -np 4 ./Z2FH Bi2Se3-Z2.scfout < Z2FH.in > Z2FH.out
```

The file 'Z2FH.in' contains parameters which are requested by 'Z2FH' such as

```text

   5
   1
   1
```

In the first case above, you will be interactively asked from the program
as follows:

```text

    ******************************************************************
    ******************************************************************
     Z2FH:
     code for calculating the Z2 invariant of bulk systems
     by Fukui-Hatsugai method.
     Copyright (C), 2019, Hikaru Sawahata, Naoya Yamaguchi,
     Fumiyuki Ishii and Taisuke Ozaki 
     This is free software, and you are welcome to         
     redistribute it under the constitution of the GNU-GPL.
     
     Please cite the following article:
     H. Sawahata, N. Yamaguchi, H. Kotaka and F. Ishii,
     Jpn. J. Appl. Phys. 57, 030309 (2018).
    ******************************************************************
    ******************************************************************
    Mesh1 Number(Half Direction):5
    Calculate All plane?(0:No,1:Yes)1
    Restart?[1:x0,2:xpi,3:y0....]1
    
    Read the scfout file (Bi2Se3-Z2.scfout)
    ***
    The file format of the SCFOUT file:  3
    And it supports the following functions:
    - jx
    - polB
    - kSpin
    - Z2FH
    - calB
    ***
```

**Parameters for Z2FH**

Let us explain the parameters in the input file 'Z2FH.in'.

- In the first line, you set the number of mesh on the half of integration interval, in other words, on the space of quarter of the first Brillouin zone (please see the Fig. [75](computing-z-2-invariant-by-the-fukui-hatsugai-method-general.md#fig:Z2-Fig1)). If you set as '5', the code performs the integrations on the square plaquettes formed by 5$\times $5 k-point mesh in the quarter Brillouin zone.
- In the second line, you can speficy a flag whether computing $Z_{2}$ invariant is performed or not on all the six k-planes on which the $Z_2$ invariant is defined. If you want to compute only four planes for $(\nu_{0}, \nu_{1}, \nu_{2}, \nu_{3})$, you can set as '0'. Otherwise, please set as '1', corresponding to all the calculations of the six planes for ( $x_{0},x_{\pi},y_{0},y_{\pi},z_{0},z_{\pi}$).
- In the third line, you can set the ${\bf k}$-plane on which you want to restart the calculation. The numbers 1, 2, 3, 4, 5, and 6 correspond to $k_1=0$, $k_1=\frac{{\bf G}_{1}}{2}$, $k_2=0$, $k_2=\frac{{\bf G}_{2}}{2}$, $k_3=0$, and $k_3=\frac{{\bf G}_{3}}{2}$ planes, respectively.

**Output files**

After the calculation by 'Z2FH', the following files are generated.

- Z2.dat
  This file stores the computational result of $Z_{2}$ invariant.
  In case of computing all the ${\bf k}$-plane (you set the second row parameter as '1'.),
  the $Z_{2}$ invariants on the six ${\bf k}$-planes are on the first line,
  and four of $Z_{2}$ invariant are on the second line as shown below:
  ```text

    Z2 invariant:(x0,xpi,y0,ypi,z0,zpi)=(1.000000,-0.000000,1.000000,-0.000000,1.000000,-0.000000)
    Z2 invariant:(nu0,nu1,nu2,nu3):(1,0,0,0)
  ```
- LCNum*.dat
  Data files of integer-valued field $n({\bf k})$. The '*' behind 'LCNum' is the index running from 1 to 6.
  The number (1,2,3,4,5,6) corresponds to
  $(x_{0},x_{\pi},y_{0},y_{\pi},z_{0},z_{\pi})$, respectively.
  When you calculate only four planes, four files 'LCNum(2,4,5,6).dat' are generated, corresponding to

  $(x_{\pi},y_{\pi},z_{0},z_{\pi})$.
- LCNum*.pl
  Script files for gnuplot.
  The '*' behind 'LCNum' is the index running from 1 to 6.
  The number (1,2,3,4,5,6) corresponds to
  $(x_{0},x_{\pi},y_{0},y_{\pi},z_{0},z_{\pi})$, respectively.
  When you calculate only four planes, four files 'LCNum(2,4,5,6).dat' are generated, corresponding to

  $(x_{\pi},y_{\pi},z_{0},z_{\pi})$.
  You can visualize of integer-valued field $n({\bf k})$ by
  ```text

        % gnuplot LCNum1.pl
  ```
- temporal_12345.input
  This is a copy of input file, which was used for the SCF calculation, reconstructed from the scfout file.

As an example, we show the integer-valued field $n({\bf k})$ on $k_1=0$ in Fig. [77](fig:Z2-Fig3),
which can be obtained by the procedure explained above as 'gnuplot LCNum1.pl'.
Since $n({\bf k})$ is the gauge dependent value, you may find a different result in your calculation,
while the Z$_2$ invariant should be reproduced.

<a id="fig:Z2-Fig3"></a>
<a id="6437"></a>
| ![\includegraphics[width=10.0cm]{Z2-Fig3.eps}](assets/Z2-Fig3.png) |
| --- |
