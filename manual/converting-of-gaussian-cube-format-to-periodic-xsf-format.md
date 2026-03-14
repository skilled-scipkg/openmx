<a id="SECTION000740000000000000000"></a>
# Converting of Gaussian cube format to periodic XSF format

When we use a volumetric data-visualization software (such as VESTA and XCrysDen),
the acceptable operation is dependent on the data format and the keyword.
The current version of VESTA (at 2015/8) cannot display a periodic structure
with the Gaussian cube format input file;
we have to use a periodic XSF format-input file to display a periodic structure.
OpenMX produces Gaussian cube format files of the charge/spin density,
Kohn-Sham orbitals, eiggenchannels, and so on;
A tool (`cube2xsf`) to convert the Gaussian cube format to the periodic XSF format is prepared.

The usage of it is as follows:

```text

  $ cube2xsf a.cube
  $ cube2xsf b.cube.bin
  $ cube2xsf a.cube b.cube.bin
  $ cube2xsf *.cube.bin
```

Then, files that have `.xsf` extention are generated.

---
