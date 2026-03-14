<a id="SECTION000445000000000000000"></a>
## Running again the step 3 only

We can skip the NEGF calculation if it is finished in the previous `openmx` execution.
In this case, please specify the following keyword:

```text

   NEGF.tran.SCF.skip  on
```

`openmx` reads a file *System.Name*`.tranb` generated in the previous
step 2 calculation, and calculates the transmission, eigenchannels, and so on.

<a id="2831"></a>
<a id="2832"></a>
<a id="2833"></a>
On the other hand, if we intend to stop `openmx` after it finishes the step 2 calculation,
the following keywords
should be set as follows:

```text

   NEGF.tran.SCF.skip  off
   NEGF.tran.Analysis  off
   NEGF.tran.Channel   off
```

---
