<a id="SECTION000100000000000000000"></a>
# Functional

<a id="588"></a>
In OpenMX, local density approximations (LDA, LSDA) [[2](bibliography.md#LDA),[3](bibliography.md#LSDA),[4](bibliography.md#LSDA-PW)]
and a generalized gradient approximation (GGA) [[5](bibliography.md#GGA-PBE)]
to exchange-correlation functional are used.
Using a keyword 'scf.XcType', you can choose
one of approximations to the exchange-correlation functional:

```text

  scf.XcType                  LDA        # LDA|LSDA-CA|LSDA-PW|GGA-PBE
```

Currently, 'LDA', 'LSDA-CA', 'LSDA-PW', and 'GGA-PBE' are available,
where 'LSDA-CA' is the local spin density functional of
Ceperley-Alder [[2](bibliography.md#LDA)], 'LSDA-PW' is the local spin density
functional of Perdew-Wang, in which the gradient of density
is set in zero in their GGA formalism [[4](bibliography.md#LSDA-PW)].
Note: 'LSDA-CA' is faster than 'LSDA-PW'.
'GGA-PBE' is GGA proposed by Perdew, Burke, and Ernzerhof [[5](bibliography.md#GGA-PBE)].
The GGA is implemented by using the first order finite difference method
in real space. In addition, LDA+$U$ (or GGA+$U$) functionals are also available.
For the details, see the Section 'DFT+$U$'.
The relevant keyword to specify the spin (un)polarized and non-collinear
calculations is 'scf.SpinPolarization'.

```text

  scf.SpinPolarization        off        # On|Off|NC
```

If the calculation for the spin polarization is performed, then
specify 'ON'. If the calculation for the non-spin polarization
is performed, then specify 'OFF'. When you use 'LDA' for the keyword
'scf.XcType', the keyword 'scf.SpinPolarization' must be off.
In addition to these options, 'NC' is supported for the non-collinear
DFT calculation. For this calculation, see also the Section
'Non-collinear DFT'.
