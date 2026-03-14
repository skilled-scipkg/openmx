<a id="SECTION000700000000000000000"></a>
# Automatic force tester

An effective way of assuring the reliability of implementation
of many functionalities is to compare analytic and numerical forces.
If any program bug is introduced, they will not be consistent with each
other. To do this, one can run an automatic tester by

**For serial running**

```text

  % ./openmx -forcetest 0
```

**For parallel running**

```text

  % ./openmx -forcetest 0 "mpirun -np 4 openmx"
```

where '0' is a flag to specify energy terms to be included
in the consistency check, and one can change 0 to 8.
Each number corresponds to

```text

  flag           0   1   2   3   4   5   6   7   8  

  Kinetic        1   0   1   0   0   0   0   0   0  
  Non-local      1   0   0   1   0   0   0   0   0  
  Neutral atom   1   0   0   0   1   0   0   0   0  
  diff Hartree   1   0   0   0   0   1   0   0   0  
  Ex-Corr        1   0   0   0   0   0   1   0   0  
  E. Field       1   0   0   0   0   0   0   1   0  
  Hubbard U      1   0   0   0   0   0   0   0   1
```

where '1' means that it is included in the force consistency check.
In a directory 'work/force_example', there are 36 test inputs which
are used for the force consistency check. After finishing the test,
a file 'forcetest.result' is generated in the directory 'work'.
You will see results of the comparison as follows:

```text

  force_example/C2_GGA.dat
  flag= 0
  Numerical force= -(Utot(s+ds)-Utot(s-ds))/(2*ds)
  ds=   0.0003000000
  Forces (Hartree/Bohr) on atom 1
  x              y               z
  Analytic force       -1.676203071292 -1.397113794193 -1.117456296887
  Numerical force      -1.676101156844 -1.397036485449 -1.117288361652
  diff                 -0.000101914447 -0.000077308744 -0.000167935235

  force_example/C2_LDA.dat
  flag= 0
  Numerical force= -(Utot(s+ds)-Utot(s-ds))/(2*ds)
  ......
  ....
```

---
