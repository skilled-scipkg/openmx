<a id="SECTION000710000000000000000"></a>
# Automatic memory leak tester

In OpenMX, the memory used is dynamically allocated when it is required.
However, the dynamic memory allocation causes often a serious memory leak
which wastes the memory used as the MD steps increase.
To check the memory leak, one can run OpenMX as follows:

**For serial running**

```text

  % ./openmx -mltest
```

**For parallel running**

```text

  % ./openmx -mltest "mpirun -np 4 openmx"
```

By monitoring VSZ and RSS actually used at the same monitoring point
in the program code for 14 test inputs
in a directory 'work/ml_example', one can find whether
the memory leak takes place or not.
After finishing the run, a file 'mltest.result' is generated
in the directory 'work'.
You will see the monitored VSZ and RSS as a function of MD steps
as follows:

```text

    1     ml_example/DIA8.dat             

                   CPU (%)     VSZ (kbyte)    RSS (kbyte)
 MD_iter=   1      68.300     397396         123076
 MD_iter=   2      96.400     436264         131916
 MD_iter=   3      99.000     436264         131916
 MD_iter=   4      97.900     436264         131916
 MD_iter=   5      98.800     436264         131916
 MD_iter=   6      99.300     436264         131916
 MD_iter=   7      98.800     436264         131916
 MD_iter=   8      99.200     436264         131916
 MD_iter=   9      99.500     436264         131916
 MD_iter=  10      99.100     436264         131916
 MD_iter=  11      99.400     436264         131916
 MD_iter=  12      99.500     436264         131916
 MD_iter=  13      99.300     436260         131916
 MD_iter=  14      99.500     436264         131916
 MD_iter=  15      99.300     436264         131916
 MD_iter=  16      99.500     436260         131916
 MD_iter=  17      99.600     436264         131916
 MD_iter=  18      99.400     436264         131916
 MD_iter=  19      99.600     436264         133848
 MD_iter=  20      99.400     436264         133848
 MD_iter=  21      99.500     436264         133848
 MD_iter=  22      99.600     436264         133848
 MD_iter=  23      99.500     436264         133848
 MD_iter=  24      99.500     436264         133848
 MD_iter=  25      99.700     436264         133848
 MD_iter=  26      99.500     436264         133848
 MD_iter=  27      99.600     436264         133848
 MD_iter=  28      99.500     436264         133848
 MD_iter=  29      99.600     436264         133848
 MD_iter=  30      99.600     436264         133848

    2     ml_example/DIA8_DC.dat          

                   CPU (%)     VSZ (kbyte)    RSS (kbyte)
 MD_iter=   1     101.000     412508         136448
 MD_iter=   2     100.000     516940         210312
 MD_iter=   3      98.200     517016         210440
 MD_iter=   4      98.900     517016         210440
 MD_iter=   5      99.300     517016         210440
 MD_iter=   6      99.500     517016         210440
    ......
    ....
```

---
