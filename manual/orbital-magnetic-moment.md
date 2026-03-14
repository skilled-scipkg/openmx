<a id="SECTION000370000000000000000"></a>
# Orbital magnetic moment

<a id="1939"></a>
The orbital magnetic moment at each atomic site is calculated as default
in the non-collinear DFT. Since the orbital magnetic moment
appears as a manifestation of spin-orbit coupling (SOC),
the calculated values become finite when the SOC is included [[118](bibliography.md#Igor),[119](bibliography.md#Knopfle)].
As an example, a non-collinear LDA+U (U=5 eV) calculation of iron
monoxide bulk is illustrated using an input file 'FeO_NC.dat'
in the directory 'work'. As for the LDA+U calculation, see the Section
'LDA+U'. The calculated orbital and spin magnetic moments
at the Fe site are listed in Table 4. Also, you can find the orientation
of the (decomposed) orbital moment in '*System.Name*.out', where '*System.Name*' means
'System.Name'
as follows:

```text

***********************************************************
***********************************************************
                     Orbital moments
***********************************************************
***********************************************************

   Total Orbital Moment (muB)   0.000001885   Angles  (Deg) 126.954120326  185.681623854

          Orbital moment (muB)   theta (Deg)  phi (Deg)
    1   Fe   0.76440           131.30039   51.57082
    2   Fe   0.76440            48.69972  231.57071
    3    O   0.00000            40.68612  210.48405
    4    O   0.00000            48.18387  222.72367

  Decomposed Orbital Moments

    1   Fe         Orbital Moment(muB)    Angles (Deg)
            multiple
  s           0    0.000000000           90.0000    0.0000
   sum over m      0.000000000           90.0000    0.0000
  s           1    0.000000000           90.0000    0.0000
   sum over m      0.000000000           90.0000    0.0000
  px          0    0.000055764           42.7669  270.0000
  py          0    0.000046795           28.9750  180.0000
  pz          0    0.000044132           90.0000  239.0920
   sum over m      0.000120390           47.1503  239.0920
  px          1    0.001838092           10.8128  -90.0000
  py          1    0.001809013            3.5933  180.0000
  pz          1    0.000362989           90.0000  251.7994
   sum over m      0.003683170           11.3678  251.7994
  d3z^2-r^2   0    0.043435663           90.0000  224.2874
  dx^2-y^2    0    0.066105902           24.3591  229.7056
  dxy         0    0.361874370           80.4206   50.6465
  dxz         0    0.397108491          144.2572  -12.7324
  dyz         0    0.427070801          138.9995  100.0151
   sum over m      0.776513038          132.4577   51.6984
  d3z^2-r^2   1    0.000144144           90.0000  196.4795
  dx^2-y^2    1    0.000270422           31.2673  224.0799
  dxy         1    0.003006770           85.5910   50.2117
  dxz         1    0.002952926          139.3539   -4.1301
  dyz         1    0.003222374          134.0513   95.9246
   sum over m      0.006795789          126.2536   52.1993
  f5z^2-3r^2  0    0.001903274           90.0000   33.4663
  f5xz^2-xr^2 0    0.005186342           14.5594  118.0868
  f5yz^2-yr^2 0    0.005258572           17.3323  -35.0807
  fzx^2-zy^2  0    0.005477755           29.3372  224.9067
  fxyz        0    0.004851020           10.1407  249.0607
  fx^3-3*xy^2 0    0.002029489           84.1842  -81.2087
  f3yx^2-y^3  0    0.001611593           82.6686  176.3172
   sum over m      0.020307129            9.9551  249.3739
  .....
  ...
```

As shown in Table [6](orbital-magnetic-moment.md#table:Ms-Mo-TMO), OpenMX gives a good agreement for both the
spin and orbital magnetic moments of a series of $3d$-transition
metal oxides with other calculation results.
However, it is noted that the absolute value of orbital magnetic moment
seems to be significantly influenced by calculation conditions
such as basis functions and on-site 'U' in the LDA+U method,
while the spin magnetic moment is relatively insensitive to
the calculation conditions, and that a rather rich basis set including
polarization functions will be needed for convergent calculations of
the orbital magnetic moment.

<a id="table:Ms-Mo-TMO"></a>
<a id="6290"></a>
<a id="6290"></a>
|  | $M_s$ |  | $M_o$ |  |  |
| --- | --- | --- | --- | --- | --- |
| Compound | OpenMX | Other calc. | OpenMX | Other calc. | Expt. in total |
| MnO | 4.519 | 4.49 | 0.004 | 0.00 | 4.79,4.58 |
| FeO | 3.653 | 3.54 | 0.764 | 1.01 | 3.32 |
| CoO | 2.714 | 2.53 | 1.269 | 1.19 | 3.35,3.8 |
| NiO | 1.687 | 1.53 | 0.247 | 0.27 | 1.77,1.64,1.90 |
