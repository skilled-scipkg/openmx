<a id="SECTION000382200000000000000"></a>
### Estimation of $J$ and $F^4/F^2$ from input parameter $U$

One can estimate $J$ and $F^4/F^2$ from input $U$ value via Yukawa-type
screened Coulomb potential by the following keyword:

```text

  scf.Yukawa                       on      # default=off
```

By setting `scf.Yukawa=on`, only $U$ values in `<Hubbard.U.values ... Hubbard.U.values>`
are read and $J$ values in `<Hund.J.values ... Hund.J.values>` and `scf.Slater.Ratio`
are ignored. Instead, $J$ values and $F^4/F^2$ will be automatically generated
by estimating the Thomas-Fermi screening length corresponding to the input $U$ values [[21](bibliography.md#Ryee1),[22](bibliography.md#Ryee2)].
As an example, for the following orbitals defined by:

```text

  <Definition.of.Atomic.Species
    Ni Ni6.0S-s2p2d2f1  Ni_CA13S
    O  O5.0-s2p2d1      O_CA13
  Definition.of.Atomic.Species>
```

when `scf.Yukawa=on` and $U$ values are set to:

```text

  <Hubbard.U.values   # eV  
    Ni 1s 0.0 2s 0.0 1p 0.0 2p 0.0 1d 6.4 2d 3.0 1f 0.0
    O  1s 0.0 2s 0.0 1p 0.0 2p 0.0 1d 0.0
  Hubbard.U.values>
```

one can see the following message in the standard output before SCF loop begins:

```text

  *******************************************************
        Calculating Thomas-Fermi screening length 
  *******************************************************

  <species: Ni, angular momentum= 2, multiplicity number= 0>
   TF-screening-length lambda= 1.340787 1/au
   Hubbard U= 6.400000 eV
   Hund J= 1.154943 eV
   Slater F0= 6.399932 eV
   Slater F2= 9.321381 eV
   Slater F4= 6.847820 eV
   F4/F2= 0.734636

  <species: Ni, angular momentum= 2, multiplicity number= 1>
   TF-screening-length lambda= 0.271461 1/au
   Hubbard U= 3.000000 eV
   Hund J= 0.380184 eV
   Slater F0= 3.000017 eV
   Slater F2= 2.970544 eV
   Slater F4= 2.352036 eV
   F4/F2= 0.791786
```

These $U$, $J$, and $F^4/F^2$ values will be used for a subsequent DFT+$U$ SCF loop.
The input file, 'NiO-Yukawa.dat' can be found in the directory 'work'.

---
