<a id="SECTION000446000000000000000"></a>
## Periodic system under zero bias

<a id="2839"></a>
When the transmission of a system with the periodicity along the **a**-axis
as well as the periodicity of the **bc**-plane is evaluated under zero
bias voltage,
it can be easily obtained by making use of the Hamiltonian calculated
by the conventional band structure calculation without employing the Green
function method.
This scheme enables us to explore transport properties for a wide variety
of possible geometric and magnetic structures with a low computational cost, and
thereby can be very useful for many materials such as superlattice structures.
The calculation is performed by adding a keyword
'NEGF.Output.for.TranMain':

```text

  NEGF.Output.for.TranMain    on
```

in the band structure calculation of the step 1. Then, after the calculation of
the step 1, you will obtain a file '*System.Name*.tranb' which can be used in the calculation
of the step 3, which means that you can skip the calculation of the step 2.

---
