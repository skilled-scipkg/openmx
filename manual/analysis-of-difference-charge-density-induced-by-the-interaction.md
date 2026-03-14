<a id="SECTION000660000000000000000"></a>
# Analysis of difference charge density induced by the interaction

The redistribution of charge (spin) density induced by the interaction between
two systems A and B can be analyzed by the following procedure:

**(i) Calculate the composite system consisting of A and B**

Then, you will have a cube file for charge (spin) density. Let it be 'AB.cube'.
Also, you will find 'Grid_Origin' in the standard output which gives $x$-, $y$-,
and $z$-components of the origin of the regular grid as:

```text

  Grid_Origin  xxx  yyy  zzz
```

The values will be used in the following calculations (ii) and (iii).

**(ii) Calculate the system A**

This calculation must be performed by the same calculation condition with the
same unit cell as in the composite system consisting of A and B.
Also, the coordinates of the system A must be the same as in the calculation (i).
To use the same origin as in the calculation (i) rather than the use of
an automatically determined origin, you have to include the following keyword
in your input file:

```text

  scf.fixed.grid  xxx  yyy  zzz
```

where 'xxx yyy zzz' is the coordinate of the origin you got in the calculation (i).
Then, you will have a cube file for charge (spin) density. Let it be 'A.cube'.

**(iii) Calculate the system B**

As well as the calculation (ii), this calculation must be performed by the
same calculation condition with the same unit cell as in the composite system
consisting of A and B. Also, the coordinates of the system B must be the same
as in the calculation (i). To use the same origin as in the calculation (i)
rather than the use of an automatically determined origin, you have to include
the following keyword in your input file:

```text

  scf.fixed.grid  xxx  yyy  zzz
```

where 'xxx yyy zzz' is the coordinate of the origin you got in the calculation (i).
Then, you will have a cube file for charge (spin) density. Let it be 'B.cube'.

**(iv) Compile two codes**

compile two codes as follows:

```text

  % gcc diff_gcube.c -lm -o diff_gcube
  % gcc add_gcube.c -lm -o add_gcube
```

**(v) Generate a cube file for difference charge (spin) density**

First, generate a cube file for the superposition of two charge (spin) densities
of the systems A and B by

```text

  % ./add_gcube A.cube B.cube A_B.cube
```

The file 'A_B.cube' is the cube file for the superposition of charge (spin)
density of two isolated systems. Then, you can generate a cube file for the
difference charge (spin) density induced by the interaction as follows:

```text

  % ./diff_gcube AB.cube A_B.cube dAB.cube
```

The file 'dAB.cube' is the cube file for the difference charge (spin) density
induced by the interaction, where the difference means (AB - A_B).
