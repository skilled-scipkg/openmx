<a id="SECTION000381200000000000000"></a>
### Choice of the double-counting

A double-counting (dc) correction is common for any 'embedding' methods such as DFT+$U$.
When using `scf.DFTU.Type=2`, the dc term should be specified by the following keyword:

```text

  scf.dc.Type                 cFLL	   # sFLL|sAMF|cFLL|cAMF, default=sFLL
```

In the above case, the 'cFLL' dc-term is chosen. In the specification of 'sFLL', 'sAMF', 'cFLL', and 'cAMF',
'c' and 's' mean the density functional scheme within charge (spin-unpolarized) density and spin density LDA/GGA, respectively,
and 'FLL' and 'AMF' correspond to a fully localized limit (FLL) and around mean-field (AMF) for the treatment
of the double-counting term. For the detailed definitions and behaviors of each scheme,
please refer to Ref. [[21](bibliography.md#Ryee1),[22](bibliography.md#Ryee2)]. Users should keep in mind that when `cFLL` or
`cAMF` dc-term is chosen, spin-density exchange-correlation energy of LDA (or GGA) is not taken
into account during the SCF loop [[21](bibliography.md#Ryee1),[22](bibliography.md#Ryee2)]. `scf.dc.Type=sFLL` corresponds to the form proposed
by Liechtenstein *et al.* [[26](bibliography.md#Liechtenstein1995)].
Note also that when using a simplified scheme (`scf.DFTU.Type=1`), `sFLL` dc-term is
implicit in its functional form.

Users can check what kinds of DFT+$U$ scheme has been specified with the following message before
SCF loop begins in the standard output:

```text

  For scf.DFTU.Type=1,

  *******************************************************
                     DFT+U Type and DC
  *******************************************************
                scf.DFTU.Type: 1(Simplified)   

  For scf.DFTU.Type=2 and scf.dc.Type=cFLL,

  *******************************************************
                     DFT+U Type and DC
  *******************************************************
       scf.DFTU.Type: 2(General)   scf.dc.Type: cFLL
```

As an example of the DFT+$U$ calculation, the density of states for NiO bulk is shown in Fig. [34](choice-of-the-double-counting.md#DFTU_FIG1)
for cases with $U=5$ eV and two different $J$ values (0.5 and 1.0 eV) for $d$-orbitals of Ni.

<a id="DFTU_FIG1"></a>
<a id="2001"></a>
| ![\includegraphics[width=1.0\textwidth, angle=0]{DFTU_FIG1.eps}](assets/img202.png) |
| --- |

The input files, `NiO-cFLL.dat' and `NiO-sFLL.dat' can be found in the directory `work'.
We can see that the gap increases due to the introduction of $U$ on the $d$-orbitals
as well as the different behaviors of varying $J$ depending on the choice `scf.dc.Type`.

The occupation number for each orbital is output to the file '*System.Name*.out'
in the same form as that of decomposed Mulliken populations which
starts from the title 'Occupation Number in LDA+U', e.g.,
NiO with 'scf.dc.Type=cFLL' of $U=5$ eV and $J=0.5$ eV, as follows:

```text

***********************************************************
***********************************************************
       Occupation Number in LDA+U and Constraint DFT

    Eigenvalues and eigenvectors for a matrix consisting
           of occupation numbers on each site
***********************************************************
***********************************************************

    1   Ni

     spin= 0

  Sum =  8.708572022602

                    1       2       3       4       5       6       7       8    
  Individual     -0.0041  0.0012  0.0012  0.0022  0.0040  0.0040  0.0044  0.0064 

  s           0   0.1792 -0.0008 -0.0000  0.0015 -0.0000  0.0003  0.0124 -0.0000 
  s           1  -0.9756  0.0052  0.0000  0.0026  0.0000 -0.0041 -0.1251  0.0000 
  px          0   0.0006  0.0007 -0.0012 -0.0123  0.0003  0.0006 -0.0033 -0.0000 
  py          0   0.0006 -0.0013 -0.0000 -0.0122  0.0000  0.0000 -0.0033  0.0000 
  pz          0   0.0006  0.0007  0.0012 -0.0123 -0.0003  0.0006 -0.0033  0.0000 
  px          1   0.0091  0.0053 -0.0095 -0.0867  0.0205  0.0152 -0.0206  0.0026 
  py          1   0.0093 -0.0116 -0.0000 -0.0870 -0.0000 -0.0207 -0.0236 -0.0000 
  pz          1   0.0091  0.0052  0.0095 -0.0867 -0.0205  0.0152 -0.0206 -0.0026 
  d3z^2-r^2   0   0.0002  0.0348  0.0604 -0.0000 -0.0020  0.0012  0.0001 -0.0005 
  dx^2-y^2    0   0.0004  0.0604 -0.0348 -0.0000  0.0011  0.0020  0.0001  0.0003 
  dxy         0  -0.0001  0.0007  0.0012  0.0151  0.0367 -0.0218  0.0097 -0.0003 
  dxz         0  -0.0006 -0.0015 -0.0000  0.0167  0.0000  0.0417  0.0112  0.0000 
  dyz         0  -0.0001  0.0007 -0.0012  0.0151 -0.0367 -0.0218  0.0097  0.0003 
  d3z^2-r^2   1  -0.0025 -0.4966 -0.8626 -0.0006  0.0295 -0.0174 -0.0006  0.0056 
  dx^2-y^2    1  -0.0042 -0.8625  0.4967 -0.0010 -0.0170 -0.0301 -0.0010 -0.0033 
  dxy         1   0.0136 -0.0160 -0.0276 -0.5343 -0.7016  0.4220 -0.1326  0.0055 
  dxz         1   0.0225  0.0332  0.0000 -0.5657 -0.0000 -0.7918 -0.1607 -0.0000 
  dyz         1   0.0136 -0.0161  0.0275 -0.5343  0.7016  0.4219 -0.1325 -0.0055 
  f5z^2-3r^2  0  -0.0029  0.0032  0.0065 -0.0804 -0.0514  0.0334 -0.0282 -0.0069 
  f5xz^2-xr^2 0   0.0017 -0.0304 -0.0148  0.0467 -0.0113 -0.0653  0.0174 -0.4673 
  f5yz^2-yr^2 0   0.0013  0.0057 -0.0294  0.0479  0.0517  0.0341  0.0272  0.4428 
  fzx^2-zy^2  0  -0.0001 -0.0360  0.0237 -0.0031 -0.0256 -0.0567  0.0001  0.5857 
  fxyz        0   0.1218 -0.0003 -0.0000  0.2573  0.0000  0.0172 -0.9581  0.0000 
  fx^3-3*xy^2 0  -0.0023 -0.0195 -0.0197 -0.0655  0.0563 -0.0083 -0.0223 -0.3532 
  f3yx^2-y^3  0   0.0017  0.0072  0.0228  0.0618 -0.0401  0.0441  0.0352 -0.3430 

                    9      10      11      12      13      14      15      16    
  Individual      0.0116  0.0117  0.0207  0.0207  0.0238  0.0972  0.1112  0.1114 

  s           0  -0.0003 -0.0000  0.0000 -0.0005 -0.0075 -0.0206 -0.0000 -0.0000 
  s           1   0.0001  0.0000  0.0000 -0.0013  0.0076  0.0102  0.0000 -0.0000 
  px          0  -0.0005  0.0006 -0.0024  0.0014  0.0043 -0.0270  0.0291  0.0170 
  py          0   0.0006  0.0000  0.0000 -0.0027  0.0044 -0.0279 -0.0000 -0.0338 
  pz          0  -0.0005 -0.0006  0.0024  0.0014  0.0043 -0.0270 -0.0291  0.0171 
  px          1   0.0229 -0.0402  0.1442 -0.0832 -0.1073  0.5479 -0.6901 -0.4038 
  py          1  -0.0437  0.0000 -0.0005  0.1632 -0.1127  0.5594  0.0003  0.7916 
  pz          1   0.0229  0.0402 -0.1437 -0.0841 -0.1073  0.5478  0.6898 -0.4043 
  d3z^2-r^2   0   0.0053  0.0093  0.0012  0.0006 -0.0001  0.0003 -0.0202  0.0115 
  dx^2-y^2    0   0.0092 -0.0053 -0.0007  0.0011 -0.0002  0.0006  0.0117  0.0199 
  dxy         0  -0.0033 -0.0056 -0.0049 -0.0032 -0.0237  0.0916  0.0095 -0.0067 
  dxz         0   0.0069 -0.0000 -0.0000  0.0054 -0.0236  0.0915  0.0000  0.0102 
  dyz         0  -0.0033  0.0056  0.0049 -0.0031 -0.0237  0.0916 -0.0095 -0.0067 
  d3z^2-r^2   1  -0.0241 -0.0404 -0.0230 -0.0138  0.0011 -0.0001  0.0089 -0.0052 
  dx^2-y^2    1  -0.0418  0.0233  0.0134 -0.0238  0.0018 -0.0002 -0.0051 -0.0090 
  dxy         1   0.0224  0.0367  0.0645  0.0399  0.1012 -0.0657 -0.0086  0.0058 
  dxz         1  -0.0489  0.0000  0.0002 -0.0737  0.1010 -0.0652 -0.0000 -0.0096 
  dyz         1   0.0224 -0.0367 -0.0648  0.0395  0.1011 -0.0657  0.0086  0.0058 
  f5z^2-3r^2  0   0.0928  0.1648 -0.6676 -0.3997 -0.5498 -0.1226 -0.1505  0.0868 
  f5xz^2-xr^2 0   0.4854  0.4030 -0.3328  0.3674  0.3359  0.0744 -0.0944 -0.0506 
  f5yz^2-yr^2 0   0.1112  0.6352  0.1497 -0.4674  0.3502  0.0772 -0.0023  0.1046 
  fzx^2-zy^2  0   0.6859 -0.3821 -0.0991  0.1577 -0.0010 -0.0008  0.0028  0.0032 
  fxyz        0   0.0052  0.0000  0.0000 -0.0109  0.0195  0.0064  0.0000  0.0007 
  fx^3-3*xy^2 0   0.4934  0.1037  0.5899 -0.2158 -0.4352 -0.0974  0.1173  0.0705 
  f3yx^2-y^3  0   0.1435 -0.4920 -0.1130 -0.6043  0.4520  0.0997  0.0019  0.1351 

                   17      18      19      20      21      22      23      24    
  Individual      0.2342  0.9866  0.9949  0.9950  1.0070  1.0070  1.0101  1.0101 

  s           0   0.9835 -0.0030 -0.0001  0.0000 -0.0000  0.0001  0.0003  0.0000 
  s           1   0.1796 -0.0015 -0.0000  0.0000  0.0000 -0.0000 -0.0000 -0.0000 
  px          0  -0.0023 -0.5138 -0.3934 -0.6753 -0.0494 -0.0317  0.1133 -0.2016 
  py          0  -0.0021 -0.5218  0.7787 -0.0000 -0.0000  0.0587 -0.2264 -0.0000 
  pz          0  -0.0023 -0.5138 -0.3933  0.6753  0.0494 -0.0317  0.1132  0.2017 
  px          1   0.0092 -0.0625 -0.0195 -0.0329  0.0012  0.0006 -0.0049  0.0083 
  py          1   0.0095 -0.0631  0.0376 -0.0000  0.0000 -0.0016  0.0097  0.0000 
  pz          1   0.0092 -0.0625 -0.0195  0.0329 -0.0012  0.0006 -0.0049 -0.0083 
  ..... 
  ...
```

The eigenvalues of the occupation number matrix of each atomic site correspond
to the occupation number to each local state given by the eigenvector.
