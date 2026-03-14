<a id="SECTION000240000000000000000"></a>
# Order($N$) method

The computational effort of the conventional diagonalization scheme
scales as the third power of the number of basis orbitals, which means
that the part could be a bottleneck when large-scale systems are calculated.
On the other hand, the O($N$) methods can solve the eigenvalue problem
in O($N$) operation in exchange for accuracy.
Thus, O($N$) methods could be efficient for large-scale systems, while
a careful consideration is always required for the accuracy.
In OpenMX Ver. 3.9, three O($N$) methods are available:
a divide-conquer (DC) method [[50](bibliography.md#DC)], a divide-conquer (DC) method with localized natural orbitals (LNO) [[51](bibliography.md#DC-LNO)],
and a Krylov subspace method [[43](bibliography.md#Ozaki3)].
Our recommendation among the three O($N$) methods is the DC-LNO method, since the method is robust, and can be applied to
a wide range of materials including metals, and the parallel efficiency is expected to be the best one among the three methods.
In the following subsections each O($N$) method is illustrated by examples.

---

**Subsections**

- [Divide-conquer method](divide-conquer-method.md)
- [Divide-conquer method with localized natural orbitals (DC-LNO) method](divide-conquer-method-with-localized-natural-orbitals-dc-lno-method.md)
- [Krylov subspace method](krylov-subspace-method.md)
- [User definition of FNAN+SNAN](user-definition-of-fnan-plus-snan.md)

---
