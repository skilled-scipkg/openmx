<a id="SECTION000434000000000000000"></a>
## Preparation of config file for jx

For the execution of 'jx' in OpenMX 3.9 implementation, it is necessary to specify a couple of parameters in a configuration file,
which should be written in the same format to that of OpenMX input files.

<a id="2366"></a>
<a id="2367"></a>
<a id="2368"></a>
<a id="2369"></a>
<a id="2370"></a>
<a id="2371"></a>
An example of 'jx.config' is shown below:

```text
                                   
     Flag.PeriodicSum           off       # default - off
     Num.Poles                  60 
     Num.Kgrid                  27 27 27
     Num.ij.pairs               236
     Bunch.ij.pairs             236
     <ijpairs.cellid
       1 1 -2 -2 -2
       1 1 -2 -2 -1
       1 1 -2 -2 0
        ...
        ...
       2 2 0 -1 2
       2 2 0 0 -2
       2 2 0 0 -1
     ijpairs.cellid>
```

Each keyword is explained below:

```text

     Flag.PeriodicSum           off       # default - off
```

This flag determines how you calculate the exchange couplings.
When 'on' for periodic systems, the program derives the $J_{ij}$ based on Eq. ([8](exchange-coupling-parameter-general.md#eq:Jij_periodic)).
When 'off' for periodic systems, the program derives the
$J_{i\mathbf{0},j\mathbf{R}}$ based on Eq. ([5](exchange-coupling-parameter-general.md#eq:Jij_indiv_res)).
This flag has no role in cluster calculations. For cluster calculations,
the program calculates $J_{ij}$ by Eq. ([3](exchange-coupling-parameter-general.md#eq:Jij_cluster)).

```text
 
     Num.Poles                  60
```

This keyword specifies the number of poles
$N_{\mathrm{P}}$ for the finite pole approximation
of Fermi function [[74](bibliography.md#Ozaki_FD)], appearing in Eq. ([5](exchange-coupling-parameter-general.md#eq:Jij_indiv_res)).
The computation becomes more accurate as increasing the number of poles at the cost of execution time.
The most appropriate value depends on the system, and for bcc-Fe a proper value is evaluated as
about 60 to attain the accuracy of 0.05 meV. For the electronic temperature of 300 K, the 60 poles
might be enough in most cases.
However, you can take larger value so as to attain further computational accuracy,
because the computational times to construct each exchange coupling were proven much
smaller than that of eigenvalue calculation.

```text

     Num.Kgrid                  27 27 27
```

This keyword specifies the number of $k$-grids. These values should be same or a bit larger
than those in OpenMX calculation. No role in cluster calculations.

```text

     Num.ij.pairs               236        # NOTE: Number of ij pairs.
```

This keyword specifies how many exchange coupling constants to be calculated.
The value must be same as the number of rows between
the keywords `<ijpairs.cellid` and `ijpairs.cellid>`.

```text

     <ijpairs.cellid
       1 1 -2 -2 -2
       1 1 -2 -2 -1
       1 1 -2 -2 0
        ...
        ...
       2 2 0 -1 2
       2 2 0 0 -2
       2 2 0 0 -1
     ijpairs.cellid>
```

This field specifies the sites $i$, $j$, and
cell vector
$\mathbf{R}=l_1\mathbf{a}_{1}+l_2\mathbf{a}_{2}+l_3\mathbf{a}_{3}$
of
$J_{i\mathbf{0},j\mathbf{R}}$, where
$\mathbf{a}_{1}$,
$\mathbf{a}_{2}$
and
$\mathbf{a}_{3}$ are unit lattice vectors in the OpenMX input.
The data order of this field is as follows: $i$ $j$ $l_1$ $l_2$ $l_3$.
In the case of cluster or periodic image calculations, you should use alternative field as follows:

```text

     <ijpairs.nocellid
       1 1
       1 2
     ijpairs.nocellid>
```

because they do not use cell vectors in $J_{ij}$ calculations.

```text

     Bunch.ij.pairs           236        # default=Num.ij.pairs
```

This is an optional keyword to use when the memory consumption is too large at the default setting.
This value should be same to or smaller than `Num.ij.pairs`.
The smaller Bunch.ij.pairs results in smaller memory consumption with larger calculation time.
