<a id="SECTION000181000000000000000"></a>
## NVE molecular dynamics (NVE)

<a id="1095"></a>
A constant energy molecular dynamics simulation is performed by the following
keyword 'MD.Type':

```text

    MD.Type          NVE       # NOMD|Opt|NVE|NVT_VS|NVT_VS2|NVT_NH
```

Calculated quantities at every MD step are stored in an output
file '*System.Name*.ene', where *System.Name* means 'System.Name'.
Although you can find the details in 'iterout.c' in the directory 'source',
several quantities are summarized for your convenience as follows:

```text

         1:    MD step
         2:    MD time
        14:    kinetic energy of nuclear motion, Ukc (Hartree)  
        15:    DFT total energy, Utot (Hartree)  
        16:    Utot + Ukc (Hartree)  
        17:    Fermi energy (Hartree)
```

which means that the first and second columns correspond to
MD step and MD time, and so on.

---
