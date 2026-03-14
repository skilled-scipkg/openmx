<a id="SECTION000172000000000000000"></a>
## Stress tensor

In the previous subsection, we discussed how the variable cell optimizations can be performed by specifying
the keyword 'MD.Type'.
In these cases, the stress tensor is automatically calculated by analytically evaluating
the gradient of the total energy with respect to strain, and then transformed to the gradients
with respect to cell vectors.
If you do not perform the variable cell optimization, and however want to calculate the gradient of
the total energy with respect to cell vectors, the following keyword is available:

```text

     scf.stress.tensor  on  # on|off, default=off
```

When the keyword 'scf.stress.tensor' is switched on, you may find the gradient of the total energy
with respect cell vectors in '*System.Name*.out.

---
