<a id="SECTION000720000000000000000"></a>
# Analysis of memory usage

<a id="5756"></a>
The memory usage can be found by analyzing files '*.memory0', '*.memory1',..., and '*.memory#',
where '*' is the file name specified by the keyword 'System.Name' and the number in
the file extension corresponds to process ID in the MPI parallelization.
The files are output by setting the keyword 'memory.usage.fileout' as

```text

  memory.usage.fileout   on   # default=off, on|off
```

As an example 'met.memory0' is shown below

```text

  Memory: SetPara_DFT: Spe_PAO_XV                             0.01 MBytes
  Memory: SetPara_DFT: Spe_PAO_RV                             0.01 MBytes
  Memory: SetPara_DFT: Spe_Atomic_Den                         0.01 MBytes
  Memory: SetPara_DFT: Spe_PAO_RWF                            0.57 MBytes
  Memory: SetPara_DFT: Spe_RF_Bessel                          1.03 MBytes
  Memory: SetPara_DFT: Spe_VPS_XV                             0.01 MBytes
  Memory: SetPara_DFT: Spe_VPS_RV                             0.01 MBytes
  Memory: SetPara_DFT: Spe_Vna                                0.01 MBytes
  Memory: SetPara_DFT: Spe_VH_Atom                            0.01 MBytes
  Memory: SetPara_DFT: Spe_Atomic_PCC                         0.01 MBytes
  Memory: SetPara_DFT: Spe_VNL                                0.11 MBytes
  Memory: SetPara_DFT: Spe_VNLE                               0.00 MBytes
  Memory: SetPara_DFT: Spe_VPS_List                           0.00 MBytes
  .....
  ....
  ...
  Memory: Poisson: array0                                     4.00 MBytes
  Memory: Poisson: array1                                     4.00 MBytes
  Memory: Poisson: request_send                               0.00 MBytes
  Memory: Poisson: stat_send                                  0.00 MBytes
  Memory: Poisson: request_recv                               0.00 MBytes
  Memory: Poisson: stat_recv                                  0.00 MBytes
  Memory: Force: Hx                                           0.00 MBytes
  Memory: Force: Hy                                           0.00 MBytes
  Memory: Force: Hz                                           0.00 MBytes
  Memory: Force: CDM0                                         0.00 MBytes
  Memory: Data_Grid_Copy_B2C_1: Work_Array_Snd_Grid_B2C       0.72 MBytes
  Memory: Data_Grid_Copy_B2C_1: Work_Array_Rcv_Grid_B2C       0.72 MBytes
  Memory: total                                             256.99 MBytes
```

The file can be obtained by setting the keyword in the input file 'Methane.dat' and performing
a single process. Note that memory usages for most of arrays are listed in the file, but the list
is not complete.

---
