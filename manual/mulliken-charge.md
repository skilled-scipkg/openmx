<a id="SECTION000331000000000000000"></a>
## Mulliken charge

The Mulliken charges are output in '*System.Name*.out' by default as shown in
Section 'Test calculation'.
In addition to the Mulliken charge projected to each atom, you can
also find a decomposed Mulliken charge to each orbital in '*System.Name*.out'.
The result stored in '*System.Name*.out' for a methane molecule is as follows:

```text

  Decomposed Mulliken populations

    1    C          Up spin      Down spin     Sum           Diff
            multiple
  s           0    0.598003833  0.598003833   1.196007667   0.000000000
   sum over m      0.598003833  0.598003833   1.196007667   0.000000000
   sum over m+mul  0.598003833  0.598003833   1.196007667   0.000000000
  px          0    0.588514081  0.588514081   1.177028163   0.000000000
  py          0    0.588703212  0.588703212   1.177406424   0.000000000
  pz          0    0.588514081  0.588514081   1.177028162   0.000000000
   sum over m      1.765731375  1.765731375   3.531462749   0.000000000
   sum over m+mul  1.765731375  1.765731375   3.531462749   0.000000000

    2    H          Up spin      Down spin     Sum           Diff
            multiple
  s           0    0.409066346  0.409066346   0.818132693   0.000000000
   sum over m      0.409066346  0.409066346   0.818132693   0.000000000
   sum over m+mul  0.409066346  0.409066346   0.818132693   0.000000000

    3    H          Up spin      Down spin     Sum           Diff
            multiple
  s           0    0.409065912  0.409065912   0.818131824   0.000000000
   sum over m      0.409065912  0.409065912   0.818131824   0.000000000
   sum over m+mul  0.409065912  0.409065912   0.818131824   0.000000000

   .......
   ....
```

As you can see, the Mulliken charges are decomposed for all the orbitals.
There are two kind of summations in this decomposition.
One of the summations is 'sum over m' which means a summation over
magnetic quantum number for each multiple orbital.
The second summation is 'sum over m+mul' which means a summation
over both magnetic quantum number and orbital multiplicity, where
"multiple" means a number to specify a radial wave function.
Therefore, Mulliken charges are decomposed to contributions of
all the orbitals.

---
