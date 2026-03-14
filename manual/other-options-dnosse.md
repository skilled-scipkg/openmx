<a id="SECTION00046100000000000000"></a>
### -Dnosse

Since the routine (Krylov.c) for the O($N$) Krylov subspace method has been optimized using
Streaming SIMD Extensions (SSE), the code will be compiled including SSE on default compilation.
If your processors do not support SSE, then include '-Dnosse' as compilation option
for **CC**.

---
