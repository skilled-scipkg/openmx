<a id="SECTION000447000000000000000"></a>
## Interpolation of the effect by the bias voltage

Since for large-scale systems it is very time-consuming to perform
the SCF calculation at each bias voltage, an interpolation scheme
is available to reduce the computational cost in the calculations
by the NEGF method.
The interpolation scheme is performed in the following way:
(i) the SCF calculations are performed
for a few bias voltages which are selected in the regime of the bias
voltage of interest.
(ii) when the transmission and current are calculated,
linear interpolation is made for the Hamiltonian block elements,

$H_{\sigma,C}^{(\bf k)}$ and
$H_{\sigma,R}^{(\bf k)}$, of
the central scattering region and the right lead, and the chemical
potential, $\mu_{R}$, of the right lead by

<a id="eq:c1-60"></a>
<a id="eq:c1-61"></a>
<a id="eq:c1-62"></a>
| $\displaystyle H_{\sigma,C}^{(\bf k)}$ | $\textstyle =$ | $\displaystyle \lambda H_{\sigma,C}^{({\bf k},1)}
+ (1-\lambda) H_{\sigma,C}^{({\bf k},2)},$ |  |
| --- | --- | --- | --- |
| $\displaystyle H_{\sigma,R}^{(\bf k)}$ | $\textstyle =$ | $\displaystyle \lambda H_{\sigma,R}^{({\bf k},1)}
+ (1-\lambda) H_{\sigma,R}^{({\bf k},2)},$ |  |
| $\displaystyle \mu_{R}$ | $\textstyle =$ | $\displaystyle \lambda \mu_{R}^{(1)} + (1-\lambda) \mu_{R}^{(2)},$ |  |

where the indices $1$ and $2$ in the superscript mean that
the quantities are calculated or used at the corresponding bias voltages
where the SCF calculations are performed beforehand.
In general, $\lambda$ should range from 0 to 1 for the moderate
interpolation.

In the calculation of the step 3, the interpolation is made by adding
the following keywords in the input file:

```text

  NEGF.tran.interpolate         on               # default=off, on|off
  NEGF.tran.interpolate.file1  c1-negf-0.5.tranb
  NEGF.tran.interpolate.file2  c1-negf-1.0.tranb
  NEGF.tran.interpolate.coes    0.7 0.3          # default=1.0 0.0
```

When you perform the interpolation, the keyword
'NEGF.tran.interpolate'
should be 'on'.
In this case, files 'c1-negf-0.5.tranb' and 'c1-negf-1.0.tranb'
specified by the keywords 'NEGF.tran.interpolate.file1'
and 'NEGF.tran.interpolate.file2'
are the results under bias voltages of 0.5 and 1.0 V, respectively, and
the transmission and current at
$V=0.7*0.5+0.3*1.0=0.65 [V]$ are evaluated
by the interpolation scheme, where the weights of 0.7 and 0.3 are specified
by the keyword 'NEGF.tran.interpolate.coes'.

<a id="fig:NEGF_int"></a>
<a id="2881"></a>
| ![\includegraphics[width=17.0cm]{NEGF_int.eps}](assets/img314.png) |
| --- |

A comparison between the fully self consistent and the interpolated
results is shown with respect to the current and transmission
in the linear carbon chain in Figs. [44](interpolation-of-the-effect-by-the-bias-voltage.md#fig:NEGF_int)(a) and (b).
In this case, the SCF calculations at three bias voltages of 0, 0.5,
and 1.0 V are performed, and the results at the other bias voltages
are obtained by the interpolation scheme. For comparison we also
calculate the currents via the SCF calculations at all the bias voltages.
It is confirmed that the simple interpolation scheme gives notably
accurate results for both the calculations of the current and transmission.
Although the proper selection of bias voltages used for the SCF calculations
may depend on systems, the result suggests that the simple scheme is
very useful to interpolate the effect of the bias voltage while keeping
the accuracy of the calculations.
