<a id="SECTION000173000000000000000"></a>
## Constraint for cell vectors

<a id="1059"></a>
When the options 'OptC1', 'OptC2', or 'OptC5' is used for the keyword 'MD.Type', each Cartesian component
of cell vectors can be fixed at the initial value by using the following keyword :

```text

    <MD.Fixed.Cell.Vectors
     0 0 1
     0 0 0
     0 0 0
    MD.Fixed.Cell.Vectors>
```

where the first line provides the flag for $a_x$, $a_y$, $a_z$, the second $b_x$, $b_y$, $b_z$,
and the third $c_x$, $c_y$, $c_z$, respectively.
'1' means that the component is fixed, and '0' relaxed.

---
