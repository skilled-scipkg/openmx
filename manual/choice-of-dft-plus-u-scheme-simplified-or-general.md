<a id="SECTION000381100000000000000"></a>
### Choice of DFT+$U$ scheme; simplified or general

The general forms of DFT+$U$ methods with different definitions of the occupation number operator,
the functional form, and the choice of the double counting term are available
in OpenMX for both collinear and noncollinear calculations [[21](bibliography.md#Ryee1),[22](bibliography.md#Ryee2)] by the following two keywords:

```text

  scf.Hubbard.U                 on  # on|off, default=off
  scf.DFTU.Type                 2   # 1:Simplified(Dudarev)|2:General, default=1
```

`scf.DFTU.Type=1` corresponds to the so-called 'simplified rotationally invariant form'
by Dudarev *et al.* [[25](bibliography.md#Dudarev1998)] as implemented in the previous versions of OpenMX [[20](bibliography.md#Han2)],
where only $U$ (Hubbard $U$) plays a role.
In more general DFT+$U$ schemes, not only $U$ but also $J$ (Hund's coupling $J$) are used as input parameters.
Note that the keyword 'scf.SpinPolarization' should be always switched on, meaning that
'on' or 'nc' has to be specified, whenever the DFT+U methods are used.

<a id="1975"></a>
The occupation number operator [[20](bibliography.md#Han2)] is specified by the following keyword:

```text

  scf.Hubbard.Occupation        dual  # onsite|full|dual, default=dual
```

Among three occupation number operators, only the dual operator satisfies a sum rule that the trace of
occupation number matrix gives the total number of electrons. For the details of the operators onsite,
full, and dual, see Ref. [[20](bibliography.md#Han2)].

The $U$ and $J$ values in eV on each orbital of species defined by

```text

  <Definition.of.Atomic.Species
    Ni Ni6.0S-s2p2d2f1  Ni_CA13S
    O  O5.0-s2p2d1      O_CA13
  Definition.of.Atomic.Species>
```

are specified by

```text

  <Hubbard.U.values   # eV
    Ni 1s 0.0 2s 0.0 1p 0.0 2p 0.0 1d 5.0 2d 0.0 1f 0.0
    O  1s 0.0 2s 0.0 1p 0.0 2p 0.0 1d 0.0
  Hubbard.U.values>
```

and

```text

  <Hund.J.values      # eV
    Ni 1s 0.0 2s 0.0 1p 0.0 2p 0.0 1d 0.9 2d 0.0 1f 0.0
    O  1s 0.0 2s 0.0 1p 0.0 2p 0.0 1d 0.0
  Hund.J.values>
```

The beginning of the description must be `<Hubbard.U.values` (`<Hund.J.values`),
and the last of the description must be `Hubbard.U.values>` (`Hund.J.values>`) for $U$ ($J$).
For all the basis orbitals, you have to give $U$ and $J$ values in eV as in the above format.
The '1s' and '2s' mean the first and second $s$-orbital, and the number behind '1s' is the
$U$ (or $J$) value for the first $s$-orbital. The same rule is applied to $p$- and $d$-orbitals.
When `scf.DFTU.Type=1`, only $U$ values are read and thus users do not need to specify $J$ values.
