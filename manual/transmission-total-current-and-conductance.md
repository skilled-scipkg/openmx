<a id="SECTION000444100000000000000"></a>
### Transmission, total current, and conductance

At first, `openmx` calculates the transmission, the total current,
and the conductance.
The relevant keywords for the calculation are as follows:

```text

    NEGF.tran.Analysis         on        #  default on
    NEGF.tran.CurrentDensity   on        #  default on
    NEGF.tran.energyrange -10 10 1.0e-3  # default=-10.0 10.0 1.0e-3 (eV)
    NEGF.tran.energydiv        200       # default=200
    NEGF.tran.Kgrid            1 1       # default= 1 1
```

<a id="2709"></a>
<a id="2710"></a>
<a id="2711"></a>
<a id="2712"></a>
<a id="2713"></a>
<a id="2714"></a>
<a id="2715"></a>
<a id="2716"></a>
<a id="2720"></a>
<a id="2721"></a>
<a id="2722"></a>
- `NEGF.tran.Analysis`, `NEGF.tran.Channel`, `NEGF.tran.CurrentDensity`
  If `NEGF.tran.Analysis` is set to `on`,
  the transmission, the total current, and the conductance are calculated.
- `NEGF.tran.energyrange`, `NEGF.tran.energydiv`
  <a id="2713"></a>
  <a id="2714"></a>
  <a id="2715"></a>
  The energy range where the transmission is calculated is given by
  the keyword 'NEGF.tran.energyrange',
  where the first and second numbers correspond
  to the lower and upper bounds, and the third number is an imaginary number
  used for smearing out the transmission. The energy range specified by
  'NEGF.tran.energyrange' is divided
  by the number specified by the keyword
  'NEGF.tran.energydiv'.
- `NEGF.tran.Kgrid`
  <a id="2720"></a>
  <a id="2721"></a>
  <a id="2722"></a>
  The numbers of **k**-points to discretize the reciprocal vectors

  ${\bf\tilde{b}}$ and
  ${\bf\tilde{c}}$ are specified by the keyword
  'NEGF.tran.Kgrid'. The set of numbers given by
  'NEGF.tran.Kgrid'
  can be different
  and tends to be larger than that by 'NEGF.scf.Kgrid'
  to take account of the computational efficiency.

In the calculations of the transmission, the current, and the conductance,
following messages are printed in the standard output.

```text

*******************************************************
*******************************************************
 Welcome to TRAN_Main_Analysis.                        
 This is a post-processing code of OpenMX to analyze   
 transport properties such as electronic transmission, 
 current, eigen channel, and current distribution in   
 real space based on NEGF.                             
 Copyright (C), 2002-2015, H. Kino and T. Ozaki        
 TRAN_Main_Analysis comes with ABSOLUTELY NO WARRANTY. 
 This is free software, and you are welcome to         
 redistribute it under the constitution of the GNU-GPL.
*******************************************************
*******************************************************

Chemical potentials used in the SCF calculation
  Left lead:  -5.125617225230 (eV)
  Right lead: -5.125617225230 (eV)
NEGF.current.energy.step 1.0000e-02 seems to be large for the calculation of current ...
The recommended Tran.current.energy.step is 0.0000e+00 (eV).
  TRAN_Channel_kpoint  0    0.000000    0.000000
  TRAN_Channel_energy  0    0.000000 eV
  TRAN_Channel_Num 5 

Parameters for the calculation of the current
  lower bound:     -5.125617225230 (eV)
  upper bound:     -5.125617225230 (eV)
  energy step:      0.010000000000 (eV)
  imaginary energy  0.001000000000 (eV)
  number of steps:   0         

  calculating...

  myid0= 0 i2= 0 i3= 0  k2=  0.0000 k3= -0.0000
  myid0= 1 i2= 0 i3= 0  k2=  0.0000 k3= -0.0000

Transmission:  files

  ./negf-chain.tran0_0

Current:  file

  ./negf-chain.current

Conductance:  file

  ./negf-chain.conductance
```

After the calculations, in this case you will obtain three files
`negf-chain.tran0_0`,
`negf-chain.current`,

`negf-chain.conductance`:

<a id="2731"></a>
- *System.Name*.tran#_%
  <a id="2731"></a>
  The file stores transmissions for up- and down-spin states.
  The fourth column is the energy relative to the chemical potential
  of the **left** lead, and the sixth and eighth columns are
  transmission for up- and down-spin states, respectively.
  When you employ a lot of **k**-points which is given by
  'NEGF.tran.Kgrid',
  a file with a different set of '#' and '%' in the file extension
  is generated for each **k**-point. The correspondence between the numbers
  and the **k**-points can be found in the file.
- *System.Name*.current
  The file stores **k**-resolved currents and its average for up- and down-spin
  states in units of ampere.
- *System.Name*.conductance
  The file stores **k**-resolved conductance and its average for up- and
  down-spin states in units of quantum conductance (
  $G_0\equiv \frac{e^2}{h}$).
  Thus, the conductance $G$ is proportional to the transmission $T$
  at the chemical potential of the **left** lead, $\mu_{L}$, as follows:
  | $\displaystyle G = \frac{e^2}{h} T(\mu_{L})$ |  |  |  |
  | --- | --- | --- | --- |

As an example, the **k**-resolved transmission drawn by
using the file '*System.Name*.conductance' is shown in Fig. [41](transmission-total-current-and-conductance.md#fig:NEGF_MgO).

<a id="fig:NEGF_MgO"></a>
<a id="6330"></a>
| ![\includegraphics[width=8.0cm]{NEGF_MgO.eps}](assets/img296.png) |
| --- |
