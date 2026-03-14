<a id="SECTION000640000000000000000"></a>
<a id="sec:Analysis_of_difference_in_two_Gaussian_cube_files"></a>
# Analysis of difference in two Gaussian cube files

A utility tool is provided to generate a Gaussian cube file
which stores the difference between two Gaussian cube files
for total charge density, spin density, and potentials.
If you analyze the difference between two states, this tool
would be useful.

**(1) Compiling of diff_gcube.c**

There is a file 'diff_gcube.c' in the directory 'source'.
Compile the file as follows:

```text

  % gcc diff_gcube.c -lm -o diff_gcube
```

When the compile is completed normally, then you can find
an executable file 'diff_gcube' in the directory 'source'.
Please copy the executable file to the directory 'work'.

**(2) Calculation of the difference**

If you want to know the difference between two Gaussian cube files
'input1.cube' and 'input2.cube', and output the result to a file
'output.cube', then perform the executable file as follows:

```text

  % ./diff_gcube input1.cube input2.cube output.cube
```

The difference is output to 'output.cube' in the Gaussian cube format.
Thus, you can easily visualize the difference using many software,
such XCrySDen [[105](bibliography.md#XCrySDen)], VESTA [[103](bibliography.md#VESTA)], and Molekel [[104](bibliography.md#Molekel)].
In fact, Fig. [28](electric-field.md#fig:nben_diff) in the Section 'Electric field' was made
by this procedure.

---
