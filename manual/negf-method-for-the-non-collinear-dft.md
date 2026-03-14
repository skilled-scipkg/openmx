<a id="SECTION000449000000000000000"></a>
## NEGF method for the non-collinear DFT

OpenMX Ver. 3.9 supports the NEGF method coupled with the non-collinear DFT method,
which can be regarded as a full implementation of NEGF within NC-DFT.
The spin-orbit coupling, the DFT+$U$ method, and the constraint schemes to control
direction of spin and orbital magnetic moments supported for NC-DFT are all compatible
with the implementation of the NEGF method.
Thus, it is expected that a wide variety of problems can be treated, such as transport through
magnetic domains with spiral magnetic structure.
The usage of the functionality is the same as that for the collinear DFT case.

As an example, we show a result for zigzag graphene nanoribbon calculated by the NEGF method
coupled with NC-DFT in Fig. [46](negf-method-for-the-non-collinear-dft.md#fig:NEGF-ZGNR-NC).
It is assumed that spin moments at the zigzag edges align upward and rightward in the left and
right leads, respectively. Those calculations were performed by the conventional NC band structure
method with the constraint scheme as the step 1. Then, any constraint was not applied in the
calculation of the step 2. After getting the SCF convergence in the step 2, it is found that
the spin direction gradually rotates in the central region as shown in Fig. [46](negf-method-for-the-non-collinear-dft.md#fig:NEGF-ZGNR-NC)(a).
The calculations can be traced by input files 'Lead-L-8ZGNR-NC.dat', 'Lead-R-8ZGNR-NC.dat', and
'NEGF-8ZGNR-NC.dat' stored in the directory 'work/negf_example'.
Also, you will find another example for input files of a gold chain in the same directory.

<a id="fig:NEGF-ZGNR-NC"></a>
<a id="6337"></a>
| ![\includegraphics[width=15.0cm]{NEGF-ZGNR-NC.eps}](assets/img316.png) |
| --- |
