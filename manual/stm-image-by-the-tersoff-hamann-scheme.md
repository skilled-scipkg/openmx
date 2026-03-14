<a id="SECTION000510000000000000000"></a>
# STM image by the Tersoff-Hamann scheme

<a id="3564"></a>
<a id="3565"></a>
Scanning tunneling microscope (STM) image can be obtained by the Tersoff-Hamann
scheme [[71](bibliography.md#TersoffHamann)]. The method is nothing but calculation of partial charge
density in an energy window measured from the chemical potential. The calculation
of the partial charge density is performed by the following keywords:

```text

  partial.charge                 on       # on|off, default=off
  partial.charge.energy.window   0.0      # in eV
```

where the second keyword defines an energy window (in eV) measured from
the chemical potential (a plus value means conduction band and negative valence).
Since the calculation of the partial charge density is performed during calculation
of the density of states (DOS), the following keywords have to be specified as well:

```text

  Dos.fileout                  on        # on|off, default=off
  Dos.Erange              -20.0  20.0    # default = -20 20
  Dos.Kgrid                  5 5 5       # default = Kgrid1 Kgrid2 Kgrid3
```

After the calculation with the keywords, you will get '*System.Name*.pden.cube' which can
be used for the STM simulation within the Tersoff-Hamman approximation.
As an example, a simulated STM image of a graphene layer is shown in Fig. [59](stm-image-by-the-tersoff-hamann-scheme.md#fig:STM1).

<a id="fig:STM1"></a>
<a id="6367"></a>
| ![\includegraphics[width=9.0cm]{STM1.eps}](assets/img400.png) |
| --- |
