<a id="SECTION000453000000000000000"></a>
## Monitoring optimization of spread function

The output during optimization steps is printed to the standard output.
To monitor the optimization progress, the following method may be helpful.
For convenient, we assume the standard output is stored in a file
'stdout.std'. The following example is for Si.dat which can be found in
openmx*.*/work/wf_example, and each user can trace the same calculation.

**DISE**

Monitor the self-consistent loops for disentangling progress
(the first step of optimization):

```text

  % grep "DISE" stdout.std

  |  Iter  | Omega_I (Angs^2) | Delta_I (Angs^2) |  ---> DISE
  |     1  |   18.371525257652|   18.371525257652|  ---> DISE
  |     2  |   17.955767336391|   -0.415757921261|  ---> DISE
  |     3  |   17.659503060694|   -0.296264275698|  ---> DISE
  |     4  |   17.454033576174|   -0.205469484520|  ---> DISE
  |     5  |   17.311180447271|   -0.142853128902|  ---> DISE
  |     6  |   17.210945408916|   -0.100235038355|  ---> DISE
  |     7  |   17.139778800398|   -0.071166608519|  ---> DISE
  |     8  |   17.088603102826|   -0.051175697572|  ---> DISE
  |     9  |   17.051329329614|   -0.037273773211|  ---> DISE
  |    10  |   17.023842837298|   -0.027486492316|  ---> DISE
  ........
  .....
  ...
  .
```

where 'Iter', 'Omega_I', and 'Delta_I' mean the iteration number,
the gauge invariant part of the spread function, and its difference
between two neighboring steps.
The criterion given by
the keyword 'Wannier.Dis.Conv.Criterion'
is applied to 'Delta_I'.

**CONV**

Monitor the optimization of the gauge dependent part of the spread
function (the second step of optimization):

```text

  % grep "CONV" stdout.std

  Opt Step |Mode of Gradient|d_Omega_in_steps|     d_Omega   | (in Angs^2) ---> CONV 
  | SD    1 | 6.52434844E-01 | 5.41612774E-04 |-5.41340331E-04|  ---> CONV 
  | SD    2 | 6.51123660E-01 | 5.40524307E-04 |-5.40253165E-04|  ---> CONV 
  .....
  .....
  | SD  200 | 4.77499752E-01 | 3.96392019E-04 |-3.96271308E-04|  ---> CONV 
  |Opt Step |Mode of Gradient|     d_Omega    | (Angs^2) ---> CONV 
  | CG    1 | 8.61043764E-01 | -3.24716990E-01|  ---> CONV 
  .....
  .....
  | CG   58 | 1.67083857E-12 | -5.37225101E-13|  ---> CONV 
  | CG   59 | 5.44431651E-13 | -1.98972260E-13|  ---> CONV 
  ************************************************************* ---> CONV
  CONVERGENCE ACHIEVED !                      ---> CONV
  ************************************************************* ---> CONV
  CONVERGENCE ACHIEVED !                      ---> SPRD
```

where 'Opt Step' and 'Modu.of Gradient' are the optimization step
in either 'SD' or 'CG' method and the modulus of gradient of the
spread function.
The difference between two neighboring steps in the gauge dependent spread
functions is calculated in two different way in the SD method, giving
'd_Omega_in_steps' and 'd_Omega'.
'd_Omega_in_steps'
is given by

| $\displaystyle d\Omega = \epsilon \sum_{\bf k} \vert\vert G^{\bf (k)} \vert\vert^2,$ |  |  |  |
| --- | --- | --- | --- |

where $\epsilon$ is the step length, $G^{\bf (k)}$ is the gradient
of the spread function. The details of the equation can be found in
Ref. [[122](bibliography.md#mlwf1)].
On the other hand, 'd_Omega' is given by

| $\displaystyle d\Omega = \Omega^{(n+1)} - \Omega^{(n)},$ |  |  |  |
| --- | --- | --- | --- |

where $n$ is the iteration number.
In the CG method, only 'd_Omega' is evaluated. The criterion given by
the keyword 'Wannier.Minimizing.Conv.Criterion'
is applied to 'Modu.of Gradient'.

**SPRD**

Monitor the variation of spread of the Wannier functions:

```text

  % grep "SPRD" stdout.std

  |Opt Step |     Omega_I    |     Omega_D    |     Omega_OD  |    Tot_Omega  | (in Angs^2) ---> SPRD 
  | SD    1 |   16.93053479  |    0.13727387  |    6.57748455 |   23.64529321 |  ---> SPRD 
  | SD    2 |   16.93053479  |    0.13724827  |    6.57696989 |   23.64475295 |  ---> SPRD 
  | SD    3 |   16.93053479  |    0.13722279  |    6.57645620 |   23.64421378 |  ---> SPRD 
  | SD    4 |   16.93053479  |    0.13719743  |    6.57594347 |   23.64367569 |  ---> SPRD 
  .....
  .....
  | SD  199 |   16.93053479  |    0.13399285  |    6.48989479 |   23.55442243 |  ---> SPRD 
  | SD  200 |   16.93053479  |    0.13398326  |    6.48950811 |   23.55402616 |  ---> SPRD 
  |Opt Step |     Omega_I    |     Omega_D    |     Omega_OD  |    Tot_Omega  | (Angs^2) ---> SPRD 
  | CG    1 |    16.93053479 |     0.15480701 |    6.14396737 |   23.22930917 |  ---> SPRD 
  | CG    2 |    16.93053479 |     0.17172507 |    5.87830203 |   22.98056189 |  ---> SPRD 
  | CG    3 |    16.93053479 |     0.17012089 |    5.78940789 |   22.89006357 |  ---> SPRD 
  .....
  .....
  | CG   57 |    16.93053479 |     0.16557875 |    5.73752928 |   22.83364282 |  ---> SPRD 
  | CG   58 |    16.93053479 |     0.16557876 |    5.73752928 |   22.83364282 |  ---> SPRD 
  | CG   59 |    16.93053479 |     0.16557876 |    5.73752928 |   22.83364282 |  ---> SPRD 
  ************************************************************* ---> SPRD
  CONVERGENCE ACHIEVED !                      ---> SPRD
  ************************************************************* ---> SPRD
```

where 'Opt Step' is the optimization step in either 'SD' or 'CG' method.
'Omega_I' is the gauge invariant part of spread function.
'Omega_D' and 'Omega_OD' are the gauge dependent diagonal and off-diagonal
contribution, respectively. 'Tot_Omega' is the sum up of all the above three
components of the spread function.

**CENT**

Monitor the variation of Wannier function center:

```text

  % grep "CENT" stdout.std
  WF   1 ( 1.14164289, 1.14164298, 1.14164266) |   2.95573380  --->CENT
  WF   2 ( 1.55716251, 1.55716342, 1.14164203) |   2.95572597  --->CENT
  WF   3 ( 1.55716191, 1.14164295, 1.55716190) |   2.95572978  --->CENT
  WF   4 ( 1.14164389, 1.55716087, 1.55716055) |   2.95572957  --->CENT
  WF   5 ( 0.20775982, 0.20775967, 0.20775893) |   2.95572677  --->CENT
  WF   6 ( 0.20776045,-0.20775959,-0.20775914) |   2.95572605  --->CENT
  WF   7 (-0.20775851, 0.20775981,-0.20775888) |   2.95572925  --->CENT
  WF   8 (-0.20775787,-0.20775767, 0.20775933) |   2.95573335  --->CENT
  Total Center ( 5.39761509, 5.39761243, 5.39760738) sum_spread  23.64583455 --->CENT
  SD     1 ------------------------------------------------------------------------> CENT
  WF   1 ( 1.14164582, 1.14164592, 1.14164559) |   2.95566613  --->CENT
  WF   2 ( 1.55715957, 1.55716049, 1.14164497) |   2.95565831  --->CENT
  WF   3 ( 1.55715897, 1.14164588, 1.55715897) |   2.95566211  --->CENT
  WF   4 ( 1.14164683, 1.55715794, 1.55715761) |   2.95566190  --->CENT
  WF   5 ( 0.20775689, 0.20775673, 0.20775599) |   2.95565910  --->CENT
  WF   6 ( 0.20775752,-0.20775666,-0.20775620) |   2.95565838  --->CENT
  WF   7 (-0.20775558, 0.20775687,-0.20775594) |   2.95566158  --->CENT
  WF   8 (-0.20775493,-0.20775474, 0.20775639) |   2.95566569  --->CENT
  Total Center ( 5.39761509, 5.39761243, 5.39760738) sum_spread  23.64529321 --->CENT
  SD     2 ------------------------------------------------------------------------> CENT
  .....
  .....
  CG    59 ------------------------------------------------------------------------> CENT
  WF   1 ( 1.14585349, 1.14584696, 1.14584386) |   2.85421846  --->CENT
  WF   2 ( 1.55295615, 1.55294970, 1.14584792) |   2.85422167  --->CENT
  WF   3 ( 1.55296133, 1.14584610, 1.55295139) |   2.85421070  --->CENT
  WF   4 ( 1.14584053, 1.55296761, 1.55296391) |   2.85417080  --->CENT
  WF   5 ( 0.20356211, 0.20355857, 0.20355600) |   2.85418933  --->CENT
  WF   6 ( 0.20355119,-0.20355008,-0.20355192) |   2.85422458  --->CENT
  WF   7 (-0.20355306, 0.20355395,-0.20355905) |   2.85420611  --->CENT
  WF   8 (-0.20355603,-0.20356000, 0.20355520) |   2.85420117  --->CENT
  Total Center ( 5.39761571, 5.39761281, 5.39760730) sum_spread  22.83364282 --->CENT
```

where the optimization method and step are indicated by starting with 'SD' or 'CG'.
Lines starting with 'WF' show the center of each Wannier function with ($x$, $y$, $z$)
coordinates in Å unit.
and its spread in Å$^{2}$. The sum up of all the Wannier functions center and
spread are given in the line starting with 'Total Center'.
