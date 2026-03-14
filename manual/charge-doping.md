<a id="SECTION000290000000000000000"></a>
# Charge doping

The following keyword is available for both the electron and hole dopings.

```text

    scf.system.charge     1.0     # default=0.0
```

The plus and minus signs correspond to hole and electron dopings,
respectively.
A partial charge doping is also possible. The excess charge
given by the keyword 'scf.system.charge' is compensated
by a uniform background opposite charge, since FFT is used
to solve Poisson's equation in OpenMX. Therefore, if you compare
the total energy between different charged states, a careful
treatment is required, because additional electrostatic interactions
induced by the background charge are included in the total energy.
Note that in Sec. [58](ionization-potential-and-electron-affinity-of-gaseous-systems.md#sec:Ionization_potential_and_electron_affinity_of_gaseous_systems),
a proper way of treating charged and isolated systems is discussed.

As an example, we show spin densities of hole doped, neutral, and
electron doped (5,5) carbon nanotubes with a finite length
of 14 Å in Fig. [29](charge-doping.md#fig:nt140_sden).
The neutral and electron doped nanotubes possess the total spin
moment of 1.0 and 2.2, while the total spin moment almost disappears
in the hole doped nanotube. We can see that the spin polarization
takes place at the edges of the neutral and electron doped nanotubes
due to dangling bonds of edge regions.

<a id="fig:nt140_sden"></a>
<a id="1699"></a>
| ![\includegraphics[width=17.0cm]{nt140_sden.eps}](assets/img188.png) |
| --- |
