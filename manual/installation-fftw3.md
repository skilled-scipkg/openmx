<a id="SECTION00045000000000000000"></a>
## FFTW3

OpenMX Ver. 3.9 supports only FFTW3, while older versions up to Ver. 3.6 also support
FFTW2 as well as FFTW3. Then, you may link FFTW3 in your makefile as follows:

```text

     LIB = -lfftw3
```

We wonder that many users will use the built-in libarary of FFTW3 in the Intel MKL.

---
