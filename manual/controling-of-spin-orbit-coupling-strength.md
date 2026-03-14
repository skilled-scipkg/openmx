<a id="SECTION000362000000000000000"></a>
## Controling of spin-orbit coupling strength

<a id="1924"></a>
In OpenMX Ver. 3.9, it is possible to contol the spin-orbit coupling strength using a conventional
pseudopotential stored in the database Ver. 2019 without generating a special pseudopotential with
a larger or smaller spin-orbit coupling. The scaling factors can be specified to each angular momentum
quantum number by the following keyword:

```text

  <scf.SO.factor
    Ga  s 1.0 p 2.0 d 1.0 f 1.0
    As  s 1.0 p 2.0 d 1.0 f 1.0
  scf.SO.factor>
```

The first column is the name of species which is defined by the keyword 'Definition.of.Atomic.Species', and
followed by the subsequent columns: a symbol for angular momentum quantum number and a scaling factor.
The '1.0' corresponds to the spin-orbit coupling strength in the channel with the angular momentum quantum
number in the real atom. The set of information needs to be specified up to the f-channel for all the species
in your system regardless of a kind of pseudopotentials.

---
